PORTNAME=	ruby-dcl
PORTVERSION=	1.8.1
PORTREVISION=	1
CATEGORIES=	science rubygems
MASTER_SITES=	RG

MAINTAINER=	murashin@gfd-dennou.org
COMMENT=	Ruby interface to the scientific graphic library DCL
WWW=		http://ruby.gfd-dennou.org/products/ruby-dcl/

LICENSE=	BSD2CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

DEPRECATED=	requires deprecated science/cdcl
EXPIRATION_DATE=	2023-04-21

BUILD_DEPENDS=	rubygem-narray>=0.5.5:math/rubygem-narray
LIB_DEPENDS=	libcdcl.so:science/cdcl \
		libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2
RUN_DEPENDS=	rubygem-narray>=0.5.5:math/rubygem-narray \
		rubygem-narray_miss>0:math/rubygem-narray_miss

USES=		gem gettext-runtime gnome xorg
USE_GNOME=	atk cairo gdkpixbuf2 glib20 gtk20 pango
USE_XORG=	ice sm x11

.include <bsd.port.mk>
