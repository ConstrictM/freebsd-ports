PORTNAME=	milter-callback
PORTVERSION=	1.6.0
PORTREVISION=	8
CATEGORIES=	mail
MASTER_SITES=	LOCAL/ehaupt

MAINTAINER=	ehaupt@FreeBSD.org
COMMENT=	Milter to perform a envelope-from sender verification on target MX
WWW=		http://unix.zhegan.in

LICENSE=	GPLv3

LIB_DEPENDS=	libspf2.so:mail/libspf2

USES=		compiler tar:xz
USE_RC_SUBR=	milter-callback
USE_GCC=	yes

SUB_FILES=	pkg-message

SRC_FILES=	cache.c commonprocs.c cpit.c dealwithmxes.c detectlamespf.c \
		makedecision.c mcspf.c milter-callback.c pgupdate.c \
		processdirectpart.c processmxpart.c pushhistory.c sigusr1.c

CFLAGS+=	-DFREEBSD -DHAVE_NS_TYPE -DWITH_SPF -I${LOCALBASE}/include \
		-I${WRKSRC} -std=gnu99
LDFLAGS+=	-lmilter -lthr -L${LOCALBASE}/lib -lspf2

.include <bsd.port.pre.mk>

do-build:
.for f in ${SRC_FILES}
	${CC} ${CFLAGS} -c ${WRKSRC}/${f} -o ${WRKSRC}/${f:C/\.c/.o/}
.endfor
	${CC} ${LDFLAGS} ${SRC_FILES:C/(.*)\.c/${WRKSRC}\/\1.o/} \
		-o ${WRKSRC}/${PORTNAME}

post-patch:
	@${REINPLACE_CMD} -e "s|/usr/local|${PREFIX}|" \
		${WRKSRC}/${PORTNAME}.c
	@${REINPLACE_CMD} -e "s|/usr/local|${LOCALBASE}|" \
		${WRKSRC}/Makefile
	@${REINPLACE_CMD} -e 's|/var/tmp/|/var/run/|' \
		${WRKSRC}/${PORTNAME}.conf

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/libexec
	${INSTALL_MAN} ${WRKSRC}/${PORTNAME}.8 ${STAGEDIR}${MANPREFIX}/man/man8

	@${MKDIR} ${STAGEDIR}${PREFIX}/etc/mail
	${INSTALL_DATA} ${WRKSRC}/${PORTNAME}.conf \
		${STAGEDIR}${PREFIX}/etc/mail/${PORTNAME}.conf.sample

.include <bsd.port.post.mk>
