# https://github.com/CentOS/CentOS-Dockerfiles/blob/master/postgres/centos6/Dockerfile
# https://www.andreagrandi.it/2015/02/21/how-to-create-a-docker-image-for-postgresql-and-persist-data/
# https://serverfault.com/questions/720967/how-to-run-postgresql-on-centos-within-docker

FROM centos:centos6
MAINTAINER The CentOS Project <cloud-ops@centos.org>

RUN yum -y update; yum clean all
RUN yum -y install epel-release; yum clean all
RUN yum -y install vim wget tree postgresql postgresql-server postgresql-contrib supervisor; yum clean all
RUN yum -y install httpd perl-DBI perl-DBD-Pg mod_perl perl-DBIx-Simple tetex tetex-fonts tetex-dvips tetex-latex ghostscript lynx; yum clean all
RUN yum -y install java-1.7.0-openjdk-devel.x86_64; yum clean all

ADD ./postgresql-setup /usr/bin/postgresql-setup
ADD ./postgres_user.sh /postgres_user.sh
ADD ./supervisord.conf /etc/supervisord.conf
ADD ./start_postgres.sh /start_postgres.sh

RUN chmod +x /usr/bin/postgresql-setup
RUN chmod +x /start_postgres.sh
RUN chmod +x /postgres_user.sh

RUN /usr/bin/postgresql-setup initdb

ADD ./postgresql.conf /var/lib/pgsql/data/postgresql.conf

RUN chown -v postgres.postgres /var/lib/pgsql/data/postgresql.conf

RUN echo "host    all             all             0.0.0.0/0               md5" >> /var/lib/pgsql/data/pg_hba.conf

RUN /postgres_user.sh

EXPOSE 80
EXPOSE 8080
EXPOSE 5432

#CMD ["/bin/bash"]
CMD ["/bin/bash", "/start_postgres.sh"]
