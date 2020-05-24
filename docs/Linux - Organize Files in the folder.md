# Linux - Organize  files by date into folders

This command will Organize files by date into folders based on files creation date.
A Sub folder will be created for a date if a file is present for that date. All the Files created on that date will be moved to this sub folder.
This is especially useful for organizing the Log Files.

```bash
for f in *.log; do mkdir -p "$(date -r "$f" +"%Y%m%d")" ; mv -n "$f" "$(date -r "$f" +"%Y%m%d")"/"$f"; done

```

In the below command the Log file is also getting renamed to the Date_Time

```bash
for f in *.log; do mkdir -p "$(date -r "$f" +"%Y%m%d")" ; mv -n "$f" "$(date -r "$f" +"%Y%m%d")"/"$(date -r "$f" +"%Y%m%d_%H%M%S").log"; done

for f in *.flac; do mkdir -p "$(date -r "$f" +"%Y%m%d")" ; mv -n "$f" "$(date -r "$f" +"%Y%m%d")"/"$(date -r "$f" +"%Y%m%d_%H%M%S").flac"; done



```
