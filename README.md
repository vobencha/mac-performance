# mac-performance

I've used the Geekbench suite to assess CPU and memory performance. It does not
measure disk I/O so I'll find a different test for that. Ideally I'd run this
test 100 times and take the average but, in the interest of time, I've
reported a single result so bear that in mind. (That said, when run manually
several times the output didn't vary much.)

Machines tested:  
|merida2: | MacStadium machine running El Capitan
|macHV2: |New Mac Pro host (hypervisor) running Mojave
|celaya2: |New Mac Pro guest (VM on macHV2) running El Capitan

- Results

Full results are available [here](https://vobencha.github.io/mac-performance/).

High-level result summary:

|               | **merida2** | **macHV2** | **celaya2**
| ------------- | ----------- | ---------- | ----------- 
| **Topology**  | 1 processor, 12 cores, 24 threads | 1 processor, 12 cores, 24 threads | 1 processor, 23 cores
| **Memory** | 65536 MB 1866 MHz DDR3 | 65536 MB 1866 MHz DDR3 | 57344 MB 667 MHz DRAM
| | | |
| **Single-core** | | |
| Overall score | 3570 | 3582 | 3422
| Memory score | 3512 | 3473 | 3384
| Memory copy | 10.5 GB/sec | 10.4 GB/sec | 9.89 GB/sec
| Memory latency | 74.2 ns | 74.5 ns | 77.4 ns
| Memory bandwidth | 10.5 GB/sec | 10.3 GB/sec | 10.4 GB/sec
| | | |
| **Multi-core** | | |
| Overall score | 28570 | 31194 | 25799 
| Memory score | 5235 | 5232 | 4814 
| Memory copy | 19.2 GB/sec | 18.9 GB/sec | 17.1 GB/sec
| Memory latency | 75.6 ns | 76.6 ns | 83.1 ns
| Memory bandwidth | 19.4 GB/sec | 19.8 GB/sec | 18.5 GB/sec

- Cost of virtualization

The VM was allocated 23 of the 24 cores and 57344 of 65536 MB of memory.

It doesn't look like we take much of a hit in virtualizing. The single-core
performance serves as a baseline but multi-core is closer what we'll see in
practice. As expected, the VM is slower to access memory (latency) and has a
worse copy to bandwidth ratio. However, it isn't bad and is better than what I
was expecting for a VM.

Multi-core memory copy-to-bandwidth ratio:  
merida2: 98.9%  
macHV2: 95.5%  
celaya2: 92.4%  

Multi-core memory latency:
In this snapshot, celaya2 is ~ 8% slower than macHV2 and 10% slower than merida2.

- Machines in MacStadium are not virtualized

Looking at the Topology, Memory and BIOS output, it appears that merida1 and
merida2 are dedicated Mac Pro machines. I didn't think this was the case. 

The only Mac Pro you can buy these days is from 2013. I believe this is old
enough hardware to be running El Capitain directly and must be what MacStadium
is doing.

- Should we run El Capitain directly on our Mac Pro instead of using Parallels?

No, I don't think so. Even if our current Mac Pro is old enough hardware to run
El Capitan, this probably won't be the case for the next Mac machine we buy. It
would be good to manage the machines the same way.

The virtualization approach also allows us to create images that can be used to
configure future machines.

