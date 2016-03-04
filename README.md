github clone of (original, as at 2016-03-03) fixsrcip - http://0pointer.de/lennart/projects/fixsrcip/

From fixsrcip-0.1/README:
-------------------------

fixsrcip is a tool for binding outgoing TCP and UDP client sockets
(IPv4) to specific source IP addresses on multi-homed hosts. It
requires a current Linux system. It uses LD_PRELOAD for preloading a
small shared object to executables. The shared object overwrites the
connnect() (for TCP) and sendto()/sendmsg() (for UDP) functions.

If you don't understand the short description above, fixsrcip is
probably not what you're looking for.

For compiling and installing just run "make" and copy the newly
created shared object "fixsrcip.so" and the shell script "fixsrcip" to
some suitable places. (i.e. /usr/local/lib resp. /usr/local/bin) Edit
fixsrcip and adjust the path to the shared object in the variable
FIXSRCIP. (For building fixsrcip you have to install gcc, make and the
glibc header files.)

After that you may use fixsrcip like this:

      fixsrcip 47.11.8.15 telnet heise.de 80

(This will start telnet for a connction to heise.de on port 80 using
the source address 47.11.8.15.)

You may use fixsrcp.so without using the supplied shell script. The
shared object relies on $LD_PRELOAD set to the path of the shared
object and $FIXSRCIP set to the source IP address to use. This is
especially useful for assigning different IP adresses for different
users: just put 

       export LD_PRELOAD=/path/to/fixsrcip.so FIXSRCIP=47.11.8.15 

into the respective ~/.bashrc file. Whenever the user logs in he'll
make his connections from 47.11.8.15.

No, there's no protection that the user disables fixsrcip at his own
will.

No, fixsrcip doesn't work on SETUID programs. This is a limitation of
LD_PRELOAD.

No, fixsrcip doesn't work for ICMP. This is a limitation of BSD
sockets. Yes, that means that ping doesn't care about $FIXSRCIP.

-- 
November 2004, Lennart Poettering, mzsvkfepvc (at) 0pointer (dot) de

$Id: README 43 2004-11-22 20:57:29Z lennart $
