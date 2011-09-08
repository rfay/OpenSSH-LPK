# $Id: Makefile.in,v 1.44 2010/01/15 01:38:30 dtucker Exp $

sysconfdir=/etc/ssh
piddir=/var/run
srcdir=../../openbsd-compat
top_srcdir=../..

VPATH=../../openbsd-compat
CC=gcc
LD=gcc
CFLAGS=-g -O2 -Wall -Wpointer-arith -Wuninitialized -Wsign-compare -Wno-pointer-sign -Wformat-security -fno-strict-aliasing -fno-builtin-memset -fstack-protector-all -O2   -fPIE  -fstack-protector  -D_FORTIFY_SOURCE=2  -Wformat -Wformat-security  -DLOGIN_PROGRAM=\"/bin/login\" -DLOGIN_NO_ENDOPT -DSSH_EXTRAVERSION=\"Debian-6cg1\" -DWITH_LDAP_PUBKEY  
CPPFLAGS=-I. -I.. -I$(srcdir) -I$(srcdir)/..     -DHAVE_CONFIG_H
LIBS=-lcrypto -lutil -lz -lnsl  -lcrypt -g -O2 -Wall -Wpointer-arith -Wuninitialized -Wsign-compare -Wno-pointer-sign -Wformat-security -fno-strict-aliasing -fno-builtin-memset -fstack-protector-all -O2 -fPIE -fstack-protector -D_FORTIFY_SOURCE=2 -Wformat -Wformat-security -DLOGIN_PROGRAM="/bin/login" -DLOGIN_NO_ENDOPT -DSSH_EXTRAVERSION="Debian-6cg1" -DWITH_LDAP_PUBKEY -lgssapi_krb5 -lkrb5 -lk5crypto -lcom_err
AR=/usr/bin/ar
RANLIB=ranlib
INSTALL=/usr/bin/install -c
LDFLAGS=-L.  -fstack-protector-all -L/usr/lib -lldap -Wl,--as-needed -fPIE -pie -Wl,-z,relro -Wl,-z,now

OPENBSD=base64.o basename.o bindresvport.o daemon.o dirname.o fmt_scaled.o getcwd.o getgrouplist.o getopt.o getrrsetbyname.o glob.o inet_aton.o inet_ntoa.o inet_ntop.o mktemp.o pwcache.o readpassphrase.o realpath.o rresvport.o setenv.o setproctitle.o sha2.o sigact.o strlcat.o strlcpy.o strmode.o strsep.o strtonum.o strtoll.o strtoul.o vis.o

COMPAT=bsd-arc4random.o bsd-asprintf.o bsd-closefrom.o bsd-cray.o bsd-cygwin_util.o bsd-getpeereid.o bsd-misc.o bsd-nextstep.o bsd-openpty.o bsd-poll.o bsd-snprintf.o bsd-statvfs.o bsd-waitpid.o fake-rfc2553.o openssl-compat.o xmmap.o xcrypt.o

PORTS=port-aix.o port-irix.o port-linux.o port-solaris.o port-tun.o port-uw.o

.c.o:
	$(CC) $(CFLAGS) $(CPPFLAGS) -c $<

all: libopenbsd-compat.a

$(COMPAT): ../config.h
$(OPENBSD): ../config.h
$(PORTS): ../config.h

libopenbsd-compat.a:  $(COMPAT) $(OPENBSD) $(PORTS)
	$(AR) rv $@ $(COMPAT) $(OPENBSD) $(PORTS)
	$(RANLIB) $@

clean:
	rm -f *.o *.a core 

distclean: clean
	rm -f Makefile *~
