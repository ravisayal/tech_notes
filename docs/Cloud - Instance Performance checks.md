## EXPLORING THE GOOGLE CLOUD F1-MICRO INSTANCE

> Source
https://www.opsdash.com/blog/google-cloud-f1-micro.html#:~:text=The%20f1%2Dmicro%20is%20a,%E2%80%9D%20of%20time%20%E2%80%9Cautomatically%E2%80%9D.


Check out what Google Cloud Platform's f1-micro Instance can do.

The Google Cloud Platform folks [recently announced](https://cloudplatform.googleblog.com/2017/03/Google-Cloud-Platform-your-Next-home-in-the-cloud.html) an [“always free” tier](https://cloud.google.com/free/), which includes an “f1-micro” instance and a 30 GB magnetic disk.

So what is an f1-micro instance capable of? Let’s find out.

### CPU

The f1-micro is a [shared-core](https://cloud.google.com/compute/docs/machine-types#sharedcore) machine type having 0.2 virtual CPUs. A virtual CPU is a single hardware hyperthread on an Intel Xeon E5.

According to the [documentation](https://cloud.google.com/compute/docs/machine-types#sharedcore), the f1-micro has a bursting capability that allows it to use additional physical CPU for “short periods” of time “automatically”.

So how exactly does “0.2 CPU” look like? Let’s kick the tyres a bit:

```
$ stress -c 3 --timeout 10m
stress: info: [6296] dispatching hogs: 3 cpu, 0 io, 0 vm, 0 hdd
stress: info: [6296] successful run completed in 600s
```

And here is what we saw:

[![f1-micro CPU Usage Throttling](https://www.opsdash.com/blog/images/f1-micro-cpu-usage.png)](https://www.opsdash.com/blog/images/f1-micro-cpu-usage.png)

f1-micro CPU Usage Throttling



The load average stays at 3, corresponding to the number of tasks run by `stress`. The user CPU stayed at 0.22 for the duration of execution. The guest VM always sees that CPU steal as 0, but as you can see from the graph, the total CPU ticks available to the VM’s CPU gets throttled down to 0.2 once it actually starts using it.

In summary – yes, you really get only 0.2 of a CPU.

### RAM

0.6 GB RAM comes to a total available memory of 588 MiB reported by an Ubuntu 16.04 kernel.

### NETWORK

By default, each project in the Google Cloud Platform (GCP) comes with a private network with built-in DHCP and DNS servers. Each VM gets a private IP, and an optional public IPv4 address from a GCP-wide pool of IPs.

The network egress throughput is [capped](https://cloud.google.com/compute/docs/networks-and-firewalls#egress_throughput_caps) to 2 Gbps per core. As an exception, for shared-core machines the throughput is capped at 1 Gbps. 1 Gbps is around [119 MiB/s](https://www.google.com/?gfe_rd=cr&ei=FL_QWJvrKqjv8wfms5OwCA&gws_rd=cr&fg=1#q=1+gbits/s+to+mib/s&*).

Let’s test it out:

```
$ qperf -t 1m 10.138.0.3 udp_bw
udp_bw:
    send_bw  =  120 MB/sec
    recv_bw  =  119 MB/sec
```

Close enough. You can read more about qperf [here](https://www.opsdash.com/blog/network-performance-linux.html).

As with AWS, the disk I/O throughput is carved out of the total network bandwidth. It is not documented how the bandwidth is split or traffic is shaped between the two, but of course, it’s best practice not to have both contending.

### DISK

GCP offers magnetic and SSD block storage, and NVMe-based instance storage. There is no IOPS provisioning for block storage, rather the throughput is computed using guidelines given in [this documentation](https://cloud.google.com/compute/docs/disks/performance#type_comparison).

According to that, the 30 GB magnetic disk storage in the free tier should have write throughput of:

- write IOPS = 1.5 IOPS/GB * 30 GB = 45 IOPS
- write throughput = 0.12 MB/s/GB * 30 GB = 3.6 MB/s

There is also another limit, imposed by the network throughput cap, and documented [here](https://cloud.google.com/compute/docs/disks/performance#egress_performance_cap). Basically, if a process tries to write K bytes of data to the disk, the device driver writes out 3.3 * K bytes of data to the network. Because of the network cap, this introduces a limit on the write throughput:

- write throughput = 1 Gbps / 3.3 = ~36 MB/s

Now let’s try a few writes and reads:

```
$ dd if=/dev/zero of=testfil bs=4K count=2621440
2621440+0 records in
2621440+0 records out
10737418240 bytes (11 GB, 10 GiB) copied, 285.65 s, 37.6 MB/s

$ dd if=testfil of=testfil.2 bs=4K
2621440+0 records in
2621440+0 records out
10737418240 bytes (11 GB, 10 GiB) copied, 322.312 s, 33.3 MB/s
```

Hmm, we actually expected tthe 3.6 MB/s limit imposed by the disk size to be hit, rather than the 36 MB/s limit imposed by the network egress cap. It is not clear why this is so.

Let’s have a look at the graphs:

[![Disk IOPS](https://www.opsdash.com/blog/images/f1-micro-disk-iops.png)](https://www.opsdash.com/blog/images/f1-micro-disk-iops.png)

Disk IOPS



We hit around 211 IOPS for the write. And here is the disk throughput graph showing reads and writes at ~33 MB/s:

[![Disk Throughput](https://www.opsdash.com/blog/images/f1-micro-disk-throughput.png)](https://www.opsdash.com/blog/images/f1-micro-disk-throughput.png)

Disk Throughput



### THE VM “FAILOVER”

Google Cloud VMs have a built-in “failover” feature, which they call [live migration](https://cloud.google.com/compute/docs/instances/live-migration) Essentially, a running VM can be migrated from one physical host to another with a downtime in the order of [100s of milliseconds](https://cloudplatform.googleblog.com/2016/04/lessons-learned-from-a-year-of-using-live-migration-in-production-on-Google-Cloud.html). The migration is automatic, and typically undetectable, but for logs like this in the GCP console:

[![Live Migration](https://www.opsdash.com/blog/images/google-cloud-live-migration.png)](https://www.opsdash.com/blog/images/google-cloud-live-migration.png)

Live Migration



Much better than those your-instances-will-be-terminated emails, for sure.

##### NEW HERE?

OpsDash is a server monitoring, service monitoring, and database monitoring solution for monitoring MySQL, PostgreSQL, MongoDB, memcache, Redis, Apache, Nginx, Elasticsearch and more. It provides intelligent, customizable dashboards and spam-free alerting via email, HipChat, Slack, PagerDuty and Webhooks. Send in your custom metrics with StatsD and Graphite interfaces built into each agent.
