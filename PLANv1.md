Things we need to sort out before we start testing
==================================================

#### Benchmarks
  + Homegrown benchmarks (fun, but maybe not very intersting to the world at
    large)
  + Coremark
  + Linux Kernel Compile
  + Web Server (too IO bound?)

#### Hardware configurations
  + [1..8] cores (i.e. the difference between more cores and more hyperthreads)
  + If we can't do the above, just with and without hyperthreading (but this
    seems weak to me)
  + Increase the frequency of short SMIs (granularity?)
  + Increase the frequency of long SMIs (granularity?)

#### Hypothesis
  + SMI's should have a similar effect on non-hyperthreaded cpus as it does hyperthreaded cpus.  In other words, 
    the expected performance change when changing from non-hyper threaded cpus to hyperthreaded cpus should 
    not change due to the presence of SMI.
  + Theoretical Evidence 
    * One might argue that since hyperthreading allows for multiple threads to simultaneously execute on a core, it could result in more CPU state to save/restore before/after an SMI. However, a source suggests that when an SMI occurs, "...almost every single CPU register is saved in a “memory saved state map” that is itself stored into a memory zone called SMRAM" (https://cansecwest.com/csw09/csw09-duflot.pdf)
    * TODO: investigate cache coherence impact. Wikipedia says that any write-back caches must be flushed on an SMI. 

#### Hyperthreading materials
  + Characterizing the Performance of Data Management Systems on Hyper-Threaded Architectures 
    * http://ieeexplore.ieee.org.proxy.lib.pdx.edu/stamp/stamp.jsp?tp=&arnumber=4032421
    * Reports the effects of HT on DB performance (up to 1.16x improvement) 
    * Majority of their performance benefit from reduction in L2 cache misses 
    * Older processor, but here's their cache behavior model: 

> In SMT architectures the cache
> hierarchy is shared among all the thread contexts. This
> is also the case in the Intel Pentium 4 hyperthreaded
> architecture, where both threads share the L1
> instruction trace cache, the L1 data cache, and the
> unified L2 cache. This sharing can be either beneficial,
> if for example one thread prefetches data for the other,
> or detrimental, if one thread conflicts with the other
> causing a large number of cache misses

  + The Impact of Hyper-Threading on Processor Resource Utilization in Production Applications
    * http://www.nas.nasa.gov/assets/pdf/papers/saini_s_impact_hyper_threading_2011.pdf
    * Good summary of what we'd expect from HT regarding memory contention (and model for functional unit usage as well): 

> If sufficient resources (cache and memory bandwidth) are available, 
> sharing them across multiple threads in HT mode will result in better 
> performance than with ST. However, we expect that if such sharing increases 
> contention between the threads to the extent that data needs to be accessed 
> from the next level of cache for each of the threads, there will, in general, 
> be no performance benefit of running in HT

> The main benefit of HT comes from the ability of
> execution units in the core, such as the floating-point units
> (FPU), to handle instructions from more than one thread
> simultaneously. The FPU is a shared resource that is
> unaware of the multiple threads. From its perspective, it is merely 
> handling a stream of instructions organized in a pipeline of the six 
> execution units — during each cycle, it can
> start executing the micro-operation in the next stage. Note
> that this will often lead to gaps (as shown earlier in Figure 1)
> where there is no micro-operation to execute. This could be,
> for example, due to a wait for a load instruction to complete.
> With HT, such gaps in the FPU’s pipeline can be filled with 
> micro-operations from a second thread — thus making for
> better utilization of the FPU.


  + Improving Database Performance on Simultaneous Multithreading Processors
    * http://delivery.acm.org.proxy.lib.pdx.edu/10.1145/1090000/1083602/p49-zhou.pdf?ip=131.252.96.28&id=1083602&acc=ACTIVE%20SERVICE&key=B63ACEF81C6334F5.CA8B0988038A4DF4.4D4702B0C3E38B35.4D4702B0C3E38B35&CFID=513444346&CFTOKEN=74238333&__acm__=1432247660_e729e68f72bd9d9cb0c1b84f604679de
    * Interesting way to improve DB performance with HT: 

> We also propose a new, general thread-based
> preloading technique for SMT processors. We utilize
> one thread, the helper thread to perform aggressive
> data preloading. The main computation is executed in
> the other thread, which we call the main thread.
> The helper thread works ahead of the main thread, triggering 
> memory accesses for data elements that will soon
> be needed in the main thread. For reasons discussed
> in Section 2.3, the helper thread performs an explicit
> load instruction, and not a prefetch instruction.
> If the preloading happens in an optimal manner,
> the main thread will almost always find the requested
> data in the cache and experience a higher cache hit
> rate. The data preloading performed by the helper
> thread can be overlapped with the CPU computation
> done by the main thread. The helper thread suffers
> most of the memory latency, while the main thread is
> free to work on the real computation.



#### Tasks
  + Research previous work
    * http://web.cecs.pdx.edu/~karavan/research/SMM_IISWC_preprint.pdf
    * http://cs.gmu.edu/~astavrou/research/Hypercheck_raid10.pdf
    * http://cs.gmu.edu/~tr-admin/papers/GMU-CS-TR-2011-8.pdf
  + Identify why this subject is important to others  
  + Identify testing metrics 
    * We should not only test performance of some task, but also throughput of the system within some timeframe 
  + Strictly define scope of tests / project 
  + Test some chosen benchmarks / experiments with mixes of hyperthreading on/off and SMI on/off with various durations/frequencies 
    * (Task's finish time with hyperthreading - Task's finish time **without** hyperthreading) == Expected effect of hyperthreading (EEH)
    * Task's finish time with SMI and hyperthreading - Task's finish time **without** SMI and with hyperthreading == Effect of SMI (ES_h)
    * Task's finish time with SMI and **without** hyperthreading - Task's finish time **without** SMI and **without** hyperthreading == Effect of SMI (ES_s)
    * At this point we have measured the effect on finish time of SMI with and without hyperthreading. If our hypothesis is correct, the effects should not be too different. We can further validate asking: does (Task's finish time with SMI and hyperthreading - EEH) approximate (Task's finish time with SMI and **without** hyperthreading). That is, after accounting for the expected effect of hyperthreading, is the effect of SMI between the two simulations similar? Put another way, does the combination of SMI and hyperthreading compound the effect of SMI? 
  + After testing, investigate reasons for differences (were we correct in our hypothesis?) 
  + Identify areas for future work 
  
  

