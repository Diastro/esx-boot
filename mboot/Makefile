#*******************************************************************************
# Copyright (c) 2008-2017 VMware, Inc.  All rights reserved.
# SPDX-License-Identifier: GPL-2.0
#*******************************************************************************

#
# Mboot Makefile
#

TOPDIR      := ..
include common.mk

SRC         := config.c              \
               elf.c                 \
               $(IARCH)/elf_arch.c   \
               gui.c                 \
               load.c                \
               mboot.c               \
               $(IARCH)/multiboot.c  \
               mutiboot.c            \
               $(IARCH)/mutiboot_arch.c \
               reloc.c               \
               secure.c              \
               system.c              \
               $(IARCH)/system_arch.c\

ifeq ($(IARCH),x86)
#
# NASM source - x86 and x64.
#
SRC += $(IARCH)/trampoline.s
else
#
# GNU AS source - arm64.
#
SRC += $(IARCH)/trampoline.S
endif

TARGETTYPE  := app
INC += .

ifeq (,$(EKEY))
   BASENAME := mboot
   LIBS     := $(BOOTLIB) $(ENV_LIB)
else
   BASENAME := mboot-$(EKEY)
   INC      += $(CRYPTOINC)
   CFLAGS   += -D$(EKEY) -DSECURE_BOOT
   LIBS     := $(BOOTLIB) $(CRYPTOLIB) $(ENV_LIB)
endif

include rules.mk
