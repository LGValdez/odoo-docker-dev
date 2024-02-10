FROM ubuntu:18.04
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get upgrade -y
RUN apt-get install sudo zsh git wget -y
RUN apt-get install python-dateutil python-docutils python-feedparser python-jinja2 \
    python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid \
    python-psycopg2 python-psutil python-babel python-pychart python-pydot \
    python-pyparsing python-reportlab -y
RUN apt-get install python-simplejson python-tz python-unittest2 \
    python-vatnumber python-vobject python-webdav python-werkzeug python-xlwt \
    python-yaml python-zsi poppler-utils python-pip python-pypdf2 python-passlib \
    python-decorator gcc python-dev mc bzr -y
RUN apt-get install python-setuptools python-markupsafe \
    python-reportlab-accel python-zsi python-yaml python-argparse python-openssl \
    python-egenix-mxdatetime python-usb python-serial lptools make python-pydot \
    python-psutil python-paramiko poppler-utils python-pdftools antiword python-requests \
    python-xlsxwriter python-suds python-psycogreen python-ofxparse python-gevent \
    software-properties-common wkhtmltopdf -y
RUN pip install virtualenv
RUN apt-get install postgresql postgresql-contrib -f -y && \
    apt-get install python-psycopg2 libpq-dev libsasl2-dev libldap2-dev libssl-dev \
    libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev libffi-dev -y
RUN apt-get install -y npm && npm install -g less@3.0.4 less-plugin-clean-css
RUN useradd -rm -d /home/odoo -s /bin/zsh -g root -G sudo -u 1001 odoo && \
    usermod -aG sudo odoo && \
    echo "odoo:odoo" | chpasswd
USER odoo
WORKDIR /home/odoo
RUN sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
RUN ["zsh"]