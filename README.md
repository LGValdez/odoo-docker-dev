# Plug and Play Odoo Docker Dev

- Run multiple odoo instances per container.
- Run old odoo versions on old ubuntu versions.
- Have a dev environment compatible with multiple platforms macOS / Windows.

## How to setup

- Go into the odoo directory inside this repository.
```
cd odoo
```

- Run docker compose unattached.
```
docker-compose up -d
```
- A bunch of things need to be downloaded to build all these images so be patient.

## How to develop

- Connect to your container via a text editor from your preference.

- Create a new folder for your project and move to that directory.
```
mkdir <my_project> && cd <my_project>
```

- Clone the from odoo repository here picking you appropriate version. The following command will clone `v16` in a folder named `<odoo_folder>` of your choice.
```
git clone https://github.com/odoo/odoo --branch 16.0 --depth 1 <odoo_folder>
```

- Create a folder to contain you custom addons.
```
mkdir <custom_addons>
```

- Create an appropriate python virtual environment.

For python 3.x
```
python3 -m venv venv
```

For python 2.7.x
```
virtualenv --python=python2.7 venv 
```

- Activate your venv and install all requirements. Note: This requirements might be on a different folder for odoo enterprise versions.
```
source venv/bin/activate
```
```
pip install -r <odoo_folder>/requirements.txt
```

- Create an odoo.conf file with the following.
```bash
[options]
admin_passwd = <admin_password>
db_host = host.docker.internal
db_port = 5432
db_user = <db_user>
db_password = <db_password>
xmlrpc_port = 8069
addons_path=/home/odoo/<your_project>/<odoo_folder>/addons,/home/odoo/<custom_addons>
# limit_time_cpu = 160000000
# limit_time_real = 170000000
```

- Launch Odoo. Note: If odoo-bin is not present directly under your `<odoo_folder>` copy it from the `<odoo_folder>/setup`.
```
python <odoo_folder>/odoo-bin --conf odoo.conf
```

Odoo will be available on the exposed port for each container. With this setting only one instance per container can run at the time. You can change that by forwarding more ports outside of docker.

## Additional notes
- Addons path may vary when working with enterprise versions.
- Database filtering is important. One suggestion that works well is to directly restrict it by user, so create one superuser in the DB for each odoo project.
```
CREATE USER <db_user> SUPERUSER PASSWORD '<db_password>';
```
- Do not change the `8069` port if using default behavior.

## Why so many containers

Older versions of Odoo use python 2.7.x which is really hard for newer OS systems. Here are some suggestions.

- Ubuntu 18 and python 2.7.x for Odoo v9, v10.
- Ubuntu 20 and python 3.7.x^ for Odoo v12, v13, v14.
- Ubuntu 24 and python 3.8.x^ for Odoo v15, v16, v17.


### Happy Coding!
