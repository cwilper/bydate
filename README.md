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
  the file is examined first. If it's a JPEG and has a date in the `EXIF`
  metadata, that will be used. Otherwise, the filesystem date
  (`mtime`) will be used.
* After copying or moving it, the filesystem date will be set
  on the destination file according to the authoritative date as
  determined above.
* Files will never be overwritten; if the destination file already
  exists, the source file will be left in place and the destination
  won't be touched.

## Installation

You need ruby. Sorry about that. If you don't know what ruby is, ask one of
your nerd friends to help. You can find out which of your friends are nerds
by gathering them into a room and casually asking, "Have you seen the latest
XKCD?". Whoever turns their head fastest is going to be your best bet.

Anyway, I recommend installing ruby via [RVM](https://rvm.io/rvm/install)
if you don't have it yet.

Once ruby is installed, you'll need to grab a couple prerequisites:

```
gem install ftools
gem install exifr
```

Then you can put this script somewhere easy to execute, like
`/usr/local/bin/bydate`, and make sure it's executable and in your
`PATH`.
