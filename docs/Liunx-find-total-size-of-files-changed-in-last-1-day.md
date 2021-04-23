## Find total size of files change in past 1 day 

Change -mtime param for other time units

```
find . -type f -name "*.*" -mtime -1 -exec du -ch {} + | grep total$

```
