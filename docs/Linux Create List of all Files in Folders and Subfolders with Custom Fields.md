
# Linux Create List of all Files in Folders and Subfolders with Custom Fields

There are multiple ways to create a text file listing all the files. 
ls command or find command in Linux can provide the simple listing with all the filenames. 

However if there is a need to add additional columns in the output, we would need some additional scripting to get the desired output.

In this example we are creating a text file with below output format

|hostname |directory  | filename|creation date| date|
|--|--|--|--|--|
|  |  |   |  |  |


**Approach**

We will create a compound command in Linux shell and use this compound command in the -exec parameter of the find command.
Note the use of *bash -c* in the find command

```
custom_file_listing() {      echo $(hostname),$(dirname $1),$(basename $1),$(date -r $1 +"%Y%m%d_%H%M%S"),$(stat -t --format "%s" $1); }; 

export -f custom_file_listing; 

find . -name "*.flac" -exec bash -c 'custom_file_listing "$0"' {} \; > filelist.txt
```

