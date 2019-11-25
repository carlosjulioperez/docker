FROM scratch
ADD centos-6-docker.tar.xz /

LABEL org.label-schema.schema-version="1.0" \
    org.label-schema.name="CentOS Base Image" \
    org.label-schema.vendor="CentOS" \
    org.label-schema.license="GPLv2" \
    org.label-schema.build-date="20180804"

EXPOSE 80
EXPOSE 8080

RUN yum -y update && \
yum -y install vim lsof wget tree screen man man-pages postgresql postgresql-server postgresql-contrib

CMD ["/bin/bash"]
