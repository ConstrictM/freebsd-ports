PORTNAME=	github-markup
PORTVERSION=	1.7.0
CATEGORIES=	textproc rubygems
MASTER_SITES=	RG
PKGNAMESUFFIX=	17

MAINTAINER=	mfechner@FreeBSD.org
COMMENT=	Render any fancy markup
WWW=		https://github.com/github/markup

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		gem shebangfix

CONFLICTS_INSTALL=	rubygem-github-markup*

NO_ARCH=	yes

REINPLACE_ARGS=	-i ''

PLIST_FILES=	bin/github-markup

SHEBANG_FILES=	script/*

PORTSCOUT=	limit:^1\.7\.

post-patch:
	@${REINPLACE_CMD} -e '1d' ${WRKSRC}/lib/github/commands/rest2html

.include <bsd.port.mk>
