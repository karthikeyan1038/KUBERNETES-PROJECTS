FROM bitnami/minideb-extras:stretch-r277
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV BITNAMI_PKG_CHMOD="-R g+rwX" \
    BITNAMI_PKG_EXTRA_DIRS="/home/tomcat" \
    HOME="/"

# Install required system packages and dependencies
RUN install_packages libc6 libgcc1
RUN bitnami-pkg install java-1.8.201-0 --checksum de49557872836fdbd965389ebcc72e163f7242cf691d435993cc2e4f3cd56ae7
RUN bitnami-pkg unpack tomcat-7.0.92-21 --checksum 37071a1c9d6ee8dd398b7dfec4aed7c4b809de5a33fb20d2c3d63b12781bcbf8
RUN ln -sf /opt/bitnami/tomcat/data /app

COPY rootfs /
ENV BITNAMI_APP_NAME="tomcat" \
    BITNAMI_IMAGE_VERSION="7.0.92-debian-9-r69" \
    JAVA_OPTS="-Djava.awt.headless=true -XX:+UseG1GC -Dfile.encoding=UTF-8" \
    NAMI_PREFIX="/.nami" \
    PATH="/opt/bitnami/java/bin:/opt/bitnami/tomcat/bin:$PATH" \
    TOMCAT_AJP_PORT_NUMBER="8009" \
    TOMCAT_ALLOW_REMOTE_MANAGEMENT="0" \
    TOMCAT_HOME="/home/tomcat" \
    TOMCAT_HTTP_PORT_NUMBER="8081" \
    TOMCAT_PASSWORD="password" \
    TOMCAT_SHUTDOWN_PORT_NUMBER="8005" \
    TOMCAT_USERNAME="user"

EXPOSE 8080

#USER 1001
ADD target/*.war /opt/bitnami/tomcat/webapps
RUN ["sudo", "chmod", "+x", "/app-entrypoint.sh"]
ENTRYPOINT [ "/app-entrypoint.sh" ]
CMD [ "nami", "start", "--foreground", "tomcat" ]

