# Created by: Olivier Duchateau
# $FreeBSD$

PORTNAME=	corebird
PORTVERSION=	1.5
PORTREVISION=	1
CATEGORIES=	net-im

MAINTAINER=	cpm@FreeBSD.org
COMMENT=	GTK3 Twitter client written in Vala

LICENSE=	GPLv3+
LICENSE_FILE=	${WRKSRC}/COPYING

BUILD_DEPENDS=	valac:lang/vala
LIB_DEPENDS=	libsoup-2.4.so:devel/libsoup \
		libnotify.so:devel/libnotify \
		libjson-glib-1.0.so:devel/json-glib \
		librest-0.7.so:devel/librest \
		libgspell-1.so:textproc/gspell

USE_GITHUB=	yes
GH_ACCOUNT=	baedert

USES=		autoreconf gmake libtool pkgconfig sqlite

GNU_CONFIGURE=	yes
USE_GNOME=	atk cairo gdkpixbuf2 glib20 gtk30 intltool libxml2 pango
INSTALLS_ICONS=	yes

OPTIONS_DEFINE=		GSTREAMER NLS
OPTIONS_DEFAULT=	GSTREAMER
OPTIONS_SUB=		yes

GSTREAMER_LIB_DEPENDS=		libgstbase-1.0.so:multimedia/gstreamer1 \
				libgstreamer-1.0.so:multimedia/gstreamer1
GSTREAMER_USE=			gstreamer1=yes,bad,good,gtksink,hls,libav,soup,x,ximagesrc
GSTREAMER_CONFIGURE_OFF=	--disable-video

NLS_USES=			gettext
NLS_CONFIGURE_OFF=		--disable-nls

GLIB_SCHEMAS=	org.baedert.corebird.gschema.xml

post-extract:
	@(cd ${WRKSRC}/data && ${MV} org.baedert.corebird.desktop.in \
		corebird.desktop.in)

# Replace locales files in right place
post-configure:
	@${REINPLACE_CMD} -e 's|[$$][(]DATADIRNAME[)]|share|' \
		${WRKSRC}/po/Makefile

.include <bsd.port.mk>
