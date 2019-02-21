FROM tango_nodb

# Update the repo info
RUN apt-get update

# Install and configure supervisor
RUN apt-get install -y supervisor=3.0b2-1
RUN mkdir -p /var/log/supervisor

# Change installation dialogs policy to noninteractive, otherwise
# debconf raises errors: unable to initialize frontend: Dialog
ENV DEBIAN_FRONTEND noninteractive

# Avoid ERROR: invoke-rc.d: policy-rc.d denied execution of start.
RUN sed -i "s/^exit 101$/exit 0/" /usr/sbin/policy-rc.d

RUN apt-get install -y  mysql-client-core-5.6 \
                       mysql-client-5.6 \
                       mysql-server-5.6

# Start mysql & install tango database packages
RUN service mysql start && apt-get install -y \
                       tango-accesscontrol \
                       tango-db \
                       tango-starter \
                       tango-test

# Expose connection for TANGO DB
ENV ORB_PORT=10000
ENV TANGO_HOST=127.0.0.1:${ORB_PORT}
EXPOSE ${ORB_PORT}

# Configure supervisord
COPY resources/supervisord.conf /etc/supervisor/conf.d/
RUN mkdir /var/tmp/supervisord.child

# Start supervisor as deamon
CMD ["/usr/bin/supervisord", "--configuration", "/etc/supervisor/supervisord.conf"]
