TARGET     = libgolibc.a
STACKSIZE  =
MALLOCSIZE =
MMAREA     =
OBJS       = abs.o atof.o atoi.o errno.o frexp.o ldexp.o \
	memchr.o memcmp.o memmove.o memset.o qsort.o rand.o \
	sprintf.o strcat.o strcmp.o strcpy.o strcspn.o strdup.o \
	strlen.o strncat.o strncmp.o strncpy.o strpbrk.o strrchr.o \
	strspn.o strstr.o strtol.o strtoul.o strtoul0.o vsprintf.o

GCC = /usr/local/i386elfgcc/bin/i386-elf-gcc
CFLAGS = -I. -fno-common -Wall -O2 -c \
         -finhibit-size-directive -fno-ident \
         -fomit-frame-pointer -fcall-used-ebx
AR = /usr/local/i386elfgcc/bin/i386-elf-ar
RANLIB = /usr/local/i386elfgcc/bin/i386-elf-ranlib

ALL : ${OBJS}
	${AR} rv ${TARGET} ${OBJS}
	${RANLIB} ${TARGET}

%.o : %.c Makefile
	${GCC} ${CFLAGS} $<

clean :
	rm -f *.o ${TARGET}
