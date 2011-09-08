# $Id: Makefile.in,v 1.4 2006/08/19 09:12:14 dtucker Exp $

sysconfdir=/etc/ssh
piddir=/var/run
srcdir=../../../openbsd-compat/regress
top_srcdir=../../..

VPATH=../../../openbsd-compat/regress
CC=gcc
LD=gcc
CFLAGS=-g -O2 -Wall -Wpointer-arith -Wuninitialized -Wsign-compare -Wno-pointer-sign -Wformat-security -fno-strict-aliasing -fno-builtin-memset -fstack-protector-all -Os -DSSH_EXTRAVERSION=\"Debian-6cg1\" 
CPPFLAGS=-I. -I.. -I$(srcdir) -I$(srcdir)/..  -DHAVE_CONFIG_H
EXEEXT=
LIBCOMPAT=../libopenbsd-compat.a
LIBS=-lcrypto -ldl -lutil -lz  -lcrypt -lresolv
LDFLAGS= -fstack-protector-all -Wl,--as-needed $(LIBCOMPAT)

TESTPROGS=closefromtest$(EXEEXT) snprintftest$(EXEEXT) strduptest$(EXEEXT) \
	strtonumtest$(EXEEXT)

all:	t-exec ${OTHERTESTS}

%$(EXEEXT):	%.c
	$(CC) $(CFLAGS) $(CPPFLAGS) $(LDFLAGS) -o $@ $< $(LIBCOMPAT) $(LIBS)

t-exec:	$(TESTPROGS)
	@echo running compat regress tests
	@for TEST in ""$?; do \
		echo "run test $${TEST}" ... 1>&2; \
		./$${TEST}$(EXEEXT) || exit $$? ; \
	done
	@echo finished compat regress tests

clean:
	rm -f *.o *.a core $(TESTPROGS) valid.out

distclean: clean
	rm -f Makefile *~
