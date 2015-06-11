Modules for including the Tmix Internet Traffic Generator in the ns-3 network simulator.  This includes both Tmix and Delaybox.

Code is available in the [Downloads](http://code.google.com/p/tmix-ns3/downloads/list) section for ns-3.14.1 and earlier.  Code is available on [www.nsnam.org](http://www.nsnam.org) for later versions.  We have versions available for
  * [ns-3.21](http://www.nsnam.org/contributed/tmix-db-ns-3.21.tar.gz) (tar.gz) - see [Tmix in ns-3.21 instructions](http://code.google.com/p/tmix-ns3/wiki/Tmixns321)
  * ns-3.13, ns-3.14.1 - see [Tmix in ns-3.13 and ns-3.14.1 instructions](http://code.google.com/p/tmix-ns3/wiki/Tmixns313) - <i>Many thanks to Mats Rosbach from University of Oslo for providing compatibility with ns-3.13 and ns-3.14.1</i>
  * ns-3.10 - see [Tmix in ns-3.10 instructions](http://code.google.com/p/tmix-ns3/wiki/Tmixns310)

# More Information #
For more information on Tmix, see
  * Weigle, M. C., Adurthi, P., Hernández-Campos, F., Jeffay, K., and Smith, F. D. Tmix: a tool for generating realistic TCP application workloads in ns-2. SIGCOMM Comput. Commun. Rev. 36, 3 (Jul. 2006), 65-76. http://doi.acm.org/10.1145/1140086.1140094
  * [Tmix at ODU](http://www.cs.odu.edu/~inets/Public/Tmix/)

For more information on ns-3, see http://www.nsnam.org/

# Outstanding Issues #
We cannot offer support, but here are some issues we are aware of.  If you would like to contribute fixes, please contact us and we will give you credit.

### General Issues ###
There are several places in the code marked `TODO` or `FIXME`:
  * `src/delaybox/model/delaybox.cc`
  * `src/delaybox/model/delaybox.h`
  * `src/delaybox/model/tcp-flow-classifier.cc`
  * `src/delaybox/model/tcp-flow-classifier.h`
  * `src/tmix/helper/tmix-ns2-style-trace-helper.cc`
  * `src/tmix/helper/tmix-helper.h`
  * `src/tmix/model/tmix-topology.cc`
  * `src/tmix/model/tmix.cc`