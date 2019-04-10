FROM openjdk:8u212-jdk-stretch

MAINTAINER networkfox ohbugs@foxmail.com

ENV VERSION=20.0

WORKDIR /opt/yanagishima-${VERSION}

ADD https://github.com/yanagishima/yanagishima/archive/20.0.zip yanagishima.zip

RUN rm /etc/apt/sources.list && \
    echo "deb [check-valid-until=no] http://cdn-fastly.deb.debian.org/debian jessie main" | tee -a /etc/apt/sources.list && \
    echo "deb [check-valid-until=no] http://archive.debian.org/debian jessie-backports main" | tee -a /etc/apt/sources.list && \
    echo "Acquire::Check-Valid-Until false;" | tee -a /etc/apt/apt.conf.d/10-nocheckvalid && \
    echo 'Package: *\nPin: origin "archive.debian.org"\nPin-Priority: 500' | tee -a /etc/apt/preferences.d/10-archive-pin && \
    apt-get -o Acquire::Check-Valid-Until=false update && \
    wget https://github.com/yanagishima/yanagishima/archive/${VERSION}.zip -O yanagishima-${VERSION}-source.zip && \
    unzip yanagishima-${VERSION}-source.zip && \
    cd yanagishima-${VERSION}-source && \
    ./gradlew distZip && \
    rm ../yanagishima-${VERSION}-source.zip && \
    nohup build/distributions/yanagishima-20.0/bin/yanagishima-start.sh >y.log 2>&1 &

COPY . .

EXPOSE 8080

