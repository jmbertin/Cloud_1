# Cloud_1

Welcome to the Cloud_1 project. It's a project undertaken as part of the 42 school curriculum, a minimal introduction to cloud management.
This project aims to deploy WordPress sites simultaneously on several servers, in the cloud, using Ansible.

----

## Prerequisites

**Install Docker**
````
sudo apt-get install -y ca-certificates gnupg
sudo install -y -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo \
"deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
"$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
````

**Install Ansible**
````
sudo apt install ansible
ansible-galaxy collection install community.general
````

**Make a vault**

To store sensitive information securely, create an Ansible vault named secret.yml.
````
ansible-vault create secret.yml
````

In the vault, include the following mandatory content:
````
vault_ansible_user: USERNAME_FOR_SSH
vault_ansible_ssh_pass: PASSWORD_FOR_SSH
vault_ansible_become_pass: PASSWORD_FOR_ANSIBLE_TO_EXECUTE_ROOT
vault_ansible_ssh_port: SSH_PORT
vault_WORDPRESS_ADMIN: USERNAME_ADMIN_WORPRESS
vault_WORDPRESS_MAIL: MAIL_ADMIN_WORPRESS
vault_WORDPRESS: wordpress
vault_WORDPRESS_DB_HOST: db:3306
vault_PMA_HOST: db
````

**Edit a vault**
````
ansible-vault edit secret.yml
````

**Edit Inventory**

Edit your inventory file and specify the IP addresses for your servers:
````
server1 WORDPRESS_HTTP_PORT=8081 PHPMYADMIN_HTTP_PORT=9091 ansible_host=XXX.XXX.XXX.XXX ansible_ssh_port=2201
server2 WORDPRESS_HTTP_PORT=8082 PHPMYADMIN_HTTP_PORT=9092 ansible_host=XXX.XXX.XXX.XXX ansible_ssh_port=2202
````

----

## Launch

To execute the setup, run the following Ansible playbook command:
````
ansible-playbook -i inventory script-ansible.yaml --ask-vault-pass
````

**You can see the details of the configuration and deployment steps in the script-ansible.yaml playbook**

----

## Contribution
If you encounter any bugs or wish to add features, please feel free to open an issue or submit a pull request.

----
