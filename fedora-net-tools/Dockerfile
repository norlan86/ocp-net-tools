FROM registry.redhat.io/rhel8/support-tools:8.7-13
LABEL description="This is a custom httpd container image"
MAINTAINER Norlan Suarez <nsuarez@redhat.com>

ENV PORT 8080
ENV LogLevel "info"

RUN yum repolist
RUN yum install -y httpd && yum clean all

RUN sed -ri -e "/^Listen 80/c\Listen ${PORT}" /etc/httpd/conf/httpd.conf && \
sed -ri -e "/^#ServerName/c\ServerName 127.0.0.1" /etc/httpd/conf/httpd.conf && \
chown -R apache:apache /etc/httpd/logs/ && \
chown -R apache:apache /run/httpd/
RUN echo "Hello from Containerfile" > /var/www/html/index.html

EXPOSE ${PORT}

ENTRYPOINT ["/usr/sbin/httpd"]
CMD ["-D", "FOREGROUND"]
