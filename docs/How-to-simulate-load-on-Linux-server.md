# How to simulate high CPU load on a Linux server?

[Reference Link](https://superuser.com/questions/443406/how-can-i-produce-high-cpu-load-on-a-linux-server)

```bash
# Usage: lc [number_of_cpus_to_load [number_of_seconds] ]
lc() {
  (
    pids=""
    cpus=${1:-1}
    seconds=${2:-60}
    echo loading $cpus CPUs for $seconds seconds
    trap 'for p in $pids; do kill $p; done' 0
    for ((i=0;i<cpus;i++)); do while : ; do : ; done & pids="$pids $!"; done
    sleep $seconds
  )
}
```

> Usage Example

```bash
# simulate the load on 2 CPU for 60 seconds
$ lc 2 60
```
