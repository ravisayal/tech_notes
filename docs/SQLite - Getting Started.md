
Important links 
https://sqlite.org/cli.html
https://www.sqlitetutorial.net/ 


Importing data into SQLite tables
Use -cmd to import records from file, it accepts multiple -cmd commands and executes them in order, before the final arg.
https://unix.stackexchange.com/questions/397806/how-to-pass-multiple-commands-to-sqlite3-in-a-one-liner-shell-command

`sqlite3 tolls.sql3 -cmd ".mode csv" ".import tolls.csv tolls"`



SQLlite run multiple commandds from a file. 
sample content of sql file - save this is `cmd.sql`
```
.width
.mode markdown
.schema summary
.schema dtls

select count(1), count (distinct "﻿User HUID") from summary;
select count(1), count (distinct "﻿User HUID") from dtls;

.exit
```

to execute this file

`sqlite3 hart.sql3 -cmd ".read cmd.sql"`

