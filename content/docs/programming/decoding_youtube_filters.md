+++
title = "Decoding Youtube filters"
date = 2021-10-28
draft = false
template = "docs/page.html"

[extra]
toc = false 
top = false
+++

# Introduction
Recently, I was searching for some videos on Youtube and noticed the search filters aren't passed to the server as a series of key-value strings on the URL as one might expect, e.g.:
```
https://www.youtube.com/results?search_query=cassini?type=video&features=4k
```
Instead, all the active filters are somehow combined and hashed to the `sp` query parameter. So the valid version of the previously mentioned URL is:
```
https://www.youtube.com/results?search_query=cassini&sp=EgQQAXAB
```
There is some function on Youtube that encodes Type: **Video** and Features: **4K** filters to `EgQQAXAB`. I can only assume what's the reasoning behind such an opaque approach. More importantly, it made me curious how the encoding works concretely. Hence as a little mental excercise, I set out to decode it.

# Reading the data
`EgQQAXAB` looks like base64 encoded data, so let's fire up **ptpython** and try to decode it:
```python
>>> import base64
>>>
>>> filter = 'EgQQAXAB'
>>> bytes = base64.b64decode(filter)
>>> bytes
b'\x12\x04\x10\x01p\x01'
>>> bytes.decode('utf-8')
'\x12\x04\x10\x01p\x01'
```
We're dealing with some binary that is not a utf-8 string. Hence converting the bytes to a more explorable form is the logical next step:
```python
>>> [format(byte, '08b') for byte in bytes]
['00010010', '00000100', '00010000', '00000001', '01110000', '00000001']
```
Ok, we're in. What now?

There's not much else to do besides looking at various combinations of filters and trying to spot pattern(s).

What about `EgQQASAB` that encodes Type: **Video** and Features: **HD** filters?

```python
>>> filter = 'EgQQASAB'
>>> bytes = base64.b64decode(filter)
>>> [format(byte, '08b') for byte in bytes]
['00010010', '00000100', '00010000', '00000001', '00100000', '00000001']
```
What can we observe?
The first 4 bytes are the same. Fifth is different, so it probably encodes different feature filters:
* `01110000` is **4K** feature filter
* `00100000` is **HD** feature filter


Before validating the assumptions, it would be useful to reduce repetitive code, print bytes in more readable form, and be able to compare different `sp`s.
We can use the following little piece of code to achieve that:
```python
import base64
from tabulate import tabulate


def decode_sp(sp):
    sp = base64.b64decode(sp)

    return [format(byte, '08b') for byte in sp]


def build_header(labeled_sps):
     bytes_len = [len(bytes) for _, bytes in labeled_sps]
     header_bytes_part = [i for i in range(max(bytes_len))]

     return ["label"] + header_bytes_part


def print_sps(sps):
    sps = [(label, decode_sp(sp)) for label, sp in sps]
    header = build_header(sps)
    sps = [[label, *sp] for label, sp in sps]
    table = tabulate(sps, headers=header)

    print(table)
```

That allows us to stay organized and compare various `sp`s:
```python
>>> sps = [('type=video, features=4k', 'EgQQAXAB'), ('type=video, features=hd', 'EgQQASAB')]
>>> print_sps(sps)
label                           0         1         2         3         4         5
-----------------------  --------  --------  --------  --------  --------  --------
type=video, features=4k  00010010  00000100  00010000  00000001  01110000  00000001
type=video, features=hd  00010010  00000100  00010000  00000001  00100000  00000001

```

Moving forward I'm going to format the output to markdown table to further improve readability:

| Label | Hash | B0 | B1 | B2 | B3 | B4 | B5 
| --- | --- | --- | --- | --- | --- | --- | ---  
|type=video, features=4k|EgQQAXAB|00010010|00000100|00010000|00000001|01110000|00000001
|type=video, features=hd|EgQQASAB|00010010|00000100|00010000|00000001|00100000|00000001

# Making sense of the data
What about multiple active features filters?

| Label | Hash | B0 | B1 | B2 | B3 | B4 | B5 | B6 | B7 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|type=video, features=4k|EgQQAXAB|00010010|00000100|00010000|00000001|01110000|00000001|
|type=video, features=hd|EgQQASAB|00010010|00000100|00010000|00000001|00100000|00000001|
|**type=video, features=hd+4k**|EgYQASABcAE=|00010010|00000110|00010000|00000001|00100000|00000001|01110000|00000001|

Now we're talking.

**B0** is a constant (at least in current sample space) and probably a header.

**B1** changed from `00000100` to `00000110` after the introduction of an additional feature.
Is it a counter of active filters? The first two hashes contain 2 filters - `10` in binary, third has three filters - `11` in binary.
Why counting doesn't start at the rightmost bit though?

**B2** is the same for all the filters, it most likely identifies type: **video** filter that has been active for all the configurations.

Moreover, the following may hold:
* `00100000` identifies feature: **HD** filter
* `01110000` identifies feature: **4K** filter
* `00000001` looks like some spacer in between of filters

We can easily validate the counter assumption by applying an additional filter:

| Label | Hash | B0 | B1 | ... |
|--- | --- | --- | --- | --- |
|type=video, features=hd+4k+live|EgQQAXAB|00010010|**00001000**|...|

It's official, **B1** contains a counter that is shifted by one to the left for an unknown reason. We can consider it being part of a header and draft a specification:

### Specification v1
The `sp` hash is base64 encoded binary.
First 2 bytes are header.
The header is followed by one or more filters.

##### Header
| B0 constant | B1 counter |
| -- | -- |
| 00010010 | B7-B1: counter; B0: 0 |

#### Example

| Header - Const | Header - Count: 2 | Type: Video | Spacer? | Features: 4K | Spacer? |
| --- | --- | --- | --- | --- | --- |
|00010010|00000100|00010000|00000001|01110000|00000001


We have some understanding of the header and shape of some filters. Now we can apply different filters to see whether our assumptions hold for those.

## Additional filter types
Let's observe `EgQIAhAB` hash encoding Type: **Video** and Upload date: **Today** filters:

|B0 Header - Const |B1 Header - Count: 2 |B2 ?|B3 ?|B4 Type: Video|B5 Spacer?|
| --- | --- | --- | --- | --- | --- |
|00010010|00000100|**00001000**|**00000010**|00010000|00000001

**B0** and **B1** still hold our assumption. However Type: **Video** filter together with spacer moved from **B2** and **B3** to **B4** and **B5** respectively. Meaning **B2** should identify Upload date: **Today** but **B3** is not usual assumed spacer byte.

Maybe looking at yet another filter type may be of help. Let's check Type: **Video** and Duration: **4 - 20 minutes** given by `EgQQARgD` hash:

|B0 Header - Const |B1 Header - Count: 2 |B2 Type: Video|B3 ?|B4 ?|B5 ?|
| --- | --- | --- | --- | --- | --- |
|00010010|00000100|00010000|00000001|**00011000**|**00000011**|

Type: **Video** is back at **B2** but the spacer assumption is rendered invalid as the **B5** following assumed Duration: **4 - 20 minutes** filter is yet again different.

Here's an idea. What if there's nothing like a spacer and each piece of information in the `sp` hash is composed of **two bytes wide words**? And what if the order of filter words doesn't really matter?

We can try to decode a combination of all known filters to see whether all the assumptions fit well.

The `EgoIAhABGAMgAXAB` hash contains following filters
* Type: **Video**
* Features: **4K** + **HD**
* Duration: **4 - 20 minutes**
* Upload date: **Today**

From previous observations and assumptions made we know that the header should contain 5 in binary - `101` and that the filters should decode as:

| Type: Video | Features: 4K | Features: HD | Upload date: Today | Duration: 4 - 20 mins
| --- | --- | --- | --- | --- |
| 00010000,00000001 | 01110000,00000001 | 00100000,00000001 | 00001000,00000010 | 00011000,00000011 |


Let's try to find a match in whole decoded hash:

|Header Count: 5 |Upload date: Today|Type: Video|Duration: 4-20mins|Features: HD|Features: 4K|
|---|---|---|---|---|--- |
|00010010,00001010|00001000,00000010|00010000,00000001|00011000,00000011|00100000,00000001|01110000,00000001

All good, it seems like our assumptions are valid. Thus we can update our specification.

### Specification v2
The `sp` hash is base64 encoded binary. The binary consists of 2 bytes wide words.
The first word is a header which is followed by one or more filter words.

##### Header
The first byte is constant, second contains a counter of filter words.

| B0 constant | B1 |
| -- | -- |
| 00010010 | b7 - b1: counter; b0: 0 |

##### Filters catalog
###### Type
| Label | Binary value |
| --- | --- |
| Video | 00010000,00000001

###### Features
| Label | Binary value |
| --- | --- |
| 4K | 01110000,00000001
| HD | 00100000,00000001

###### Upload date
| Label | Binary value |
| --- | --- |
| Today | 00001000,00000010

###### Duration
| Label | Binary value |
| --- | --- |
| 4 - 20 minutes | 00011000,00000011

#### Example

| Header Const | Header Count: 2 | Type: Video | Features: 4K |
| --- | --- | --- | --- |
|00010010|00000100|00010000,00000001|01110000,00000001

## Breaking the rules
We can try to tinker with some additional combinations to see whether we fully cracked the encoding logic.
What about usual Type: **Video** combined with Features: **HDR** given by `EgUQAcgBAQ==` hash?

|B0 Header Const | B1 What? | B2-3 Type: Video | B4 ? | B5 ? | B6 ?
| --- | --- | --- | --- | --- | --- |
|00010010|**00000101**|00010000,00000001|11001000|00000001|00000001

Now, this is different.

Bit 0 on the counter got finally activated. **B2** and **B3** clearly identify Type: **Video** filter that is followed by 3 bytes.

The only possible conclusion is that bit 0 of the counter marks the presence of **special 3-bytes long filter**.
That seems to be included in the counter and I assume it will always be the last filter in the hash. Otherwise parsing would be a nightmare.

We can again apply all the known filters together with Features: **HDR** to validate the assumptions. The `Eg0IAhABGAMgAXAByAEB` hash contains the following filters:
* Type: **Video**
* Duration: **4 - 20 minutes**
* Upload date: **Today**
* Features: **4K** + **HD** + **HDR** (new)

Decoding as `00010010  00001101  00001000  00000010  00010000  00000001  00011000  00000011  00100000  00000001  01110000  00000001  11001000  00000001  00000001`
binary that can be broken down to the following sections:

**Header:**

| Const | Count: 6; 3B filter on |
| --- | --- | 
|00010010|00001101|

**Filters:**

|Upload date: Today | Type: Video | Duration: 4-20min | Features: HD | Features: 4K | Features: HDR
| --- | --- | --- | --- | --- | --- |
00001000,00000010|00010000,00000001|00011000,00000011|00100000,00000001|01110000,00000001|11001000,00000001,00000001


Another 3 bytes wide filter is Features: **VR180** given by `EgPQAQE=` (this time without any additional filter):

| Header Const | Header Count: 1; 3B filter on | Features: VR180 |
| --- | --- | --- |
|00010010|00000011|11010000,00000001,00000001

With that cracked we can update our specification and fill it with all the possible filters.

### Specification v3
The `sp` hash is base64 encoded binary.
The binary consists of 2 bytes wide header followed by 2 bytes wide filters.
When the first bit of the header is set, the last filter (tail) is 3 bytes wide.

##### Header
The first byte is constant, second contains a 3-bytes filter tail toggle and a counter of filters.

| B0 constant | B1 |
| -- | -- |
| 00010010 | b7 - b1: counter; b0: 3-bytes filter tail toggle |

###### 3-bytes filter tail toggle
When set, the last filter is 3-bytes wide.

##### Filters catalog
###### Type
| Label | Binary value |
| --- | --- |
| Video | 00010000,00000001
| Channel | 00010000,00000010
| Playlist | 00010000,00000011
| Movie | 00010000,00000100

###### Features
| Label | Binary value |
| --- | --- |
| Live | 01000000,00000001
| 4K | 01110000,00000001
| HD | 00100000,00000001
| Subtitles/CC | 00101000,00000001
| Creative commons | 00110000,00000001
| $360^{\circ}$ | 01111000,00000001
| VR180 (3B) | 11010000,00000001,00000001
| 3D | 00111000,00000001
| HDR (3B) | 11001000,00000001,00000001
| Location (3B) | 10111000,00000001,00000001
| Purchased | 01001000,00000001


###### Upload date
| Label | Binary value |
| --- | --- |
| Last hour | 00001000,00000001
| Today | 00001000,00000010
| This week | 00001000,00000011
| This month | 00001000,00000100
| This year | 00001000,00000101

###### Duration
| Label | Binary value |
| --- | --- |
| Under 4 minutes | 00011000,00000001
| 4 - 20 minutes | 00011000,00000011
| Over 20 minutes | 00011000,00000010

#### Examples

| Header Const | Header Count: 2 | Type: Video | Features: 4K |
| --- | --- | --- | --- |
|00010010|00000100|00010000,00000001|01110000,00000001

| Header Const | Header Count: 1; 3B filter on | Features: VR180 |
| --- | --- | --- |
|00010010|00000011|11010000,00000001,00000001

## Closing thoughts
I believe we cracked the filters quite accurately, I successfully tested a couple of combinations against Youtube. All were accepted and correctly parsed.

Of course, there are some additional nuances to the filters. For example when Type: **Movie** filter is active, only certain additional filters can be appended.
Also, I didn't cover sorting.

The core workings behind the `sp` hash should be covered though. 

One might write an encoder/decoder of the hash based on this breakdown.
As I don't have use of such program I'll leave it on fellow readers that would benefit from it.