FROM	alpine:3.12

MAINTAINER still_lm@sin.com
LABEL	org.label-schema.description="Useful network related tools for Devops"
LABEL	org.label-schema.author=liming
LABEL	org.label-schema.version=1.0

RUN	apk add --no-cache --update \
		bash \
		conntrack-tools \
		coreutils \
		curl \
		drill \
		iperf3 \
		iproute2 \
		iptables \
		iputils \
		ip6tables \
		keepalived \
		net-tools \
		nftables \
		socat \
		ethtool \
		mtr \
		tcpdump \
    openssh-client \
		busybox-extras \
		mysql-client \
    tzdata \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apk del tzdata

ARG REDIS_VERSION="4.0.0"
ARG REDIS_DOWNLOAD_URL="http://download.redis.io/releases/redis-${REDIS_VERSION}.tar.gz"

RUN apk add --update --no-cache --virtual build-deps gcc make linux-headers musl-dev tar \
    && wget -O redis.tar.gz "$REDIS_DOWNLOAD_URL" \
    && mkdir -p /usr/src/redis \
    && tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1 \
    && rm redis.tar.gz \
    && make -C /usr/src/redis install redis-cli /usr/bin \
    && rm -r /usr/src/redis \
    && apk del build-deps \
    && rm -rf /var/cache/apk/*

ENTRYPOINT bash
