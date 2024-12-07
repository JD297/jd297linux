PREFIX		= .

SRCDIR		= $(PREFIX)/src

BINDIR		= $(PREFIX)/bin
SBINDIR		= $(PREFIX)/sbin
LIBDIR		= $(PREFIX)/lib

USRDIR		= $(PREFIX)/usr
USRBINDIR	= $(USRDIR)/bin
USRSBINDIR	= $(USRDIR)/sbin
USRMANDIR	= $(USRDIR)/share/man
USRLIBDIR	= $(USRDIR)/lib
USRINCLUDEDIR	= $(USRDIR)/include
USRLOCALDIR	= $(USRDIR)/local

CORES		= 4

TMPDIR		= $(PREFIX)/tmp
MNTDIR		= $(PREFIX)/mnt
DEVDIR		= $(PREFIX)/dev
ETCDIR		= $(PREFIX)/etc
ROOTDIR		= $(PREFIX)/root
PROCDIR		= $(PREFIX)/proc
VARDIR		= $(PREFIX)/var
BOOTDIR		= $(PREFIX)/boot

all: / boot/bzImage $(USRLIBDIR)/libc.a $(USRLIBDIR)/libasm.a $(USRBINDIR)/coreutils $(USRBINDIR)/edt

src/linux:
	cd src/ && git clone --depth 1 git@github.com:torvalds/linux

$(USRINCLUDEDIR)/linux: src/linux
	cd src/linux && make headers_install ARCH=x86_64 INSTALL_HDR_PATH=../../$(USRDIR)

src/linux/.config: src/linux
	cd src/linux && make menuconfig

boot/bzImage: boot src/linux/.config
	cd src/linux && make -j $(CORES)
	

src/libc:
	cd src/ && git clone git@github.com:jd297/libc.git

$(USRLIBDIR)/libc.a: usr $(USRINCLUDEDIR)/linux src/libc
	cd src/libc && make install PREFIX=../../$(USRDIR)

src/libasm:
	cd src/ && git clone git@github.com:jd297/libasm.git

$(USRLIBDIR)/libasm.a: usr $(USRINCLUDEDIR)/linux src/libasm
	cd src/libasm && make install PREFIX=../../$(USRDIR)

src/coreutils:
	cd src/ && git clone git@github.com:jd297/coreutils

$(USRBINDIR)/coreutils: $(USRLIBDIR)/libc.a src/coreutils
	cd src/coreutils && make install PREFIX=../../$(USRDIR)

src/edt:
	cd src/ && git clone git@github.com:jd297/edt

$(USRBINDIR)/edt: $(USRLIBDIR)/libc.a src/edt
	cd src/edt && make install PREFIX=../../$(USRDIR)

/: usr usr/local tmp mnt dev etc root proc var bin sbin lib

usr:
	mkdir -p $(USRBINDIR) $(USRSBINDIR) $(USRMANDIR) $(USRLIBDIR) $(USRINCLUDEDIR) $(USRLOCALDIR)

usr/local: usr
	cp -r $(USRBINDIR) $(USRLOCALDIR)
	cp -r $(USRSBINDIR) $(USRLOCALDIR)
	cp -r $(USRMANDIR) $(USRLOCALDIR)
	cp -r $(USRLIBDIR) $(USRLOCALDIR)
	cp -r $(USRINCLUDEDIR) $(USRLOCALDIR)

tmp:
	mkdir $(TMPDIR)

mnt:
	mkdir $(MNTDIR)

dev:
	mkdir $(DEVDIR)

etc:
	mkdir $(ETCDIR)

root:
	mkdir $(ROOTDIR)

proc:
	mkdir $(PROCDIR)

var:
	mkdir $(VARDIR)

bin: usr
	ln -s $(subst $(PREFIX)/,,$(USRBINDIR)) $(BINDIR)

sbin: usr
	ln -s $(subst $(PREFIX)/,,$(USRSBINDIR)) $(SBINDIR)

lib: usr
	ln -s $(subst $(PREFIX)/,,$(USRLIBDIR)) $(LIBDIR)

clean:
	rm -Rf $(USRDIR) $(TMPDIR) $(MNTDIR) $(DEVDIR) $(ETCDIR) $(ROOTDIR) $(PROCDIR) $(VARDIR)
	unlink $(BINDIR) || true
	unlink $(LIBDIR) || true
	unlink $(SBINDIR) || true
