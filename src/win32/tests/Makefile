#
# BAREOS® - Backup Archiving REcovery Open Sourced
#
# Copyright (C) 2015-2015 Bareos GmbH & Co. KG
#
# This program is Free Software; you can redistribute it and/or
# modify it under the terms of version three of the GNU Affero General Public
# License as published by the Free Software Foundation and included
# in the file LICENSE.
#
# This program is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
# Affero General Public License for more details.
#
# You should have received a copy of the GNU Affero General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA
# 02110-1301, USA.
#
VPATH = .:../../tests

include ../Makefile.inc

INCLUDES = -I../.. \
	   -I../../include \
	   -I../include \
	   -I../compat/include \
	   -I../vss/include
LDLIBS = ../lib/libbareos.a \
	 ../lib/libbareos.dll \
         $(MINGW_LIB)/libpthreadGCE2.a \
         $(MINGW_LIB)/libz.dll.a \
         $(MINGW_LIB)/libreadline.dll.a \
	 $(WINSOCKLIB) -lole32 -loleaut32 -luuid

GROWSRCS = grow.c
GROWOBJS = $(GROWSRCS:.c=.o)

#WINDRESSRCS = growres.rc
#WINDRESOBJS = $(WINDRESSRCS:.rc=.o)

all: grow.exe

grow.exe: DLL_USAGE = -DUSING_DLL
grow.exe: $(GROWOBJS) $(WINDRESOBJS)
	$(CXX) $(LDFLAGS_GROW) $(GROWOBJS) $(LDLIBS) -o $@

clean:
	rm -f *.o

distclean:: clean
	rm -f grow.exe

# inference rules
.c.o:
	@echo "Compiling $<"
	$(CXX) $(DLL_USAGE) $(CXXFLAGS) -c -o $@ $<

%.o : %.rc
	@echo "Ressource Compiling $^"
	$(WINDRES) $^ -o $@