# Delete Named Folders and Contents

I had this use-case where I wanted to delete all build outputs of every package in a monorepo. Each package, once built,
would create a `dist` folder with the build inside. I needed to build locally just for debugging, but sometimes those folders would create conflicts.

This bash script is tailored for this use-case but can be easily customized.

```shell
find . -type d -path "*/node_modules/*" -prune -o -type d -name dist -delete
```

1. `find .`: This command searches for files and directories recursively starting from the current directory (.).
2. `-type d`: This option specifies that the search should only consider directories.
3. `-path "*/node_modules/*" -prune`: This part of the command tells find to ignore any directories named "node_modules" and all of their contents. The -prune option prevents find from descending into these directories.
4. `-o`: This is a logical OR operator. It allows combining multiple conditions in the find command.
5. `-type d -name dist -delete`: This part of the command searches for directories (-type d) with the name "dist" (-name dist) and deletes them (-delete). So, any directory named "dist" found outside of "node_modules" directories will be deleted.