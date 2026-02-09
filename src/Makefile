# ***********************************************************************************
#
#  RCL9's Makefile for "hex_file_overlay_of_sysgen_image.exe"
#
# ***********************************************************************************

# NOTE: Use 'unsigned char'

# Name of the Windows executable file 
WIN_EXENAME = hex_file_overlay_of_sysgen_image

OUT = /Fo
OBJ = obj

# -------------------->>>>  Directory Locations  <<<<-----------------------

# Object file directory
OBJ_DIRECTORY = vc4_obj\\

# ------------------------->>>>  Objects <<<<--------------------------------

all: $(WIN_EXENAME)

# ------------->>>>  Microsoft Visual Studio C++  <<<<---------------

# Uncomment for no debugging
NODEBUG = 1

CPU= 
	
# Include the standard Makefile defines for this specific platform
!include <ntwin32.mak>

!IFNDEF NODEBUG
VC4_OPT = 
!ELSE
cdebug = /Ogityb2 /Gs /Gy
!ENDIF

# _DLL = Used when linking against msvcrt.dll (needed for the DLL modules)
# Warning level 3, ANSI only, Compile w/o linking, unsigned char
VC4_COMMON_CFLAGS = /D_NO_MFC_SUPPORT /D_MT /MT /nologo /W3 /c /J /DOS_WIN32 /DWIN32 /DMSDOS /DWINDOWS3 $(DEBUG_MALLOC) /I\nugraf\lib\c /I\nugraf\c /I\nugraf\lib\import 

CFLAGS = 

VC4_LINK_OPTIONS  = $(lflags) $(linkdebug) /FORCE

$(WIN_EXENAME): $(OBJ_DIRECTORY)hex_file_overlay_of_sysgen_image.obj 
	$(link) /nologo $(conflags) /OUT:$(WIN_EXENAME).exe $(VC4_LINK_OPTIONS) $(OBJ_DIRECTORY)hex_file_overlay_of_sysgen_image.obj $(guilibsmt) 

$(OBJ_DIRECTORY)hex_file_overlay_of_sysgen_image.obj : hex_file_overlay_of_sysgen_image.cpp
	 $(cc) $(cflags) $(VC4_COMMON_CFLAGS) $(CFLAGS) $(cvars) $(cdebug) $(OUT)$(OBJ_DIRECTORY)hex_file_overlay_of_sysgen_image.$(OBJ) -c hex_file_overlay_of_sysgen_image.cpp

