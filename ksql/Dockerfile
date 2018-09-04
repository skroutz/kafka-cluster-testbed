FROM debian:stretch

# Faster debian mirror
RUN sed -i -e 's|http://deb.debian.org|http://debian.anycast-test.mirrors.debian.org|' /etc/apt/sources.list
RUN sed -i -e 's|http://security.debian.org|http://security.anycast-test.mirrors.debian.org/|' /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    procps \
    curl gnupg \
    openjdk-8-jre-headless

# Setup skroutz repositories
ADD skroutz-stable.list /etc/apt/sources.list.d/
ADD skroutz-pu.list /etc/apt/sources.list.d/
RUN curl -sSL http://debian.skroutz.gr/skroutz.asc | apt-key add -


RUN apt-get update && apt-get install -y --no-install-recommends \
    confluent-ksql

ADD ksql-server.properties /etc/ksql/ksql-server.properties

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

EXPOSE 8088

ENTRYPOINT ["/usr/bin/ksql-server-start", "/etc/ksql/ksql-server.properties"]