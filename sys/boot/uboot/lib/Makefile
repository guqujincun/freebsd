# $FreeBSD$

.include <bsd.init.mk>

.PATH: ${LDRSRC}

LIB=		uboot
INTERNALLIB=
WARNS?=		2

SRCS=	console.c copy.c devicename.c elf_freebsd.c glue.c
SRCS+=	module.c net.c reboot.c time.c

CFLAGS+=	-ffreestanding -msoft-float

.if ${LOADER_DISK_SUPPORT:Uyes} == "yes"
SRCS+= disk.c
.endif

.if ${MK_FDT} != "no"
LOADER_FDT_SUPPORT=	yes
.else
LOADER_FDT_SUPPORT=	no
.endif

.if ${LOADER_FDT_SUPPORT} == "yes"
CFLAGS+= -DLOADER_FDT_SUPPORT -I${FDTSRC}
.endif

# Pick up FDT includes
CFLAGS+=	-I${SYSDIR}/contrib/libfdt/

# Pick up the bootstrap header for some interface items
CFLAGS+=	-I${LDRSRC} -I${SYSDIR} -I.

.ifdef(BOOT_DISK_DEBUG)
# Make the disk code more talkative
CFLAGS+= -DDISK_DEBUG
.endif

.include <bsd.stand.mk>
.include <bsd.lib.mk>
