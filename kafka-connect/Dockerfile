FROM openjdk:11.0.8-jre-slim-buster as build-stage

ENV KAFKA_VERSION 2.6.0
ENV SCALA_VERSION 2.13

WORKDIR /opt/kafka

RUN apt update -y \
  && apt install wget -y \
  && wget https://downloads.apache.org/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz \
  && tar --strip-components=1 -zvxf kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz \
  && rm -rf kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz

FROM openjdk:11.0.8-jre-slim-buster

COPY --from=build-stage /opt/kafka /opt/kafka

WORKDIR /opt/kafka

EXPOSE 8083

CMD [ "./bin/connect-distributed.sh", "./config/connect-distributed.properties" ]
