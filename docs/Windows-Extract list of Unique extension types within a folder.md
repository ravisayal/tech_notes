# Windows-Extract list of Unique extension types within a folder/subfolder

[Reference Link](https://superuser.com/questions/397943/how-to-extract-a-complete-list-of-extension-types-within-a-directory)

```bat
Get-Childitem C:\folder -Recurse | WHERE { -NOT $_.PSIsContainer } | Group Extension -NoElement | Sort Count -Desc > FileExtensions.txt
```

>  remove *C:\folder* and it will execute in the current directory.

At the end it will produce a FileExtensions.txt containing something like the following:

```
Count Name                     
----- ----                     
 1509 .sql                     
 1221 .txt                     
  608 .java                    
  372 .class                   
  170 .xml                     
  141 .png                     
  125                          
   98 .gif                     
   90 .fmb                     
   90 .fmx                     
```
