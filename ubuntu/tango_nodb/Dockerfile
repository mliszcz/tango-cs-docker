FROM ubuntu:14.04

# Update the repo info
RUN apt-get update

# Change installation dialogs policy to noninteractive, otherwise
# debconf raises errors: unable to initialize frontend: Dialog
ENV DEBIAN_FRONTEND noninteractive

# Avoid ERROR: invoke-rc.d: policy-rc.d denied execution of start.
RUN sed -i "s/^exit 101$/exit 0/" /usr/sbin/policy-rc.d

# Install base deb packages
RUN apt-get update && apt-get -q install -y --force-yes \
                        apt-transport-https \
                        bind9-host \
                        build-essential \
                        language-pack-en \
                        perl \
                        perl-modules \
                        psmisc \
                        python \
                        python-dev \
                        rsync \
                        software-properties-common

# Remove some packages from the base template
RUN apt-get -y purge postfix

# Install other deb packages
RUN apt-get update && apt-get install -y --force-yes \
                        aptitude \
                        ftp \
                        gawk \
                        gfortran \
                        git-core \
                        language-pack-en-base \
                        libatk1.0-dev \
                        libatlas-base-dev \
                        libboost-python-dev \
                        libcairo2-dev \
                        libevent-dev \
                        libf2c2-dev \
                        libffi-dev \
                        libfontconfig1-dev \
                        libfreetype6-dev \
                        liblapack-dev \
                        libpng12-dev \
                        libpq-dev \
                        libssl0.9.8 \
                        lsof \
                        manpages \
                        man-db \
                        ntpdate \
                        python-cairo-dev \
                        tcpdump \
                        telnet \
                        tzdata \
                        unzip \
                        xauth \
                        zlib1g-dev \
                        && apt-get clean \
                        && rm -rf /var/lib/apt/lists/*

# Add tango ppa for latest tango core
RUN add-apt-repository ppa:lmc-cam-ska/tango
RUN add-apt-repository ppa:lmc-cam-ska/pytango
RUN apt-get update

# Install tango core packages
RUN apt-get install -y tango-common \
                       liblog4tango5v5 \
                       liblog4tango-dev \
                       liblog4tango-doc \
                       libtango-dev \
                       libtango-doc \
                       libtango9 \
                       python-tango
