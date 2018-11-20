# mac-performance

Performance testing Mac Pros

I've used the Geekbench suite to assess CPU and memory performance. It does not test disk I/O so I'll find a different test for that. Ideally I'd run this test 100 times and take the average. Instead I'm just reporting a single result so bear that in mind. (That said, when run manually several times the output didn't vary much.)

merida2: MacStadium
macHV2: New Mac Pro host (hypervisor)
celaya2: New Mac Pro guest (VM running on macHV2)

- Cost of virtualization

The VM was allocated 23 of the 24 cores and 57344 of 65536 MB of memory.

It doesn't look like we take much of a hit in virtualizing. The single-core performance serves as a baseline but multi-core is closer what we'll see in practice. As expected, the VM is slower to access memory (latency) and has a worse copy to bandwidth ratio. However, it isn't bad and is better than what I was expecting for a VM.

Multi-core memory copy/bandwidth:
merida2: 98.9%
macHV2: 95.5%
celaya2: 92.4%

Multi-core memory latency:
In this snapshot, celaya2 is ~ 8% slower than macHV2 and 10% slower than merida2.

- Machines in MacStadium are not virtualized

Looking at the Topology, Memory and BIOS output, it appears that merida1 and merida2 are dedicated Mac Pro machines. I didn't think this was the case. 

The only Mac Pro you can buy these days is from 2013. I believe this is old enough hardware to be running El Capitain directly and must be what MacStadium is doing.

- Should we run El Capitain directly on our Mac Pro instead of using Parallels?

No, I don't think so. Even if our current Mac Pro is old enough hardware to run El Capitan, this probably won't be the case for the next Mac machine we buy. It would be good to manage the machines the same way.

The virtualization approach also allows us to create images that can be used to configure future machines.

