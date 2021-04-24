## Monitor CPU, Memory and free space

```shell

l_hostname=`hostname`
l_ip_private=`hostname -I`
l_cpu_util=`vmstat|grep -vE "(proc|free)"|awk '{print $13+$14}'`
l_free_mem=`vmstat|grep -vE "(proc|free)"|awk '{print $4}'`
l_free_space=`df|grep -E "(/dev/root)"|awk '{print $4}'`
p_data="{ \
    \"hostname\"   : \"$l_hostname\"   ,\
    \"ip_private\" : \"$l_ip_private\" ,\
    \"cpu_util\"   : \"$l_cpu_util\"   ,\
    \"free_mem\"   : \"$l_free_mem\"   ,\
    \"free_space\" : \"$l_free_space\"  \
}"
echo  $p_data

# sending the performance data to webservice
#curl --location --request POST 'https://apex.oracle.com/pls/apex/slack/sysmon_logger/log' --header 'Content-Type: text/plain' --data "$p_data"

```


## Monitor System memory and save in file

Use the below script to monitor system memory 


```shell

for in in {1..10};  \
 do  \
   ps -AH v| awk -v date="$(date +"%Y-%m-%d %r")" '{print date,$1,$8,$9,$10}'  >> ./memusage1.txt ;   \
   sleep 3 ;  \
done


```

###
