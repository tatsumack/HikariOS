OBJS_BOOTPACK = bootpack.o naskfunc.o hankaku.obj graphic.o dsctbl.o \
		int.o fifo.o keyboard.o mouse.o memory.o sheet.o timer.o \
		mtask.o window.o console.o file.o tek.o

TOOLPATH = ../../z_tools/
INCPATH  = ../../z_tools/haribote/
LIBPATH  = ../../golibc

MAKE     = make -r
NASM     = nasm
GCC      = /usr/local/i386elfgcc/bin/i386-elf-gcc
LD       = /usr/local/i386elfgcc/bin/i386-elf-ld
MAKEFONT = $(TOOLPATH)makefont
BIN2OBJ  = $(TOOLPATH)bin2obj
COPY     = cp
DEL      = rm -f

# デフォルト動作

default :
	$(MAKE) ipl09.bin
	$(MAKE) haribote.sys

# ファイル生成規則

ipl09.bin : ipl09.nas Makefile
	$(NASM) ipl09.nas -o ipl09.bin -l ipl09.lst

asmhead.bin : asmhead.nas Makefile
	$(NASM) asmhead.nas -o asmhead.bin -l asmhead.lst

naskfunc.o : naskfunc.nas Makefile
	$(NASM) -felf naskfunc.nas -o naskfunc.o -l naskfunc.lst

hankaku.bin : hankaku.txt Makefile
	$(MAKEFONT) hankaku.txt hankaku.bin

hankaku.obj : hankaku.bin Makefile
	$(BIN2OBJ) hankaku.bin hankaku.obj hankaku

bootpack.bin : $(OBJS_BOOTPACK) Makefile
	$(LD) -m elf_i386 -Map bootpack.map -T bootpack.ls -oformat=binary $(OBJS_BOOTPACK) -static -L$(LIBPATH) -lgolibc -o bootpack.bin 

haribote.sys : asmhead.bin bootpack.bin Makefile
	cat asmhead.bin bootpack.bin > haribote.sys

# 一般規則

%.o : %.c Makefile
	$(GCC) -m32 -g -O0 -nostdlib -I$(INCPATH) -c $*.c -o $*.o

# コマンド

clean :
	-$(DEL) asmhead.bin
	-$(DEL) hankaku.bin
	-$(DEL) *.lst
	-$(DEL) *.obj
	-$(DEL) *.o
	-$(DEL) *.map
	-$(DEL) *.bim
	-$(DEL) *.hrb

src_only :
	$(MAKE) clean
	-$(DEL) ipl09.bin
	-$(DEL) haribote.sys
