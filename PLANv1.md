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
