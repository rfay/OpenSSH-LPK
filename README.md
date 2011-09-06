This is just an attempt to organize resources for an Openssh 5.5p1 OpenSSH LPK patch for a Debian Squeeze package.

Here are some resources:

* [Patching with LPK and HPN](http://zecrazytux.net/articles/Sysadmin/OpenSSH_LPK+HPN.html) (Quite dated, and it doesn't actually work out.
* [The openssh-lpk project page](http://code.google.com/p/openssh-lpk/source/checkout) which does not have a 5.5p1 patch. In the contrib directory it only has up through 5.4p1. (The openssh-lpk project is included here in the openssh-lpk-read-only directory)
* The [openssh-lpk Google group](http://groups.google.com/group/openssh-lpk), where [only one](http://groups.google.com/group/openssh-lpk/t/25af025dfad1da2d) reference is made to 5.5p1, and that got no answer. But there is a [5.6p1 patch](http://groups.google.com/group/openssh-lpk/t/94526e83898deda9).
* The [Fedora commit](http://pkgs.fedoraproject.org/gitweb/?p=openssh.git;a=tree;h=ad92f9c7485c5bf66520453ca00ffbd5a9997dbb;hb=7818e56d625e05b7b3a727cb8784e4adbece4bbb) with appropriate patches. Note that the fedora patch only fails in the makefile.
* The [openssh-lpk CVS repo](http://cvs.pld-linux.org/cgi-bin/cvsweb.cgi/packages/openssh/openssh-lpk.patch) from cvs.pld-linux.org. 1.4 does not apply. 1.6 does not apply. However, this line seems promising.
* Mandriva provides patches. They're here, extracted from the Mandriva SRPM. Also don't apply. I got the Mandriva SRPM from http://ftp.yandex.ru/mandriva/devel/2010.1/SRPMS/main/release/ Here's an [actual repository link](http://ftp.yandex.ru/mandriva/devel/2010.1/SRPMS/main/release/openssh-5.5p1-2mdv2010.1.src.rpm)


WIN: The openssh-lpk-read-only patch contrib-openssh-lpk-5.4p1-0.3.13.patch can be edited by a single line in version.h to update the version, and this patch then applies. I have left that adjusted patch as openssh-lpk-read-only/patch/contrib/contrib-openssh-lpk-5.5p1-0.3.13.patch


UPDATE: 
  apt-get source openssh
  cd openssh-5.5p1
  dquilt pop -a  # so that we can apply the LPK patch first
  dquilt import contrib-openssh-lpk-5.5p1-0.3.13.patch  # from above
  dquilt push
  dquilt refresh
  dquilt header -e

  while dquilt push
  do
    dquilt refresh
  done

This patch applies, and everything ends up in the man pages, for example, but when you uncomment the LPK configuration in the /etc/ssh/sshd_config, it complains:

  /etc/ssh/sshd_config: line 49: Bad configuration option: UseLPK
  /etc/ssh/sshd_config: line 50: Bad configuration option: LpkLdapConf
/etc/ssh/sshd_config: terminating, 2 bad configuration options