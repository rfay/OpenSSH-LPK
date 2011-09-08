# $Id: Makefile.in,v 1.4 2006/08/19 09:12:14 dtucker Exp $

sysconfdir=/etc/ssh
piddir=/var/run
srcdir=../../../openbsd-compat/regress
top_srcdir=../../..

VPATH=../../../openbsd-compat/regress
CC=gcc
LD=gcc
CFLAGS=-g -O2 -Wall -Wpointer-arith -Wuninitialized -Wsign-compare -Wno-pointer-sign -Wformat-security -fno-strict-aliasing -fno-builtin-memset -fstack-protector-all -O2   -fPIE  -fstack-protector  -D_FORTIFY_SOURCE=2  -Wformat -Wformat-security  -DLOGIN_PROGRAM=\"/bin/login\" -DLOGIN_NO_ENDOPT -DSSH_EXTRAVERSION=\"Debian-6cg1\" -DWITH_LDAP_PUBKEY  
CPPFLAGS=-I. -I.. -I$(srcdir) -I$(srcdir)/..     -DHAVE_CONFIG_H
EXEEXT=
LIBCOMPAT=../libopenbsd-compat.a
LIBS=-lcrypto -lutil -lz -lnsl  -lcrypt -g -O2 -Wall -Wpointer-arith -Wuninitialized -Wsign-compare -Wno-pointer-sign -Wformat-security -fno-strict-aliasing -fno-builtin-memset -fstack-protector-all -O2 -fPIE -fstack-protector -D_FORTIFY_SOURCE=2 -Wformat -Wformat-security -DLOGIN_PROGRAM="/bin/login" -DLOGIN_NO_ENDOPT -DSSH_EXTRAVERSION="Debian-6cg1" -DWITH_LDAP_PUBKEY -lgssapi_krb5 -lkrb5 -lk5crypto -lcom_err
LDFLAGS= -fstack-protector-all -L/usr/lib -lldap -Wl,--as-needed -fPIE -pie -Wl,-z,relro -Wl,-z,now $(LIBCOMPAT)

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
