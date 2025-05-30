FROM thingsboard/openjdk17:bookworm-slim

LABEL maintainer="thingsboard"

RUN mkdir -p /opt/project/thingsboard/data /opt/project/thingsboard/conf /opt/project/thingsboard/logs

WORKDIR /opt/project/thingsboard

EXPOSE 18080

ENV TZ=Asia/Shanghai \
    LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    JAVA_OPTS="-Xms2g -Xmx4g -XX:+UseG1GC -XX:MaxGCPauseMillis=200" \
    LOGGING_CONFIG="/opt/project/thingsboard/conf/logback.xml" \
    LOG_FOLDER="/opt/project/thingsboard/logs" \
    LOG_FILE_NAME="thingsboard"

ARG BUILD_VERSION

COPY ./thingsboard-${BUILD_VERSION}-boot.jar ./thingsboard.jar

ENTRYPOINT java ${JAVA_OPTS} -Djava.security.egd=file:/dev/./urandom \
    -Dlogging.config=${LOGGING_CONFIG} \
    -Dpkg.logFolder=${LOG_FOLDER} \
    -Dpkg.name=${LOG_FILE_NAME} \
    -jar thingsboard.jar
