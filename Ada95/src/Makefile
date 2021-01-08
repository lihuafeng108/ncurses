##############################################################################
# Copyright (c) 1998-2014,2015 Free Software Foundation, Inc.                #
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
#  $Id: Makefile.in,v 1.71 2015/08/05 23:15:41 tom Exp $
#
.SUFFIXES:

SHELL		= /bin/sh

THIS		= Makefile

MODEL		= ../../obj_s

DESTDIR		= 

top_srcdir	= ../..
srcdir		= .
prefix		= /mnt/share/work/3th_lib/build
exec_prefix	= ${prefix}
includedir	= ${prefix}/include
libdir		= ${exec_prefix}/lib

LIBDIR		= $(DESTDIR)$(libdir)
ADA_INCLUDE	= $(DESTDIR)/mnt/share/work/3th_lib/build/share/ada/adainclude
ADA_OBJECTS	= $(DESTDIR)/mnt/share/work/3th_lib/build/lib/ada/adalib

INSTALL		= /usr/bin/install -c
INSTALL_LIB	= /usr/bin/install -c -m 644

AR		= arm-linux-gnueabihf-ar
ARFLAGS		= -curv
AWK		= mawk
LN_S		= cp -p -f

CC		= arm-linux-gnueabihf-gcc
CFLAGS		= -O2 --param max-inline-insns-single=1200

CPPFLAGS	= -I. -I../include -I../../include  -I${includedir} -I. -I../include  -D_GNU_SOURCE -D_FILE_OFFSET_BITS=64  -DNDEBUG \
		  -DHAVE_CONFIG_H -I$(srcdir)

CCFLAGS		= $(CPPFLAGS) $(CFLAGS)

CFLAGS_NORMAL	= $(CCFLAGS)
CFLAGS_DEBUG	= $(CCFLAGS) -g -DTRACE
CFLAGS_PROFILE	= $(CCFLAGS) -pg
CFLAGS_SHARED	= $(CCFLAGS) -fPIC

CFLAGS_DEFAULT	= $(CFLAGS_SHARED)

LINK		= $(CC)
LDFLAGS		=   

RANLIB		= arm-linux-gnueabihf-ranlib

################################################################################
ADA             = gnatmake
ADAPREP		= gnatprep
ADAFLAGS        =  -gnatpn -O2 -I. -I$(srcdir)

LIB_NAME	= AdaCurses
SONAME		= lib$(LIB_NAME).so.1

GNAT_PROJECT	= $(srcdir)/library.gpr

# build/source are the Ada95 tree
BUILD_DIR	= ..
SOURCE_DIR	= ..

BUILD_DIR_LIB	= $(BUILD_DIR)/lib
SOURCE_DIR_SRC	= $(SOURCE_DIR)/src

ADAMAKE         = gnatmake
ADAMAKEFLAGS    = \
	-P$(GNAT_PROJECT) \
	-XBUILD_DIR=`cd $(BUILD_DIR);pwd` \
	-XSOURCE_DIR=`cd $(SOURCE_DIR);pwd` \
	-XSOURCE_DIR2=`cd $(srcdir);pwd` \
	-XLIB_NAME=$(LIB_NAME) \
	-XSONAME=$(SONAME)

CARGS           = -cargs $(ADAFLAGS)
LARGS           =

STATIC_LIBNAME	= lib$(LIB_NAME).a
SHARED_LIBNAME	= $(SONAME)
SHARED_SYMLINK	= lib$(LIB_NAME).so

ALIB            = terminal_interface
ABASE           = $(ALIB)-curses
################################################################################
GENERATED_SOURCES=$(ABASE).ads         			\
		  $(ABASE).adb         			\
	          $(ABASE)-aux.ads   			\
	          $(ABASE)-trace.ads   			\
	          $(ABASE)-menus.ads   			\
	          $(ABASE)-forms.ads   			\
	          $(ABASE)-mouse.ads 			\
	          $(ABASE)-panels.ads			\
	          $(ABASE)-menus-menu_user_data.ads	\
	          $(ABASE)-menus-item_user_data.ads	\
	          $(ABASE)-forms-form_user_data.ads	\
	          $(ABASE)-forms-field_types.ads	\
	          $(ABASE)-forms-field_user_data.ads	\
	          $(ABASE)-panels-user_data.ads
################################################################################
LIBOBJS=$(ALIB).o                			\
	$(ABASE)-aux.o           			\
	$(ABASE).o               			\
	$(ABASE)-terminfo.o				\
	$(ABASE)-termcap.o				\
	$(ABASE)-putwin.o				\
	$(ABASE)-trace.o				\
	$(ABASE)-mouse.o         			\
	$(ABASE)-panels.o        			\
	$(ABASE)-menus.o         			\
	$(ABASE)-forms.o         			\
	$(ABASE)-forms-field_types.o      		\
	$(ABASE)-forms-field_types-alpha.o      	\
	$(ABASE)-forms-field_types-alphanumeric.o	\
	$(ABASE)-forms-field_types-intfield.o     	\
	$(ABASE)-forms-field_types-numeric.o     	\
	$(ABASE)-forms-field_types-regexp.o       	\
	$(ABASE)-forms-field_types-enumeration.o	\
	$(ABASE)-forms-field_types-ipv4_address.o	\
	$(ABASE)-forms-field_types-user.o 		\
	$(ABASE)-forms-field_types-user-choice.o 	\
	$(ABASE)-text_io.o       			\
	$(ABASE)-text_io-aux.o

# Ada object files for generic packages. Since gnat 3.10 they are
# also compiled
GENOBJS=$(ABASE)-menus-menu_user_data.o			\
	$(ABASE)-menus-item_user_data.o			\
	$(ABASE)-forms-form_user_data.o			\
	$(ABASE)-forms-field_user_data.o		\
	$(ABASE)-forms-field_types-enumeration-ada.o	\
	$(ABASE)-panels-user_data.o			\
	$(ABASE)-text_io-integer_io.o			\
	$(ABASE)-text_io-float_io.o			\
	$(ABASE)-text_io-fixed_io.o			\
	$(ABASE)-text_io-decimal_io.o			\
	$(ABASE)-text_io-enumeration_io.o		\
	$(ABASE)-text_io-modular_io.o			\
	$(ABASE)-text_io-complex_io.o

all ::  $(BUILD_DIR_LIB)/$(STATIC_LIBNAME)
	@echo done

$(ADA_INCLUDE) \
$(ADA_OBJECTS) \
$(LIBDIR) \
$(BUILD_DIR_LIB) :
	mkdir -p $@

sources :
	@echo made $@

libs \
install \
install.libs :: \
		$(BUILD_DIR_LIB)/$(STATIC_LIBNAME)
	@echo made $(STATIC_LIBNAME)

install \
install.libs :: \
		$(BUILD_DIR_LIB)/$(STATIC_LIBNAME) \
		$(ADA_OBJECTS)
	@$(INSTALL_LIB) \
		$(BUILD_DIR_LIB)/$(STATIC_LIBNAME) \
		$(ADA_OBJECTS)

uninstall \
uninstall.libs ::
	@rm -f $(ADA_OBJECTS)/$(STATIC_LIBNAME)

mostlyclean ::
	rm -f *.o *.ali b_t*.* *.s $(PROGS) a.out core b_*_test.c *.xr[bs] *.a

clean :: mostlyclean
	rm -f $(ABASE)-trace.adb

distclean :: clean
	rm -f Makefile

realclean :: distclean

BASEDEPS=$(ABASE).ads $(ABASE)-aux.ads $(ABASE).adb

$(ABASE)-trace.adb : $(srcdir)/$(ABASE)-trace.adb_p
	rm -f $@
	$(ADAPREP) -DADA_TRACE=FALSE -T  $(srcdir)/$(ABASE)-trace.adb_p $@

###############################################################################
# Use these definitions when building a shared library.
SHARED_C_OBJS	= c_varargs_to_ada.o c_threaded_variables.o ncurses_compat.o
SHARED_OBJS 	= $(SHARED_C_OBJS) #$(LIBOBJS) ${GENOBJS}

c_varargs_to_ada.o :	$(srcdir)/c_varargs_to_ada.c
	$(CC) $(CFLAGS_DEFAULT) -c -o $@ $(srcdir)/c_varargs_to_ada.c

c_threaded_variables.o : $(srcdir)/c_threaded_variables.c
	$(CC) $(CFLAGS_DEFAULT) -c -o $@ $(srcdir)/c_threaded_variables.c

ncurses_compat.o :	$(srcdir)/ncurses_compat.c
	$(CC) $(CFLAGS_DEFAULT) -c -o $@ $(srcdir)/ncurses_compat.c

###############################################################################
# Use these definitions when building a static library.
STATIC_C_OBJS	= static_c_varargs_to_ada.o static_c_threaded_variables.o static_ncurses_compat.o
STATIC_OBJS 	= $(STATIC_C_OBJS) #$(LIBOBJS) ${GENOBJS}

static_c_varargs_to_ada.o :	$(srcdir)/c_varargs_to_ada.c
	$(CC) $(CFLAGS_NORMAL) -c -o $@ $(srcdir)/c_varargs_to_ada.c

static_c_threaded_variables.o : $(srcdir)/c_threaded_variables.c
	$(CC) $(CFLAGS_NORMAL) -c -o $@ $(srcdir)/c_threaded_variables.c

static_ncurses_compat.o :	$(srcdir)/ncurses_compat.c
	$(CC) $(CFLAGS_NORMAL) -c -o $@ $(srcdir)/ncurses_compat.c

###############################################################################

#$(BUILD_DIR_LIB)/$(STATIC_LIBNAME) :: \
#		$(BUILD_DIR_LIB) \
#		$(STATIC_OBJS)
#	$(AR) $(ARFLAGS) $@ $(STATIC_OBJS)

$(BUILD_DIR)/static-ali : ; mkdir -p $@
$(BUILD_DIR)/static-obj : ; mkdir -p $@

STATIC_DIRS = \
	$(BUILD_DIR_LIB) \
	$(BUILD_DIR)/static-ali \
	$(BUILD_DIR)/static-obj

$(BUILD_DIR_LIB)/$(STATIC_LIBNAME) :: \
		$(ABASE)-trace.adb \
		$(STATIC_C_OBJS) \
		$(STATIC_DIRS)
	$(ADAMAKE) $(ADAMAKEFLAGS) -XLIB_KIND=static
	$(AR) $(ARFLAGS) $@ $(STATIC_C_OBJS)

install \
install.libs :: \
		$(ADA_OBJECTS)
	$(INSTALL_LIB) \
		$(BUILD_DIR)/static-ali/*.ali \
		$(ADA_OBJECTS)

uninstall \
uninstall.libs ::
	@rm -f $(ADA_OBJECTS)/$(STATIC_LIBNAME)

uninstall \
uninstall.libs ::
	@$(SHELL) -c 'for name in $(BUILD_DIR)/static-ali/*.ali ; do rm -f $(ADA_OBJECTS)/`basename $$name`; done'

$(BUILD_DIR)/dynamic-ali : ; mkdir -p $@
$(BUILD_DIR)/dynamic-obj : ; mkdir -p $@

SHARED_DIRS = \
	$(BUILD_DIR_LIB) \
	$(BUILD_DIR)/dynamic-ali \
	$(BUILD_DIR)/dynamic-obj

#all :: $(BUILD_DIR_LIB)/$(SHARED_LIBNAME)
#$(BUILD_DIR_LIB)/$(SHARED_LIBNAME) :: \
#		$(ABASE)-trace.adb \
#		$(SHARED_DIRS) \
#		$(SHARED_OBJS)
#	cp $(SHARED_OBJS) $(BUILD_DIR)/dynamic-obj/
#	$(ADAMAKE) $(ADAMAKEFLAGS) -XLIB_KIND=dynamic

install \
install.libs :: $(ADA_INCLUDE)
	$(INSTALL_LIB) \
		$(SOURCE_DIR_SRC)/*.ad[sb] \
		$(ADA_INCLUDE)

install \
install.libs :: $(ADA_INCLUDE)
	$(INSTALL_LIB) \
		$(GENERATED_SOURCES) \
		$(ADA_INCLUDE)

uninstall \
uninstall.libs ::
	$(SHELL) -c 'for name in $(SOURCE_DIR_SRC)/*.ad[sb] $(GENERATED_SOURCES); do rm -f $(ADA_INCLUDE)/`basename $$name`; done'

#install \
#install.libs :: $(ADA_OBJECTS) $(LIBDIR)
#	$(INSTALL_LIB) \
#		$(BUILD_DIR)/dynamic-ali/* \
#		$(ADA_OBJECTS)
#	$(INSTALL_LIB) \
#		$(BUILD_DIR_LIB)/$(SHARED_LIBNAME) \
#		$(LIBDIR)
#	cd $(LIBDIR) && $(LN_S) $(SHARED_LIBNAME) $(SHARED_SYMLINK)
#
#uninstall \
#uninstall.libs ::
#	$(SHELL) -c 'for name in $(BUILD_DIR)/dynamic-ali/* ; do rm -f $(ADA_OBJECTS)/`basename $$name`; done'
#
#uninstall \
#uninstall.libs ::
#	rm -f $(LIBDIR)/$(SHARED_SYMLINK)
#	rm -f $(LIBDIR)/$(SHARED_LIBNAME)

clean ::
	rm -rf $(BUILD_DIR)/*-ali
	rm -rf $(BUILD_DIR)/*-obj
	rm -rf $(BUILD_DIR_LIB)
