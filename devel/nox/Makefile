PORTNAME=	nox
PORTVERSION=	2022.11.21
PORTREVISION=	1
CATEGORIES=	devel python
#MASTER_SITES=	PYPI # no tests

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	Flexible test automation
WWW=		https://nox.thea.codes/en/stable/

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

PY_DEPENDS=	${PYTHON_PKGNAMEPREFIX}argcomplete>=1.9.4<3.0:devel/py-argcomplete@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}colorlog>=2.6.1<7.0.0:devel/py-colorlog@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}packaging>=20.9:devel/py-packaging@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}virtualenv>=14:devel/py-virtualenv@${PY_FLAVOR}
BUILD_DEPENDS=	${PY_DEPENDS} \
		${PYTHON_PKGNAMEPREFIX}wheel>0:devel/py-wheel@${PY_FLAVOR}
RUN_DEPENDS=	${PY_DEPENDS}

USES=		python:3.8+
USE_PYTHON=	pep517 autoplist pytest # tests fail to run, see https://github.com/wntrblm/nox/issues/689

USE_GITHUB=	yes
GH_ACCOUNT=	wntrblm

NO_ARCH=	yes

.include <bsd.port.mk>
