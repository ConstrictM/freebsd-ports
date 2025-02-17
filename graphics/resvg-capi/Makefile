PORTNAME=	resvg-c-api
DISTVERSIONPREFIX=	v
DISTVERSION=	0.30.0
CATEGORIES=	graphics

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	SVG rendering library (C++/Qt API)
WWW=		https://github.com/RazrFalcon/resvg

LICENSE=	MPL20
LICENSE_FILE=	${WRKSRC}/../LICENSE.txt

USES=		cargo
USE_LDCONFIG=	yes

USE_GITHUB=	yes
GH_ACCOUNT=	RazrFalcon
GH_PROJECT=	resvg

WRKSRC_SUBDIR=	c-api

CARGO_CRATES=	adler-1.0.2 \
		arrayref-0.3.7 \
		arrayvec-0.7.2 \
		base64-0.21.0 \
		bitflags-1.3.2 \
		bytemuck-1.13.1 \
		cfg-if-1.0.0 \
		color_quant-1.1.0 \
		crc32fast-1.3.2 \
		data-url-0.2.0 \
		flate2-1.0.25 \
		float-cmp-0.9.0 \
		fontconfig-parser-0.5.2 \
		fontdb-0.13.0 \
		gif-0.12.0 \
		imagesize-0.11.0 \
		jpeg-decoder-0.3.0 \
		kurbo-0.9.1 \
		libc-0.2.140 \
		log-0.4.17 \
		memmap2-0.5.10 \
		miniz_oxide-0.6.2 \
		once_cell-1.17.1 \
		pico-args-0.5.0 \
		png-0.17.7 \
		rctree-0.5.0 \
		rgb-0.8.36 \
		roxmltree-0.18.0 \
		rustybuzz-0.7.0 \
		simplecss-0.2.1 \
		siphasher-0.3.10 \
		slotmap-1.0.6 \
		smallvec-1.10.0 \
		strict-num-0.1.0 \
		svgtypes-0.11.0 \
		tiny-skia-0.8.3 \
		tiny-skia-path-0.8.3 \
		ttf-parser-0.18.1 \
		unicode-bidi-0.3.13 \
		unicode-bidi-mirroring-0.1.0 \
		unicode-ccc-0.1.2 \
		unicode-general-category-0.6.0 \
		unicode-script-0.5.5 \
		unicode-vo-0.1.0 \
		version_check-0.9.4 \
		weezl-0.1.7 \
		xmlparser-0.13.5 \
		xmlwriter-0.1.0

PLIST_FILES=	include/ResvgQt.h \
		include/resvg.h \
		lib/libresvg.a \
		lib/libresvg.so

do-install:
	${INSTALL_DATA} ${WRKSRC}/resvg.h ${STAGEDIR}${PREFIX}/include
	${INSTALL_DATA} ${WRKSRC}/ResvgQt.h ${STAGEDIR}${PREFIX}/include
	cd ${WRKDIR}/target && \
		${INSTALL_LIB} */release/libresvg.so ${STAGEDIR}${PREFIX}/lib && \
		${INSTALL_DATA} */release/libresvg.a ${STAGEDIR}${PREFIX}/lib

.include <bsd.port.mk>
