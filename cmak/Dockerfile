FROM debian:buster as build-stage
LABEL maintainer=gigioSouza<giovane.bds@gmail.com>

WORKDIR /opt/cmak

RUN apt update -y \
  && apt install -y wget unzip \
  && wget https://github.com/gigioSouza/CMAK/releases/download/3.0.0.5-zk3.4.13/cmak-3.0.0.5.zip \
  && unzip cmak-3.0.0.5.zip

FROM openjdk:11.0.8-jre-slim-buster

COPY --from=build-stage /opt/cmak/cmak-3.0.0.5 /opt/cmak

WORKDIR /opt/cmak

EXPOSE 8080

ENTRYPOINT ["bin/cmak"]
CMD ["-Dconfig.file=conf/application.conf", "-Dhttp.port=8080", "-Dpidfile.path=/dev/null"]

HEALTHCHECK CMD curl -f http://127.0.0.1/api/health || exit 1