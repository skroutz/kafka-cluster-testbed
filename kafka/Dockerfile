FROM debian:stretch

ARG KAFKAPKG

# Faster debian mirror
RUN sed -i -e 's|http://deb.debian.org|http://debian.anycast-test.mirrors.debian.org|' /etc/apt/sources.list
RUN sed -i -e 's|http://security.debian.org|http://security.anycast-test.mirrors.debian.org/|' /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    procps \
    curl gnupg \
    ruby \
    openjdk-8-jre-headless

# Setup skroutz repositories
ADD skroutz-stable.list /etc/apt/sources.list.d/
ADD skroutz-pu.list /etc/apt/sources.list.d/
RUN curl -sSL https://debian.skroutz.gr/skroutz.asc | apt-key add -

RUN echo $KAFKAPKG
RUN apt-get update && apt-get install -y --no-install-recommends \
    $KAFKAPKG \
    kafkacat

ADD kafka /usr/local/bin/kafka

EXPOSE 9092

ENTRYPOINT ["/usr/local/bin/kafka"]
