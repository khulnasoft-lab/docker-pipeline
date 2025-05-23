FROM alpine:3.21.3
LABEL maintainer="security@khulnasoft.com"

ARG SONARSCANNER_VERSION

ENV PATH=/sonar-scanner/bin:/sonar-scanner/jre/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

ARG GLIBC_VERSION
ARG SONARSCANNER_VERSION
ARG ZLIB_VERSION

RUN echo "Starting ..." && \
    apk --update upgrade && apk add curl make tzdata unzip && \
    echo "Done base install!" && \
    echo "Starting Sonar Scanner" && \
    curl -sSL https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub -o /etc/apk/keys/sgerrand.rsa.pub && \
    curl -sSL https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk -O && \
    apk add -q --force-overwrite glibc-${GLIBC_VERSION}.apk && \
    rm /etc/apk/keys/sgerrand.rsa.pub glibc-${GLIBC_VERSION}.apk && \
    curl -LfsS https://archive.archlinux.org/packages/z/zlib/zlib-1%3A{$ZLIB_VERSION}-x86_64.pkg.tar.xz -o /tmp/libz.tar.xz && \
    mkdir /tmp/libz && \
    tar -xf /tmp/libz.tar.xz -C /tmp/libz && \
    mv /tmp/libz/usr/lib/libz.so* /usr/glibc-compat/lib && \
    curl -o ./sonarscanner.zip -L https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONARSCANNER_VERSION}-linux.zip && \
    unzip sonarscanner.zip && \
    rm sonarscanner.zip && \
    mv sonar-scanner-${SONARSCANNER_VERSION}-linux sonar-scanner && \
    echo "Done Sonar Scanner!" && \
    echo "Cleaning files!" && \
    rm -rf /tmp/* /var/cache/apk/* && \
    echo "Done!"