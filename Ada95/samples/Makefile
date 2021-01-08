##############################################################################
# Copyright (c) 1998-2012,2015 Free Software Foundation, Inc.                #
#                                                                            #
# Permission is hereby granted, free of charge, to any person obtaining a    #
# copy of this software and associated documentation files (the "Software"), #
# to deal in the Software without restriction, including without limitation  #
# the rights to use, copy, modify, merge, publish, distribute, distribute    #
# with modifications, sublicense, and/or sell copies of the Software, and to #
# permit persons to whom the Software is furnished to do so, subject to the  #
# following conditions:                                                      #
#                                                                            #
# The above copyright notice and this permission notice shall be included in #
# all copies or substantial portions of the Software.                        #
#                                                                            #
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR #
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,   #
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL    #
# THE ABOVE COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER      #
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING    #
# FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER        #
# DEALINGS IN THE SOFTWARE.                                                  #
#                                                                            #
# Except as contained in this notice, the name(s) of the above copyright     #
# holders shall not be used in advertising or otherwise to promote the sale, #
# use or other dealings in this Software without prior written               #
# authorization.                                                             #
##############################################################################
#
#  Author:  Juergen Pfeifer, 1996
#
#  $Id: Makefile.in,v 1.49 2015/08/05 23:15:41 tom Exp $
#
.SUFFIXES:

SHELL		= /bin/sh

THIS		= Makefile

x		= 

srcdir		= .
prefix		= /mnt/share/work/3th_lib/build
exec_prefix	= ${prefix}
bindir		= ${exec_prefix}/bin
datarootdir	= ${prefix}/share
datadir		= ${datarootdir}
libdir		= ${exec_prefix}/lib
includedir	= ${prefix}/include

INSTALL		= /usr/bin/install -c
INSTALL_DATA	= ${INSTALL} -m 644

AWK		= mawk
LN_S		= cp -p -f

CC		= arm-linux-gnueabihf-gcc
CFLAGS		= -O2 --param max-inline-insns-single=1200

CPPFLAGS	= -I. -I../include -I../../include  -I${includedir} \
		  -DHAVE_CONFIG_H -I$(srcdir)

CCFLAGS		= $(CPPFLAGS) $(CFLAGS)

CFLAGS_NORMAL	= $(CCFLAGS)
CFLAGS_DEBUG	= $(CCFLAGS) -g -DTRACE
CFLAGS_PROFILE	= $(CCFLAGS) -pg
CFLAGS_SHARED	= $(CCFLAGS) -fPIC

CFLAGS_DEFAULT	= $(CFLAGS_SHARED)

REL_VERSION	= 6.0
ABI_VERSION	= 6
LOCAL_LIBDIR	= /mnt/share/work/3th_lib/src/ncurses-6.0/lib

LINK		= $(CC)
LDFLAGS		=   

RANLIB		= arm-linux-gnueabihf-ranlib
################################################################################
BINDIR		= $(DESTDIR)$(bindir)
DATADIR		= $(DESTDIR)$(datadir)
LIBDIR		= $(DESTDIR)$(libdir)

MY_DATADIR	= $(DATADIR)/AdaCurses

################################################################################
ada_srcdir=../src

LD_FLAGS     =  $(LOCAL_LIBS)   -Wl,-rpath,$(LOCAL_LIBDIR) $(LDFLAGS)

ADA          = gnatmake
ADAFLAGS     =  -gnatpn -O2 -I$(srcdir)

ADAMAKE      = gnatmake
ADAMAKEFLAGS = -a -A$(srcdir) -A$(ada_srcdir) -A$(srcdir)/$(ada_srcdir)

ALIB         = terminal_interface
ABASE        = $(ALIB)-curses

CARGS        =-cargs $(ADAFLAGS)
LARGS        =-largs -L../lib -lAdaCurses -L../../lib -lform -lmenu -lpanel -lncurses  $(LD_FLAGS) 

PROGS        = tour$x ncurses$x  rain$x 

all ::  $(PROGS)
	@echo made $@

sources :
	@echo made $@

libs \
install \
install.libs ::
	@echo made $@

uninstall \
uninstall.libs ::
	@echo made $@

install.examples :: $(BINDIR) $(PROGS)
	$(INSTALL) $(PROGS) $(BINDIR)

install.examples :: $(MY_DATADIR)
	$(INSTALL_DATA) explain.txt $(MY_DATADIR)

uninstall.examples ::
	-cd $(BINDIR) && rm -f $(PROGS)
	-rmdir $(BINDIR)
	-rm -f $(MY_DATADIR)/explain.txt
	-rmdir $(MY_DATADIR)

$(BINDIR) \
$(MY_DATADIR) :
	mkdir -p $@

ncurses$x :
	$(ADAMAKE) $(ADAMAKEFLAGS) ncurses $(CARGS) $(LARGS)

tour$x :
	$(ADAMAKE) $(ADAMAKEFLAGS) tour $(CARGS) $(LARGS)

rain$x :
	$(ADAMAKE) $(ADAMAKEFLAGS) rain $(CARGS) $(LARGS)

mostlyclean:
	@echo made $@

clean :: mostlyclean
	rm -f *.o *.ali b_t*.* *.s $(PROGS) a.out core b_*_test.c *.xr[bs] \
	trace screendump b~*.ad[bs]

distclean :: clean
	rm -f Makefile

realclean :: distclean
	@echo made $@
