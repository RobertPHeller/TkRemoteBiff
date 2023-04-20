##-*- makefile -*-############################################################
#
#  System        : 
#  Module        : 
#  Object Name   : $RCSfile$
#  Revision      : $Revision$
#  Date          : $Date$
#  Author        : $Author$
#  Created By    : Robert Heller
#  Created       : Wed Jul 29 12:28:40 2020
#  Last Modified : <200729.1347>
#
#  Description	
#
#  Notes
#
#  History
#	
#  $Log$
#
##############################################################################
#
#    Copyright (C) 2020  Robert Heller D/B/A Deepwoods Software
#			51 Locke Hill Road
#			Wendell, MA 01379-9728
#
#    This program is free software; you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation; either version 2 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License
#    along with this program; if not, write to the Free Software
#    Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
#
# 
#
##############################################################################


ACLOCAL_AMFLAGS = -I m4
SUBDIRS = BuildScripts Scripts
EXTRA_DIST = bootstrap TkRemoteBiff.src

bin_SCRIPTS = TkRemoteBiff$(EXEEXT)

CLEANFILES  = TkRemoteBiff.kit $(bin_SCRIPTS)

AddKitDir = $(top_srcdir)/BuildScripts/AddKitDir.kit
AddKitFile = $(top_srcdir)/BuildScripts/AddKitFile.kit
MakePkgIndex = $(top_srcdir)/BuildScripts/MakePkgIndex.kit

TkRemoteBiffScripts = Scripts/IconsAndImages.tcl \
		Scripts/ReadConfiguration.tcl Scripts/snitdialog.tcl \
		Scripts/snitLFs.tcl Scripts/snitbuttonbox.tcl \
		Scripts/unknown.xpm Scripts/HaveMail.png \
		Scripts/NoMail.png

TkRemoteBiff$(EXEEXT): TkRemoteBiff.src $(TkRemoteBiffScripts)
	-rm -rf TkRemoteBiff.vfs TkRemoteBiff.kit
	$(TCLKIT) $(SDX) qwrap $(srcdir)/TkRemoteBiff.src
	$(TCLKIT) $(SDX) unwrap TkRemoteBiff.kit
	-rm -rf TkRemoteBiff.kit
	$(TCLKIT) $(AddKitDir) TkRemoteBiff lib $(SNITLIB)
	$(TCLKIT) $(AddKitDir) TkRemoteBiff lib $(IMAP4LIB)
	$(TCLKIT) $(AddKitDir) TkRemoteBiff lib $(TLSLIB)
	$(TCLKIT) $(AddKitDir) TkRemoteBiff lib $(IMGLIB)
	$(TCLKIT) $(AddKitFile) -srcdir $(srcdir) TkRemoteBiff \
		lib/Common $(TkRemoteBiffScripts)
	$(TCLKIT) $(MakePkgIndex) TkRemoteBiff Common
	cp $(TCLKIT) runtime$(EXEEXT)
	$(TCLKIT) $(SDX) wrap TkRemoteBiff$(EXEEXT) -runtime runtime$(EXEEXT)
	rm -rf runtime$(EXEEXT) TkRemoteBiff.vfs
