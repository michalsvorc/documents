# rsync

```bash
rsync -avAX /source/ /target/
```

Options:
    --archive,-a            preserves most aspects of source directory
    --verbose,-v            increase verbosity
    --acls, -A              preserve ACLs (implies --perms)
    --xattrs, -X            preserve extended attributes
    --checksum, -c          skip based on checksum, not mod-time & size
    --delete                delete extraneous files from dest dirs
    --info=progress2        display progress info
    --exclude=PATTERN       exclude files matching PATTERN, e.g. --exclude={"lost+found",".cache"}
    --dry-run, -n           perform a trial run with no changes made

Without trailing slash (`directory`): Copies the directory itself inside the destination.
With trailing slash (`directory/`): Copies all contents within the directory.

The `-A` and `-X` flags help to ensure that rsync correctly preserves ACLs (access control lists) and extended attributes, keeping all detailed permissions and extra metadata intact during backups.

## Backup files for critical data

--backup,-b             creates backups of overwritten/deleted files (renaming the old ones with a suffix)
--backup-dir=DIR        places these backup copies into a dedicated directory (instead of in-place in the destination folder)


