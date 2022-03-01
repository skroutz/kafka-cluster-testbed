FROM debian:buster

ARG KAFKAPKG

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    procps \
    curl gnupg \
    ruby \
    default-jre-headless

# Setup skroutz repositories
RUN curl -sSL https://debian.skroutz.gr/skroutz.asc | apt-key add -

ADD skroutz-stable.list /etc/apt/sources.list.d/
RUN apt-get update  && apt-get install -y --no-install-recommends skroutz-archive-keyring

ADD skroutz-pu.list /etc/apt/sources.list.d/
RUN echo $KAFKAPKG
RUN apt-get update && apt-get install -y --no-install-recommends \
    $KAFKAPKG \
    kafkacat

ADD kafka /usr/local/bin/kafka

EXPOSE 9092

ENTRYPOINT ["/usr/local/bin/kafka"]
