# Auto deploy webapp

This Ansible project aims to automate the deployment of a web project developed in PHP using the Wordpress CMS.

## Structure

- auto-deploy-webapp/
    - roles/
        - prepare_db_server/
            - defaults/main.yml
            - handlers/main.yml
            - tasks/main.yml
            - templates/
        - prepare_docker/
            - defaults/main.yml
            - handlers/main.yml
            - tasks/main.yml
            - templates/
        - prepare_http_server/
            - defaults/main.yml
            - handlers/main.yml
            - tasks/main.yml
            - templates/
        - prepare_php/
            - defaults/main.yml
            - handlers/main.yml
            - tasks/main.yml
            - templates/
        - prepare_wordpress/
            - defaults/main.yml
            - files/wordpress-6.4.3-fr_FR.tar.gz
            - tasks/main.yml
            - templates/
    - inventory.yml
    - playbook.yml
    - requirements.txt
- .gitignore
- README.md

## Control node

Before starting, you need to have:

- Python3 (>=3.11)
- pip (>=23.2.1)
- virtual-env

Clone this Ansible project and create a virtual environment at the root of the cloned project:

```bash
python3 -m venv .venv/
```

Activate the venv:

```bash
source .venv/bin/activate
```

Install the required python module into the venv:

```bash
python3 -m pip install -r auto-deploy-webapp/requirements.txt
```

You're now ready to go!

## Roles

### prepare_docker

This role aims to install and configure Docker on the target system. It includes:
- Installation of Docker and Docker Compose
- Configuration of Docker daemon
- Setting up Docker user permissions

### prepare_http_server

This role aims to install and configure the HTTP Server Apache2.

To do this, it is necessary to install the following packages:
- apache2

After installation, some modules will be necessary:
- rewrite
- http2

### prepare_php

This role aims to install the PHP scripting language, compatible with the WordPress CMS.

To do this, it is necessary to install the following packages:
- php8.2
- php8.2-bcmath
- php8.2-bz2
- php8.2-intl
- php8.2-gd
- php8.2-mbstring
- php8.2-mysql
- php8.2-zip
- php8.2-fpm
- php8.2-curl
- php8.2-dom
- php8.2-xml
- php8.2-imagick
- php8.2-soap

### prepare_db_server

This role aims to install a MariaDB database server running on a Docker container, using the official MariaDB image, version 11.2.2.

### prepare_wordpress

This role handles the installation and configuration of WordPress, including:
- Downloading and extracting WordPress
- Configuring WordPress settings
- Setting up the database connection
- Configuring security settings

## Usage

To deploy the project, run the following command from the project root:

```bash
ansible-playbook -i auto-deploy-webapp/inventory.yml auto-deploy-webapp/playbook.yml
```

## Security Considerations

- All sensitive information should be stored in the `ansible/vault.yml` file
- The vault password should be kept secure and not committed to the repository
- Regular security updates should be applied to all components
