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

# How to simulate memory load on a Linux server?

[Reference link](https://unix.stackexchange.com/questions/99334/how-to-fill-90-of-the-free-memory)

```bash
cat <( </dev/zero head -c 500m) <(sleep 15) | tail
```

This works because tail needs to keep the current line in memory, in case it turns out to be the last line. The line, read from /dev/zero which outputs only null bytes and no newlines, will be infinitely long, but is limited by head to BYTES bytes, thus tail will use only that much memory. For a more precise amount, you will need to check how much RAM head and tail itself use on your system and subtract that.

To just quickly run out of RAM completely, you can remove the limiting head part:
```
tail /dev/zero
```

If you want to also add a duration, this can be done quite easily in bash (will not work in sh):
```
cat <( </dev/zero head -c 500m) <(sleep SECONDS) | tail`
```
