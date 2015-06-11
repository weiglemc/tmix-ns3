**Page and instructions are still under construction**

Thanks to Mats Rosbach from University of Oslo for providing compatibility with ns-3.11 and higher.

### Installation ###
Download the ns-allinone-3.14.1 tarball from http://www.nsnam.org/ns-3-14 and follow the [instructions for compiling](http://www.nsnam.org/docs/release/3.14/tutorial/singlehtml/index.html#building-ns-3) and [testing](http://www.nsnam.org/docs/release/3.14/tutorial/singlehtml/index.html#testing-ns-3).  In a nutshell,
```
./build.py --enable-examples --enable-tests
cd ns-3.14.1
./waf -d debug --enable-examples --enable-tests configure
./waf
```

Test the installation:
```
./test.py -c core
```

Add the tmix and delaybox files:
  * Unpack [tmix-ns3-14.tgz](http://code.google.com/p/tmix-ns3/downloads/detail?name=tmix-ns3-14.tgz) into `src/`.  This will create the 'tmix' and 'delaybox' directories under 'src'.
  * Copy [test-tmix.cc](http://code.google.com/p/tmix-ns3/downloads/detail?name=test-tmix.cc) into `scratch`
  * Unpack [ccr06-traces-newstyle.tgz](http://code.google.com/p/tmix-ns3/downloads/detail?name=ccr06-traces-newstyle.tgz) into `scratch` (Note: These are the same traces as the [connection vectors from our CCR 2006 paper](http://code.google.com/p/tmix-ns2/downloads/detail?name=ccr06-traces.tgz), but in a different format.)

Apply the following edit to src/wscript:
```
    'contrib/energy',
    'tools/visualizer',
+   'devices/delaybox',
+   'applications/tmix',
)
```

Add appropriate directories to `LD_LIBRARY_PATH`.  Example:
```
setenv LD_LIBRARY_PATH /home/user/src/ns-allinone-3.10/ns-3.10/build/debug/:
/home/user/src/ns-allinone-3.10/ns-3.10/scratch
```

Re-compile (w/configure):
```
cd ns-3.14.1
./waf -d debug --enable-examples --enable-tests configure
./waf
```

### Running Tmix ###
`test-tmix.cc` sets up the following topology:

<img src='http://www.cs.odu.edu/~inets/files/tmix-fig.jpg' width='400'>

The src direction uses <code>outbound.ns</code>, and the dst direction uses <code>inbound.ns</code>

To run the test:<br>
<pre><code>cd ns-3.10/build/debug<br>
./scratch/test-tmix ../../scratch/outbound.ns ../../scratch/inbound.ns | gzip &gt; tmix-ns3.trace.gz<br>
</code></pre>

The test will take a couple of minutes to run and simulates 10 seconds of network traffic.  (Note that there are 3600 seconds worth of connection vectors in the input files.)  The generated trace file should start with:<br>
<pre><code>+ 0.003412 3 5 ack 40 ------- 0 3.49153 2.1024 0 0 0 0x02 40 0 <br>
- 0.003412 3 5 ack 40 ------- 0 3.49153 2.1024 0 0 0 0x02 40 0 <br>
r 0.003512 3 5 ack 40 ------- 0 3.49153 2.1024 0 0 0 0x02 40 0 <br>
+ 0.003724 3 5 ack 40 ------- 0 3.49154 2.1025 0 1 0 0x02 40 0 <br>
- 0.003724 3 5 ack 40 ------- 0 3.49154 2.1025 0 1 0 0x02 40 0 <br>
r 0.003824 3 5 ack 40 ------- 0 3.49154 2.1025 0 1 0 0x02 40 0 <br>
+ 0.003992 3 5 ack 40 ------- 0 3.49155 2.1026 0 2 0 0x02 40 0 <br>
- 0.003992 3 5 ack 40 ------- 0 3.49155 2.1026 0 2 0 0x02 40 0 <br>
r 0.004092 3 5 ack 40 ------- 0 3.49155 2.1026 0 2 0 0x02 40 0 <br>
+ 0.005564 3 5 ack 40 ------- 0 3.49156 2.1027 0 3 0 0x02 40 0 <br>
</code></pre>

This is an ns-2 style output trace with the following fields:<br>
<ol><li>type - + (enqueue), - (dequeue), r (receive), d (drop)<br>
</li><li>time<br>
</li><li>link-layer src<br>
</li><li>link-layer dst<br>
</li><li>name - {tcp, ack}, not meaningful<br>
</li><li>size<br>
</li><li>IP flags - usually -------<br>
</li><li>flow id<br>
</li><li>src node.port<br>
</li><li>dst node.port<br>
</li><li>sequence number<br>
</li><li>unique id<br>
</li><li>ACK number<br>
</li><li>TCP flags - (0x01 - FIN, 0x02 - SYN, 0x08 - PUSH, 0x10 - ACK)<br>
</li><li>TCP/IP header size<br>
</li><li>SACK length