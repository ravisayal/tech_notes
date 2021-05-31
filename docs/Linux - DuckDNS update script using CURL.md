# DuckDNS update script using CURL 

```shell
#!/bin/bash

date | tee -a /tmp/user_init.log
echo url="https://www.duckdns.org/update?domains=mc-ftp&token=73d6581b-fe2f-4d9c-b5ac-011994097450&ip=" | curl -K -|tee -a /tmp/user_init.log
```
