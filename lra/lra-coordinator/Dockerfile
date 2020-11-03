FROM registry.access.redhat.com/ubi8/ubi-minimal
MAINTAINER Ondrej Chaloupka <ochaloup@redhat.com>
EXPOSE 8080

WORKDIR /work/

ARG NARAYANA_VERSION
RUN test -n "$NARAYANA_VERSION" || (echo "NARAYANA_VERSION  not set" && false)

RUN curl -LOk https://www.jboss.org/jbosstm/downloads/${NARAYANA_VERSION}/binary/narayana-full-${NARAYANA_VERSION}-bin.zip \
    && unzip -j narayana-full-${NARAYANA_VERSION}-bin.zip narayana-full-${NARAYANA_VERSION}/rts/lra/lra-coordinator-runner -d /work/application \
    && rm narayana-full-$NARAYANA_VERSION-bin.zip

# expected values INFO, DEBUG, TRACE...
ENV LOG_LEVEL="INFO"
# path to the data directory (persistent volume)
ENV OBJECT_STORE_PATH="/data"

CMD ["./application", "-Dquarkus.http.host=0.0.0.0", "-Dquarkus.log.level=${LOG_LEVEL}"]
