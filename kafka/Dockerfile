FROM debian:stretch

ARG KAFKAPKG

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
