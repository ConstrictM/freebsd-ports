PORTNAME=	psycopg
PORTVERSION=	3.1.8
PORTREVISION=	1
CATEGORIES=	databases python
MASTER_SITES=	PYPI
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	PostgreSQL database adapter for Python
WWW=		https://www.psycopg.org/ \
		https://github.com/psycopg/psycopg

LICENSE=	LGPL3
LICENSE_FILE=	${WRKSRC}/LICENSE.txt

BUILD_DEPENDS=	${PYTHON_PKGNAMEPREFIX}setuptools>=49.2.0:devel/py-setuptools@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}wheel>=0.37:devel/py-wheel@${PY_FLAVOR}

USES=		pgsql python:3.7+
USE_PYTHON=	autoplist concurrent pep517

NO_ARCH=	yes

OPTIONS_DEFINE=	C POOL
OPTIONS_DEFAULT=C POOL
C_DESC=		C extension support
POOL_DESC=	Connection pool support

C_RUN_DEPENDS=		${PYTHON_PKGNAMEPREFIX}psycopg-c>=3.1.6<${PORTVERSION}_99:databases/py-psycopg-c@${PY_FLAVOR}
POOL_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}psycopg-pool>=0:databases/py-psycopg-pool@${PY_FLAVOR}

.include <bsd.port.pre.mk>

.if ${PYTHON_REL} < 30900
RUN_DEPENDS+=	${PYTHON_PKGNAMEPREFIX}backports.zoneinfo>=0.2.0:devel/py-backports.zoneinfo@${PY_FLAVOR}
.endif

.if ${PYTHON_REL} < 31100
RUN_DEPENDS+=	${PYTHON_PKGNAMEPREFIX}typing-extensions>=4.1:devel/py-typing-extensions@${PY_FLAVOR}
.endif

.include <bsd.port.post.mk>
