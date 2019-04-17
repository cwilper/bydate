# bydate

Sorts files into folders, by date, using embedded or filesystem metadata.

## Example

**You type this:**

```
bydate move src_dir dest_dir
```

**This happens:**

```
[1/3] src_dir/subdir1/IMG_0213.JPG -> dest_dir/2017/01/02/IMG_0213.JPG
[2/3] src_dir/subdir2/IMG_0215.JPG -> dest_dir/2017/01/08/IMG_0215.JPG
[3/3] src_dir/subdir3/Video112.mov -> dest_dir/2017/02/10/Video112.mov
```

## Usage

Copy or move file(s) based on date:

```
bydate copy|move SOURCE_DIR_OR_FILE DEST_DIR
```

Just show where file(s) would be copied or moved to:

```
bydate show SOURCE_DIR_OR_FILE DEST_DIR
```

## How it works

* Source file(s) will be copied or moved into the destination,
  beneath a folder based on the year, month, and day of the file.
  For example, files whose date is Jan 1st 2017 will be copied or moved
  into `dest_dir/2017/01/01/`
* To determine the authoritative date of the file, the metadata inside
  the file is examined first. If it has `EXIF` metadata, that will be used.
  Otherwise, the filesystem date (`mtime`) will be used.
* After copying or moving it, the filesystem date will be set
  on the destination file according to the authoritative date as
  determined above.
* Files will never be overwritten; if the destination file already
  exists, the source file will be left in place and the destination
  won't be touched.

## Installation

Make sure you have the dependencies:

* You must have `bash` version 4 or greater.
* `exiftool` must be in your PATH
* `jq` must be in your path

On macos, these can all be installed via brew. On other OSes, you
probably already have a new enough version of `bash`, and the
other dependencies are pretty straightforward to install manually
if your usual package repository doesn't have them.

Then you can put this script somewhere easy to execute, like
`/usr/local/bin/bydate`, and make sure it's executable and in your
`PATH`.

## Wishlist

* Improve speed by sending batches of files to exiftool, rather
  than one at a time.
* Leverage the built-in renaming/moving file support in
  exiftool: https://www.sno.phy.queensu.ca/~phil/exiftool/filename.html
* For each file, show whether EXIF or filesystem metadata was used
  to determine the date.

## History

* 2019-04-17
  - Switched main script from ruby to bash, simplifying deployment.
  - Now using `exiftool` for broader EXIF awareness (MOV, HEIC, etc.)
    This version is noticeably slower due to every file being
    examined by exiftool.

* 2017-02-12
  - Original version, required ruby
  - Only supported EXIF metadata on JPEG files
