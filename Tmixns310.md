### Installation ###
Download the ns-allinone-3.10 tarball from http://www.nsnam.org/ns-3-10 and follow the [instructions for compiling](http://www.nsnam.org/docs/release/3.10/tutorial/singlehtml/index.html#building-ns-3) and [testing](http://www.nsnam.org/docs/release/3.10/tutorial/singlehtml/index.html#testing-ns-3).  In a nutshell,
```
./build.py
cd ns-3.10
./waf -d debug configure
./waf
```

Test the installation:
```
./test.py -c core
```

Add the tmix and delaybox files:
  * Unpack [tmix-ns3-10.tgz](http://code.google.com/p/tmix-ns3/downloads/detail?name=tmix-ns3-10.tgz) into `src/applications/`
  * Unpack [delaybox-ns3-10.tgz](http://code.google.com/p/tmix-ns3/downloads/detail?name=delaybox-ns3-10.tgz) into `src/devices/`
  * Copy [test-tmix-ns3-10.cc](http://code.google.com/p/tmix-ns3/downloads/detail?name=test-tmix-ns3-10.cc) into `scratch`
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
cd ns-3.10
./waf -d debug configure
./waf
```

### Running Tmix ###
`test-tmix-ns3-10.cc` sets up the following topology:

<img src='http://www.cs.odu.edu/~inets/files/tmix-fig.jpg' width='400'>

The src direction uses <code>outbound.ns</code>, and the dst direction uses <code>inbound.ns</code>

To run the test:<br>
<pre><code>cd ns-3.10/build/debug<br>
./scratch/test-tmix-ns3-10 ../../scratch/outbound.ns ../../scratch/inbound.ns | gzip &gt; ../../scratch/tmix-ns3-10.trace.gz<br>
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

and end with:<br>
<pre><code>- 9.999890 2 4 ack 1500 ------- 0 2.1632 3.49448 759987 116492 1 0x10 40 0 <br>
- 9.999902 2 4 ack 1500 ------- 0 2.1632 3.49448 761447 116493 1 0x10 40 0 <br>
r 9.999914 3 5 ack 40 ------- 0 3.49470 2.2480 711 152734 340 0x10 40 0 <br>
r 9.999914 3 5 ack 40 ------- 0 3.49470 2.2480 711 152736 341 0x11 40 0 <br>
r 9.999915 3 5 ack 40 ------- 0 3.49470 2.2480 712 152737 341 0x10 40 0 <br>
r 9.999941 2 4 ack 1500 ------- 0 2.1632 3.49448 752687 116487 1 0x10 40 0 <br>
r 9.999953 2 4 ack 1500 ------- 0 2.1632 3.49448 754147 116488 1 0x10 40 0 <br>
r 9.999965 2 4 ack 1500 ------- 0 2.1632 3.49448 755607 116489 1 0x10 40 0 <br>
r 9.999978 2 4 ack 1500 ------- 0 2.1632 3.49448 757067 116490 1 0x10 40 0 <br>
r 9.999990 2 4 ack 1500 ------- 0 2.1632 3.49448 758527 116491 1 0x10 40 0 <br>
</code></pre>

This is an ns-2 style output trace with the following fields:<br>
<ol><li>type - + (enqueue), - (dequeue), r (receive), d (drop) (Note: + and - always happen in pairs and at the same time; the Delaybox delay appears between the - and r times. )<br>
</li><li>time in seconds when the event occurred<br>
</li><li>link-layer source node ID<br>
</li><li>link-layer destination node ID<br>
</li><li>name - unused, always <code>ack</code>
</li><li>total packet size in bytes<br>
</li><li>IP flags - unused, always <code>-------</code>
</li><li>flow id - unused, always <code>0</code> (TODO: implement)<br>
</li><li>source - format is nodeID.portNumber  (Warning: unlike in Tmix for ns-2, the TCP source port no longer has any meaningful relationship to anything.)<br>
</li><li>destination - format is nodeID.portNumber<br>
</li><li>sequence number<br>
</li><li>semi-unique id - (Warning: in ns-2, fragments of the same packet would get separate IDs, but in ns-3 they no longer do.)<br>
</li><li>ACK number<br>
</li><li>TCP flags - (0x01 - FIN, 0x02 - SYN, 0x08 - PUSH, 0x10 - ACK)<br>
</li><li>TCP/IP header size - unused, always <code>40</code>
</li><li>SACK length