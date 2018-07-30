FROM debian:stretch

# Faster debian mirror
RUN sed -i -e 's|http://deb.debian.org|http://debian.anycast-test.mirrors.debian.org|' /etc/apt/sources.list
RUN sed -i -e 's|http://security.debian.org|http://security.anycast-test.mirrors.debian.org/|' /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    procps \
    curl gnupg \
    ruby

# Setup skroutz repositories
ADD skroutz-stable.list /etc/apt/sources.list.d/
ADD skroutz-pu.list /etc/apt/sources.list.d/
RUN curl -sSL https://debian.skroutz.gr/skroutz.asc | apt-key add -

RUN apt-get update && apt-get install -y --no-install-recommends \
    kafkacat \
    rafka

ADD config.json /etc/rafka/config.json
EXPOSE 6380

ENTRYPOINT ["/usr/bin/rafka", "--kafka", "/etc/rafka/config.json"]
