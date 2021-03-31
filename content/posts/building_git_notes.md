+++
title = "Building Git notes"
date = 2021-03-31

[taxonomies]
categories = ["programming"]
+++

> These are my notes taken while reading the **Building Git** book ([https://shop.jcoglan.com/building-git/](https://shop.jcoglan.com/building-git/)).

# 2. Getting to know `.git`
## 2.1 The `.git` directory
is called a **repository**
```sh
.git
├── branches
├── config
├── description
├── HEAD
├── hooks
│   ├── ...
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags
```
[https://git-scm.com/docs/gitrepository-layout](https://shop.jcoglan.com/building-git/])

### `.git/config`
A configuration settings that apply only to this directory.

### `.git/description`
A name of the repository, used by gitweb.

### `.git/HEAD`
A reference to the *current commit*, either using that commit's ID or a *symbolic reference* (*symref*).
`HEAD` is used as a parent reference for new commit.
`HEAD` is changed when checking out a branch or specific comit.
When merging, the requested branch is merged with whatever `HEAD` points at.

### `.git/info`
Various pieces of metadata about the repository.

### `.git/hooks`
Scripts that Git will execute as part of certain core commands.

### `.git/objects`
Forms Git's *database*, place where Git stores all the content it tracks. Initial subdirectories are:
* `.git/objects/pack` - for storing objects in an optimised format. Every object added to the database is stored in its own file at first, such an object is called *loose object*. On certain events many individual files are rolled up into a pack - a single file containing many objects in a compressed format. It needs an index describing where to find each object in a pack.
* `.git/objects/info` stores metadata about the packs for use by some of the remote protocols. Also stores links to other object stores.

### `.git/refs`
Stores various kind of pointers into the `.git/objects` database. Usually just files that contain the ID of a commit, e.g.:
* `.git/refs/heads` store the latest commit on each local branch.
* `.git/refs/stash` references to stashed changes in `.git/objects`

## 2.2 A simple commit
```
git commit --message "First commit."
[master (root-commit) 65b1d93] First commit.
 2 files changed, 2 insertions(+)
 create mode 100644 hello.txt
 create mode 100644 world.txt
```
`root-commit` is a commit without any parent.

Newly added files after running a commit:
```
├── COMMIT_EDITMSG
├── index
├── logs
│   ├── HEAD
│   └── refs
│       └── heads
│           └── master
├── objects
│   ├── 65
│   │   └── b1d9312836b1e84233b209d8d066038aead925
│   ├── 88
│   │   └── e38705fdbd3608cddbe904b67c731f3234c45b
│   ├── cc
│   │   └── 628ccd10742baea8241c5924df992b5c019f71
│   ├── ce
│   │   └── 013625030ba8dba906f756967f9e9ca394464a
│   ├── info
│   └── pack
└── refs
    ├── heads
    │   └── master
    └── tags
```

### `.git/COMMIT_EDITMSG`
```
cat .git/COMMIT_EDITMSG 
First commit.
```
Used by Git to compose commit messages. When `--message` is not passed Git opens an editor to compose the commit message. `.git/COMMIT_EDITMSG` is asked to editor to open. After closing GIt will read this file. When `--message` is passed Git still saves it in the file.

### `.git/index`
Binary cache that that stores information about each file in the current commit and which version of each file should be present. Updated when `git add` is run. Is used to build next commit.

### `.git/logs`
Text files containing a log of every time a *ref* (*reference*, something that points to a commit, like `HEAD` or branch name) changes its value, e.g. when:
* making a commit
* checking out a branch
* merging
* rebasing
* ...

A log record for the First commit:
```
0000000000000000000000000000000000000000 65b1d9312836b1e84233b209d8d066038aead925 \
Tomas Koutsky <tomas@stepnivlk.net> 1616955235 +0200	\
commit (initial): First commit.
```
This event changes refs from pointing at nothing (`0000...`) to a commit (`65b1...`). Used by `reflog` command.

### `.git/refs/heads/master`
Records which commit is at the tip of the `master` branch, which `HEAD` is currently reffering to:
```
65b1d9312836b1e84233b209d8d066038aead925
```

## 2.3 Storing objects
Files in:
```
├── objects
│   ├── 65
│   │   └── b1d9312836b1e84233b209d8d066038aead925
│   ├── 88
│   │   └── e38705fdbd3608cddbe904b67c731f3234c45b
│   ├── cc
│   │   └── 628ccd10742baea8241c5924df992b5c019f71
│   ├── ce
│   │   └── 013625030ba8dba906f756967f9e9ca394464a
```
are where Git stores all the objects that make up the content including commits.

The object from a database can be printed using `git cat-file -p <hash>`, e.g.:
```
~> git cat-file -p 65b1d9312836b1e84233b209d8d066038aead925

tree 88e38705fdbd3608cddbe904b67c731f3234c45b
author Tomas Koutsky <tomas@stepnivlk.net> 1616955235 +0200
committer Tomas Koutsky <tomas@stepnivlk.net> 1616955235 +0200

First commit.
```

A *tree* represenets whole tree of files as they were when given commit was made:
```
~> git cat-file -p 88e38705fdbd3608cddbe904b67c731f3234c45b

100644 blob ce013625030ba8dba906f756967f9e9ca394464a	hello.txt
100644 blob cc628ccd10742baea8241c5924df992b5c019f71	world.txt
```
Tree has one tree for every directory. Each entry in a tree is either another tree or a *blob* - regular file. Each entry in a tree lists:
* mode - type + permissions, 100644 is a regular, readable, non-executable file
* type - *blob* or *tree*
* ID
* filename

For blobs, Git just stores their literal contents:
```
~> git cat-file -p ce013625030ba8dba906f756967f9e9ca394464a

hello
```

Git stores objects with first two characters forming directory in order to cope with restrictions of some operating systems when the amount of objects grows. Also it allows for faster lookup.

Objects are compressed:
```
~> cat .git/objects/ce/013625030ba8dba906f756967f9e9ca394464a 

xK��OR0c�H�����⏎ 
```
using DEFLATE (zlib).

Object can be easilly decompressed using ruby:
```
~> cat .git/objects/ce/01.. | ruby -r zlib -e "puts Zlib::Inflate.inflate(STDIN.read)"

blob 6hello
```
The file can be inspected further using hexdump:
```
cat .git/objects/ce/01.. | ruby -r ... | hexdump -C
00000000  62 6c 6f 62 20 36 00 68  65 6c 6c 6f 0a           |blob 6.hello.|
0000000d

```

* `62 6c 6f 62` - `blob` in ASCII
* `20` - space
* `36` `6` in ASCII
* `00` - null byte; separates the header from actual content

So the blobs are stored as zlib compressed:
* the word `blob`
* a space
* the lenght of the blob
* null byte
* the actual data

Trees are different though:
```
~> cat .git/objects/88/e38705fdbd3608cddbe904b67c731f3234c45b | ./inflate.sh | hexdump -C

00000000  74 72 65 65 20 37 34 00  31 30 30 36 34 34 20 68  |tree 74.100644 h|
00000010  65 6c 6c 6f 2e 74 78 74  00 ce 01 36 25 03 0b a8  |ello.txt...6%...|
00000020  db a9 06 f7 56 96 7f 9e  9c a3 94 46 4a 31 30 30  |....V......FJ100|
00000030  36 34 34 20 77 6f 72 6c  64 2e 74 78 74 00 cc 62  |644 world.txt..b|
00000040  8c cd 10 74 2b ae a8 24  1c 59 24 df 99 2b 5c 01  |...t+..$.Y$..+\.|
00000050  9f 71 0a                                          |.q.|
00000053
```
The knowns:
* `tree 74.` - header
* `100644 hello.txt` - a filename with mode
* `100644 world.txt` - a filename with mode

Then there are IDs in packed, 20B format:
* `ce 01 36 25 03 0b a8 db a9 06 f7 56 96 7f 9e 9c a3 94 46 4a`
* `cc 62 8c cd 10 74 2b ae a8 24 1c 59 24 df 99 2b 5c 01 9f 71`
The end of filename is separated using null byte.

The type of an object is implied by its mode - `10` at the beggining of `100644` indicates its a regular file, not a directory.

Commits are simpler:
```
~> cat .git/objects/65/b1d9312836b1e84233b209d8d066038aead925 | ./inflate.sh

commit 184tree 88e38705fdbd3608cddbe904b67c731f3234c45b
author Tomas Koutsky <tomas@stepnivlk.net> 1616955235 +0200
committer Tomas Koutsky <tomas@stepnivlk.net> 1616955235 +0200

First commit.
```
It's simply a series of headers followed by the message. In this commit the headers are:
* `commit 184` - its own header
* `tree` - reference to a single tree representing the state of files at that point in the history.
* `author` - simple metadata
* `committer` - simple metadata

### Computing object IDs
Objects are named by taking SHA-1 hash of their content prepended with a header before compressing them.
SHA-1 is a *cryptographic hash function*, it takes input of arbitrary sized string and outputs a fixed-size 20B number.
It's designed in such a way that it should be effectivelly impossible to find two inputs that has to the same output.
There are $2^{160}$ of possible object IDs so its *computationally infeasible* to find a collision.
This is property is a key to the distributed nature of Git - no two distinct objects in any repository will be given the same ID.
Also comparition becomes simple - if two objects have same ID they are same.

### Problems with SHA-1
A hash is considered broken when there is an attack requiring less than $2^\frac{n}{2}$ ($n$ being the size of the output in bits) inputs to find a collision. For SHA-1 tht means an attack requiring fewer than $2^80$ steps.

In 2005 an attack requiring $5.9 \times 10^{20}$ steps was reported ([https://www.schneier.com/blog/archives/2005/02/cryptanalysis_o.html](https://www.schneier.com/blog/archives/2005/02/cryptanalysis_o.html)).
In 2017 Google announced an attach requiring $9.2 \times 10^{18}$ ([https://shattered.io/](https://shattered.io/))

The migration to SHA-256 is possible however Git doesn't rely on SHA-1 as proof of trust, it's an integrity check against accidental damage. From this perspective SHA-1 is good enough.

Moreover for an attacker to replace an object it's not enough to find a collision, he needs to find collision with concrete blob.

# 3. The first commit
## `init`
The very first step is `git init` the bare essentials for it are `objects` and `refs` folder and `HEAD` file. With those Git will consider the directory valid.

## `commit`
* `Workspace` is responsible for the files in the working tree - all the files that are edited directly, rather than those stored in `.git`.

# 4. Making history
When adding second commit via Git I get:
```sh
~> git commit -m 'Second commit.'
[master 2d719c9] Second commit.
 1 file changed, 1 insertion(+), 1 deletion(-)
```
There's no `root-commit` now since it follows on from the previous commit.

The ID of the second commit is stored in master ref:
```sh
~> cat .git/refs/heads/master
2d719c90a3c181782e6e07e2fd027f90ab5de0b5
```
There's a parent field in the object representing second commit:
```sh
~> git cat-file -p 2d719c90a3c181782e6e07e2fd027f90ab5de0b5
tree 040c6f3e807f0d433870584bc91e06b6046b955d
parent 65b1d9312836b1e84233b209d8d066038aead925
author Tomas Koutsky <tomas@stepnivlk.net> 1617213880 +0200
committer Tomas Koutsky <tomas@stepnivlk.net> 1617213880 +0200

Second commit.
```

The ID behind parent points to the first commit:
```sh
~> git cat-file -p 65b1d9312836b1e84233b209d8d066038aead925
tree 88e38705fdbd3608cddbe904b67c731f3234c45b
author Tomas Koutsky <tomas@stepnivlk.net> 1616955235 +0200
committer Tomas Koutsky <tomas@stepnivlk.net> 1616955235 +0200

First commit.
```
So each commit made after the root one has parent field pointing to previous commit. This allows for understanding of how commits are *causually connected*.

Each tree contains the snapshot of all the files.
First tree:
```sh
~> git cat-file -p 88e38705fdbd3608cddbe904b67c731f3234c45b
100644 blob ce013625030ba8dba906f756967f9e9ca394464a	hello.txt
100644 blob cc628ccd10742baea8241c5924df992b5c019f71	world.txt
```
Second tree:
```sh
~> git cat-file -p 040c6f3e807f0d433870584bc91e06b6046b955d
100644 blob e019be006cf33489e2d0177a3837a2384eddebc5	hello.txt
100644 blob cc628ccd10742baea8241c5924df992b5c019f71	world.txt
```
`world.txt` is same object with same ID as its content didn't change and IDs of objects are derived from their contents.

Thus Git only creates new blobs when files have their content changed. Files with same content will point to same blob even when those files appear in many trees across many commits.
