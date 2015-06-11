#Tmix Internet Traffic Generator for the ns-3 Network Simulator#

Modules for including the Tmix Internet Traffic Generator in the ns-3 network simulator.  This includes both Tmix and Delaybox.

Code is available in the [Releases](https://github.com/weiglemc/tmix-ns3/releases) section for ns-3.14.1 and earlier.  Code is available at http://www.nsnam.org for later versions.  We have versions available for
 * ns-3.21 - see [Tmix in ns-3.21 Instructions](https://github.com/weiglemc/tmix-ns3/wiki/Tmix-in-ns-3.21)
 * ns-3.13, ns-3.14.1 - see [Tmix in ns-3.13 and ns-3.14.1 Instructions](https://github.com/weiglemc/tmix-ns3/wiki/Tmix-in-ns-3.13-and-ns-3.14.1)  - *Many thanks to Mats Rosbach from University of Oslo for providing compatibility with ns-3.13 and ns-3.14.1*
 * ns-3.10 - see [Tmix in ns-3.10 instructions](https://github.com/weiglemc/tmix-ns3/wiki/Tmix-in-ns-3.10)

Note: The source code is delivered 'as-is', and we cannot offer any support. Code last updated in 2012.

For more information on Tmix, see
 * http://www.cs.odu.edu/~mweigle/papers/ccr06.pdf
 * http://www.cs.odu.edu/~mweigle/papers/adurthi-tmix-TR06.pdf
 * [Tmix at ODU](http://www.cs.odu.edu/~inets/Public/Tmix)

For more information on ns-3, see http://www.nsnam.org/

Citation Request: If you use this in your work, please cite 

> Weigle, M. C., Adurthi, P., Hernández-Campos, F., Jeffay, K., and Smith, F. D. Tmix: a tool for generating 
>  realistic TCP application workloads in ns-2. *SIGCOMM Compututing Commununications Review* 36, 3 (Jul. 2006), 65-76. 
 * http://doi.acm.org/10.1145/1140086.1140094
 * http://www.cs.odu.edu/~mweigle/papers/ccr06.pdf

Outstanding Issues

There are several places in the code marked `TODO` or `FIXME`:
  * `src/delaybox/model/delaybox.cc`
  * `src/delaybox/model/delaybox.h`
  * `src/delaybox/model/tcp-flow-classifier.cc`
  * `src/delaybox/model/tcp-flow-classifier.h`
  * `src/tmix/helper/tmix-ns2-style-trace-helper.cc`
  * `src/tmix/helper/tmix-helper.h`
  * `src/tmix/model/tmix-topology.cc`
  * `src/tmix/model/tmix.cc`
