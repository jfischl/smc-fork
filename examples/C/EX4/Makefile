#
# The contents of this file are subject to the Mozilla Public
# License Version 1.1 (the "License"); you may not use this file
# except in compliance with the License. You may obtain a copy
# of the License at http://www.mozilla.org/MPL/
#
# Software distributed under the License is distributed on an
# "AS IS" basis, WITHOUT WARRANTY OF ANY KIND, either express or
# implied. See the License for the specific language governing
# rights and limitations under the License.
#
# The Original Code is State Machine Compiler (SMC).
#
# The Initial Developer of the Original Code is Charles W. Rapp.
# Portions created by Charles W. Rapp are
# Copyright (C) 2000 Charles W. Rapp.
# All Rights Reserved.
#
# Contributor(s):
#       Port to C by Francois Perrad, francois.perrad@gadz.org
#
# RCS ID
# $Id: Makefile,v 1.8 2008/07/29 06:50:56 fperrad Exp $
#
# CHANGE LOG
# $Log: Makefile,v $
# Revision 1.8  2008/07/29 06:50:56  fperrad
# - add a target 'png'
#
# Revision 1.7  2008/04/24 09:29:51  fperrad
# + fix #1934494 : remove 'test' from 'all' target
#
# Revision 1.6  2008/02/04 10:59:19  fperrad
# + Exhibit options
#
# Revision 1.5  2008/01/24 07:50:17  fperrad
# - add a target 'table'
#
# Revision 1.4  2008/01/22 08:45:03  fperrad
# - add a target 'graph'
#
# Revision 1.3  2007/10/12 08:55:00  fperrad
# - refactor: Makefile with variables
#
# Revision 1.2  2007/08/05 13:43:36  cwrapp
# Version 5.0.1 check-in. See net/sf/smc/CODE_README.txt for more information.
#
# Revision 1.1  2005/06/16 18:00:35  fperrad
# Added C examples 1 - 4
#
#

#################################################################
# Macros.
#

SM_SOURCES=     stoplight.sm
SOURCES=        $(SM_SOURCES:.sm=_sm.c) \
                stoplight.c \
                main.c
HEADERS=        $(SM_SOURCES:.sm=_sm.h) \
                stoplight.h
OBJECTS=        $(SOURCES:.c=.o)
TARGET=         ./traffic

# Uncomment to turn on debug message generation.
TRACE=          -g

SMC=            java -jar ../../../bin/Smc.jar
SMC_FLAGS=      -c $(TRACE)

CC=             gcc
CFLAGS=         -g -I../../../lib/C

RM_F=           rm -f

#################################################################
# Rules.
#

%_sm.h %_sm.c : %.sm
		$(SMC) $(SMC_FLAGS) $<

%_sm.dot :      %.sm
		$(SMC) -graph -glevel 1 $<

%_sm.png :      %_sm.dot
		dot -T png -o $@ $<

%_sm.html :     %.sm
		$(SMC) -table $<

all :           $(TARGET)

$(TARGET) :     $(HEADERS) $(SOURCES)
		$(CC) $(CFLAGS) -o $@ $(SOURCES)

test :          $(TARGET)
		$(TARGET)

graph :         $(SM_SOURCES:%.sm=%_sm.dot)

png :           $(SM_SOURCES:%.sm=%_sm.png)

table :         $(SM_SOURCES:%.sm=%_sm.html)

clean :
		-$(RM_F) $(TARGET)
		-$(RM_F) $(OBJECTS)
		-$(RM_F) *_sm.h
		-$(RM_F) *_sm.c
		-$(RM_F) *_sm.dot
		-$(RM_F) *_sm.png
		-$(RM_F) *_sm.html
