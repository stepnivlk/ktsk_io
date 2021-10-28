+++
title = "Building Git Notes"
date = 2021-03-31
draft = false
template = "docs/page.html"

[extra]
toc = true
top = false
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
A hash is considered broken when there is an attack requiring less than $2^\frac{n}{2}$ ($n$ being the size of the output in bits) inputs to find a collision. For SHA-1 tht means an attack requiring fewer than $2^{80}$ steps.

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

## 4.2 Implementing the `parent` chain
`.git/HEAD` needs to be updated when storing commits however it has to be done in safe, atomic way as there may be multiple readers. Multiple writers are considered as an error. This can be tackled using a lockfile.

# 5 Growing trees
## 5.1 Executable files
When commiting executable file:
```sh
~> touch cruel.txt
~> chmod +x cruel.txt 
~> git add cruel.txt 
~> git commit -m 'Third commit.'
[master 91c525a] Third commit.
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100755 cruel.txt
```
The mode is `100755` instead of `100644` and it's stored in the tree:
```sh
~> git cat-file -p HEAD^{tree}
100755 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391	cruel.txt
100644 blob e019be006cf33489e2d0177a3837a2384eddebc5	hello.txt
100644 blob cc628ccd10742baea8241c5924df992b5c019f71	world.txt
```
The mode is in base 8, it makes it easier to read in the compact format. First 4 bits are file type related, others are permissions (special, user, group other).
E.g. in `100644`:
* `10` - regular file
* `0` - no special permissions
* `6` - owner can rw
* `4` - members of the group can read
* `4` - others can read
In `100755`:
* `7` - owner can rw + execute
* `5` - members of the group can r + execute
* `5` - others can r + execute

Git only uses very restricted permissions - whether owner can execute, rest is thrown out:
```sh
~> touch out.txt
~> chmod 655 out.txt 
~> git add out.txt 
~> git commit -m 'Forth commit.'
[master 27df932] Forth commit.
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 out.txt
```

Thus Git only has two modes - `100644` and `100755`.

## 5.2 Nested trees
Trees can be arbitrarily nested:
```sh
~> mkdir -p a/b
~> touch a/b/c.txt
~> git add .
~> git commit -m 'First commit.'
~> git cat-file -p HEAD^{tree}

040000 tree c4a644afb090a8303bdb28306a2f803017551f25	a
```
Hexdump:
```sh
~> cat .git/objects/c4/a644afb090a8303bdb28306a2f803017551f25 | ./inflate.sh | hexdump -C
00000000  74 72 65 65 20 32 38 00  34 30 30 30 30 20 62 00  |tree 28.40000 b.|
00000010  17 21 a7 a9 1e 87 f5 41  3c 84 2a 9c 5c e7 3f 67  |.!.....A<.*.\.?g|
00000020  44 59 e9 2b 0a                                    |DY.+.|
00000025
```
The mode is `40000`. In Unix, directories have file type bits set to `4` and permissions to `755`. Git ingones all the permissions and just stores `40000` to indicate it's a directory.
`a` of course points to `b` - another tree.

The content of a tree is just a list of IDs and names of this contents and SHA-1 hashes the content. Thus when two trees have same IDs it means all their contents are same, recursively.
This method of storing a tree of information where each tree is labelled with the has of its children is called a Merkle tree.

Entries in trees have to be sorted in order to compare those effectively. Git sorts the file list for the entire project before building trees, thus it sorts following entries:
```sh
foo # dir with bar.txt entry
foo.txt
```
as:
```sh
foo.txt
foo
```
It sees `foo` as `foo/bar.txt`.

In Git, the `add` command reads the working tree, stores blobs in the database and adds them to the index. `commit` reads the index to create trees. The index is stored as flat list of paths.

# 6. The index
Current `commit` implementation reads and hashes every file in the project in order to store blobs, that's ineffective. Usually, in larger projects, only small subset of files is changed in commit. Moreover, the current implementation is cumbersome to use. The user should control what goes in a commit.

The `add` command and the index solve the problem by providing a cache of all the blobs representing the current state of the project. It contains the object IDs of the blobs corresponding the the current files plus a lot of information from the filesystem (size of files, timestamps).

## 6.2 Inspecting `.git/index`
Let's consider following scenario:
```sh
~> touch file.txt
~> git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	file.txt

nothing added to commit but untracked files present (use "git add" to track)
~> git add file.txt
~> git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   file.txt

~> echo "new content" > file.txt
~> git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file.txt
```
What does it mean for change to be *staged*?
```sh
~> hexdump -C .git/index
00000000  44 49 52 43 00 00 00 02  00 00 00 01 60 66 e1 3d  |DIRC........`f.=|
00000010  15 7d 40 fe 60 66 e1 3d  15 7d 40 fe 00 00 00 1a  |.}@.`f.=.}@.....|
00000020  00 1f 40 63 00 00 81 a4  00 00 03 e8 00 00 03 e8  |..@c............|
00000030  00 00 00 00 e6 9d e2 9b  b2 d1 d6 43 4b 8b 29 ae  |...........CK.).|
00000040  77 5a d8 c2 e4 8c 53 91  00 08 66 69 6c 65 2e 74  |wZ....S...file.t|
00000050  78 74 00 00 4a a4 ed 90  d2 ca 32 07 52 b6 39 d3  |xt..J.....2.R.9.|
00000060  e4 31 4b bb fc 72 8e 2d                           |.1K..r.-|
00000068
```
By checking [https://git-scm.com/docs/index-format](https://git-scm.com/docs/index-format) I ca see that the index starts with:

* A 12-byte header consisting of
	* 4-byte signature:
		* The signature is { 'D', 'I', 'R', 'C' } (stands for "dircache")
	* 4-byte version number:
		* The current supported versions are 2, 3 and 4.
	* 32-bit number of index entries.

Thus the header part of the dump is:
```sh
44 49 52 43 00 00 00 02 00 00 00 01
-----------|-----------|-----------
   DIRC    |    v2     |  1 entry
```

The header is followed by entries themselves, each entry starts with ten 4-byte `stat` numbers:
```sh
ctime seconds, the last time a file's metadata changed
ctime nanosecond fractions
mtime seconds, the last time a file's data changed
mtime nanosecond fractions
dev
ino
mode
uid
gid
file size
```

* *ctame* - time when content or metadata was changed
* *mtame* - time when content was changed
* *dev* - ID of hardware storage
* *non* - number of inode

To list all the files in the index:
```sh
~> git ls-files --stage
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0	file.txt
```