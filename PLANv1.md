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

#### Hypopothesis
  + We need one
