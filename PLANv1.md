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
  
  

