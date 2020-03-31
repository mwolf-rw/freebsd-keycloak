# $FreeBSD$

PORTNAME=	keycloak-gatekeeper
PORTVERSION=	9.0.2
CATEGORIES=	net

MAINTAINER=	freebsd@rheinwolf.de
COMMENT=	OpenID Connect proxy server

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		go:modules

USE_RC_SUBR=	keycloak-gatekeeper

USE_GITHUB=	yes
GH_ACCOUNT=	keycloak
GH_TUPLE=	PuerkitoBio:purell:v1.1.0:puerkitobio_purell/vendor/github.com/PuerkitoBio/purell \
		PuerkitoBio:urlesc:de5bf2ad4578:puerkitobio_urlesc/vendor/github.com/PuerkitoBio/urlesc \
		armon:go-proxyproto:5b7edb60ff5f:armon_go_proxyproto/vendor/github.com/armon/go-proxyproto \
		beorn7:perks:3a771d992973:beorn7_perks/vendor/github.com/beorn7/perks \
		bsm:ratelimit:db14e161995a:bsm_ratelimit/vendor/gopkg.in/bsm/ratelimit.v1 \
		codegangsta:negroni:v1.0.0:codegangsta_negroni/vendor/github.com/codegangsta/negroni \
		coreos:go-oidc:e860bd55bfa7:coreos_go_oidc/vendor/github.com/coreos/go-oidc \
		coreos:pkg:399ea9e2e55f:coreos_pkg/vendor/github.com/coreos/pkg \
		davecgh:go-spew:v1.1.1:davecgh_go_spew/vendor/github.com/davecgh/go-spew \
		elazarl:goproxy:2ce16c963a8a:elazarl_goproxy/vendor/github.com/elazarl/goproxy \
		etcd-io:bbolt:v1.3.3:etcd_io_bbolt/vendor/github.com/etcd-io/bbolt \
		etcd-io:bbolt:v1.3.3:etcd_io_bbolt_1/vendor/go.etcd.io/bbolt \
		fsnotify:fsnotify:v1.4.7:fsnotify_fsnotify/vendor/github.com/fsnotify/fsnotify \
		garyburd:redigo:v1.6.0:garyburd_redigo/vendor/github.com/garyburd/redigo \
		go-chi:chi:v3.3.3:go_chi_chi/vendor/github.com/go-chi/chi \
		go-redis:redis:v4.2.4:go_redis_redis/vendor/gopkg.in/redis.v4 \
		go-resty:resty:v1.10.3:go_resty_resty/vendor/gopkg.in/resty.v1 \
		go-yaml:yaml:v2.2.2:go_yaml_yaml/vendor/gopkg.in/yaml.v2 \
		golang:crypto:505ab145d0a9:golang_crypto/vendor/golang.org/x/crypto \
		golang:net:351d144fa1fc:golang_net/vendor/golang.org/x/net \
		golang:protobuf:v1.2.0:golang_protobuf/vendor/github.com/golang/protobuf \
		golang:sys:062a44052db1:golang_sys/vendor/golang.org/x/sys \
		golang:text:v0.3.0:golang_text/vendor/golang.org/x/text \
		jonboulle:clockwork:v0.1.0:jonboulle_clockwork/vendor/github.com/jonboulle/clockwork \
		kylelemons:godebug:d65d576e9348:kylelemons_godebug/vendor/github.com/kylelemons/godebug \
		matttproud:golang_protobuf_extensions:v1.0.1:matttproud_golang_protobuf_extensions/vendor/github.com/matttproud/golang_protobuf_extensions \
		onsi:ginkgo:v1.8.0:onsi_ginkgo/vendor/github.com/onsi/ginkgo \
		onsi:gomega:v1.5.0:onsi_gomega/vendor/github.com/onsi/gomega \
		pkg:errors:v0.8.1:pkg_errors/vendor/github.com/pkg/errors \
		pmezard:go-difflib:v1.0.0:pmezard_go_difflib/vendor/github.com/pmezard/go-difflib \
		prometheus:client_golang:v0.9.2:prometheus_client_golang/vendor/github.com/prometheus/client_golang \
		prometheus:client_model:5c3871d89910:prometheus_client_model/vendor/github.com/prometheus/client_model \
		prometheus:common:4724e9255275:prometheus_common/vendor/github.com/prometheus/common \
		prometheus:procfs:1dc9a6cbc91a:prometheus_procfs/vendor/github.com/prometheus/procfs \
		rs:cors:v1.6.0:rs_cors/vendor/github.com/rs/cors \
		satori:go.uuid:v1.2.0:satori_go_uuid/vendor/github.com/satori/go.uuid \
		stretchr:testify:v1.2.2:stretchr_testify/vendor/github.com/stretchr/testify \
		uber-go:atomic:v1.3.2:uber_go_atomic/vendor/go.uber.org/atomic \
		uber-go:multierr:v1.1.0:uber_go_multierr/vendor/go.uber.org/multierr \
		uber-go:zap:v1.9.1:uber_go_zap/vendor/go.uber.org/zap \
		unrolled:secure:0d6b5bb13069:unrolled_secure/vendor/github.com/unrolled/secure \
		urfave:cli:b67dcf995b6a:urfave_cli/vendor/github.com/urfave/cli

USER=		www
GROUP=		www

VAR_DIR?=	/var
LOG_DIR?=	${VAR_DIR}/log/keycloak
RUN_DIR?=	${VAR_DIR}/run/keycloak

SUB_LIST+=	GROUP=${GROUP} \
		LOG_DIR=${LOG_DIR} \
		PORTNAME=${PORTNAME} \
		PREFIX=${PREFIX} \
		RUN_DIR=${RUN_DIR} \
		USER=${USER}

post-patch:
	${RM} ${WRKSRC}/vendor/github.com/etcd-io/bbolt
	${LN} -s ${WRKSRC}/vendor/go.etcd.io/bbolt ${WRKSRC}/vendor/github.com/etcd-io/bbolt

post-install:
	${MKDIR} ${STAGEDIR}${LOG_DIR}
	${MKDIR} ${STAGEDIR}${RUN_DIR}
	${INSTALL_DATA} ${FILESDIR}/keycloak-gatekeeper.yaml ${STAGEDIR}${PREFIX}/etc/keycloak-gatekeeper.yaml.sample

.include <bsd.port.mk>
