# Bak

A nice and simple file backer-upper.

## Premise

I've gotten very used to writing

```bash
mv my-file{,.bak}
```

When I want to make a quick backup of a given file however the syntax is a little verbose for my liking, especially when I'm busy and trying to input quite frantically.

Because of this, and the pitfalls of mucking up the syntax by a single character, I wanted a tiny little CLI tool to do it for me; this is that

## Usage

Fairly easy to use. No options are required for general use, for example

Say you have this file

```sh
$ test -f my-file.txt && echo "Hello!"
Hello!
```

And you want to make a backup of the file, you could use

```sh
$ bak my-file.txt
my-file.txt.bak
```

Now, both `my-file.txt` and `my-file.txt.bak` exist and you can happily continue editing `my-file.txt`.

If you wanted to make a backup of this file but not preserve the existing copy, use `-d`

```sh
$ bak -d my-file.txt
my-file.txt.bak
```

Now, you have just `my-file.bak`, what about restoring it? Well, `-r` is for just that

```sh
$ test -f my-file.txt && echo "Hello!"

$ bak -r my-file.txt.bak
my-file.txt
$ test -f my-file.txt && echo "Hello!"
Hello!
```

### Help

This is the help output for further clarification.

```
Bak, a simple file backer-upper; usage:

    bak [options] [--] [<args...>]

Options:

    -h|--help
          Show this help info
    -v|--verbose
          Show additional logging and verbose messages
    -d|--delete
          Move files to a backup, instead of copying them
    -r|--restore
          Boolean option specifying that the file args are already backups and 
          should be restored (as opposed to backing up further)
    -b|--backup-backup
          Make a backup of an existing backup file if it exists.  If -r is 
          given, move the current file to a backup and move the backup to the 
          current file
    -s|--suffix <SUFFIX>
          The default suffix is $SUFFIX, use this to 
          specify a custom suffix
```
