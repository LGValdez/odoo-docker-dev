FROM ubuntu:20.04
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get upgrade -y
RUN apt-get install sudo zsh git wget -y
RUN apt-get install python3 python3-pip build-essential python3-dev \
    python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev \
    libsasl2-dev python3-setuptools node-less libjpeg-dev gdebi -y
RUN apt-get install libpq-dev python-dev libxml2-dev libxslt1-dev \ 
    libldap2-dev libsasl2-dev libffi-dev wkhtmltopdf -y
RUN apt-get install postgresql postgresql-contrib -f -y
RUN useradd -rm -d /home/odoo -s /bin/zsh -g root -G sudo -u 1001 odoo && \
    usermod -aG sudo odoo && \
    echo "odoo:odoo" | chpasswd
USER odoo
WORKDIR /home/odoo
RUN sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
RUN ["zsh"]
