PORTNAME=	rlvm
DISTVERSIONPREFIX=	release-
DISTVERSION=	0.14-77
DISTVERSIONSUFFIX=	-gfabf134a
PORTREVISION=	3
CATEGORIES=	games

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	RealLive virtual machine clone
WWW=		http://www.rlvm.net/

LICENSE=	GPLv2 GPLv3 MIT
LICENSE_COMB=	multi

BROKEN_FreeBSD_12_powerpc64=	fails to link on powerpc64 elfv1: gcn_platform.cc: undefined reference to gcn::Exception::Exception

BUILD_DEPENDS=	boost-libs>0:devel/boost-libs \
		utf8cpp>0:devel/utf8cpp
LIB_DEPENDS=	libsndfile.so:audio/libsndfile \
		libvorbisfile.so:audio/libvorbis \
		libguichan.so:devel/guichan
RUN_DEPENDS=	${LOCALBASE}/share/fonts/dejavu/DejaVuSans.ttf:x11-fonts/dejavu

USE_GITHUB=	yes
GH_ACCOUNT=	eglaysher

USES=		compiler:c++11-lib gl gnome pkgconfig scons sdl
USE_GL=		glew glu
USE_GNOME=	gtk20
USE_SDL=	image mixer ttf
EXCLUDE=	GLEW SDL_image SDL_mixer SDL_ttf gmock gtest guichan \
		luabind utf8cpp # leaving only pygame, xclannad, *.cpp
EXTRACT_AFTER_ARGS=${EXCLUDE:S,^,--exclude vendor/,}
LDFLAGS+=	-Wl,--as-needed # avoid overlinking (gtk deps)
MAKE_ARGS=	VERBOSE=1
PORTDOCS=	AUTHORS.TXT NEWS.TXT README.md STATUS.TXT notes

OPTIONS_DEFINE=	DEBUG DOCS NLS TEST
OPTIONS_DEFAULT=MONA
OPTIONS_MULTI=	JAPANESE_FONT
OPTIONS_MULTI_JAPANESE_FONT=KOCHI MONA SAZANAMI
OPTIONS_SUB=	yes

JAPANESE_FONT_DESC=msgothic.ttc alternatives with verified metrics (unless --font)
KOCHI_DESC=	kochi-gothic-subst.ttf from japanese/font-kochi
KOCHI_RUN_DEPENDS=${LOCALBASE}/share/fonts/kochi/kochi-gothic-subst.ttf:japanese/font-kochi
MONA_DESC=	mona.ttf from japanese/font-mona-ttf
MONA_RUN_DEPENDS=${LOCALBASE}/share/fonts/mona-ttf/mona.ttf:japanese/font-mona-ttf
SAZANAMI_DESC=	sazanami-gothic.ttf from japanese/font-sazanami
SAZANAMI_RUN_DEPENDS=${LOCALBASE}/share/fonts/sazanami/sazanami-gothic.ttf:japanese/font-sazanami

DEBUG_MAKE_ARGS_OFF=--release
NLS_USES=	gettext
NLS_EXTRA_PATCHES_OFF=${FILESDIR}/extra-patch-disable-nls
TEST_USES=	lua:51
TEST_BUILD_DEPENDS=googletest>=1.7.0:devel/googletest \
		luabind>0:devel/luabind
TEST_EXTRA_PATCHES_OFF=${FILESDIR}/extra-patch-disable-test

post-patch:
	@${REINPLACE_CMD} -e "s/boost_[^\"]*/:lib&$$'\\\x2e'a/" \
		${WRKSRC}/SConstruct
	@${REINPLACE_CMD} -e 's,/usr/share,${PREFIX}/share,' \
		${WRKSRC}/src/platforms/gtk/gtk_rlvm_instance.cc
	@${REINPLACE_CMD} -e 's,/usr/share,${LOCALBASE}/share,' \
		-e 's,truetype/ttf-dejavu,dejavu,' \
		-e 's,truetype/mona,mona-ttf,' \
		-e 's,truetype/,,' \
		${WRKSRC}/src/utilities/find_font_file.cc

do-test-TEST-on:
	(cd ${WRKSRC} && build/${PORTNAME}_unittests)

pre-install-TEST-on: do-test-TEST-on

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/build/${PORTNAME} \
		${STAGEDIR}${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/debian/${PORTNAME}.6 \
		${STAGEDIR}${PREFIX}/share/man/man6
	${INSTALL_DATA} ${WRKSRC}/src/platforms/gtk/${PORTNAME}.desktop \
		${STAGEDIR}${DESKTOPDIR}
	@(cd ${WRKSRC}/resources && for f in */${PORTNAME}.png; do \
		${MKDIR} ${STAGEDIR}${PREFIX}/share/icons/hicolor/$${f%/*}x$${f%/*}/apps; \
		${INSTALL_DATA} -v $$f \
			${STAGEDIR}${PREFIX}/share/icons/hicolor/$${f%/*}x$${f%/*}/apps; \
	done)

post-install-NLS-on:
	(cd ${WRKSRC}/build/locale && ${COPYTREE_SHARE} \
		. ${STAGEDIR}${PREFIX}/share/locale)

post-install-DOCS-on:
	(cd ${WRKSRC} && ${COPYTREE_SHARE} \
		"${PORTDOCS:Nnotes}" ${STAGEDIR}${DOCSDIR})
	(cd ${WRKSRC}/doc && ${COPYTREE_SHARE} \
		notes ${STAGEDIR}${DOCSDIR})

.include <bsd.port.mk>
