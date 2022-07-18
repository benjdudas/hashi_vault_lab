# hashi_vault_lab

**Purpose:**
------
This lab is intended for testing hashicorp vault integration with Ansible Automation Platform

**Control Node Requirements:**
------
- helm (https://github.com/helm/helm/releases)
- ansible 2.9+

**Variable Options:**
------
Kubernetes namespace can be set with the `vault_namespace` variable. By default this is set to `vault-lab`

~~~
ansible-playbook deploy_vault.yml -e "vault_namespace=<my-namespace>"
~~~

**Deploy Vault:**
------
1) Clone repo:
~~~
git pull https://github.com/benjdudas/hashi_vault_lab.git && cd ./hashi_vault_lab
~~~

2) Install required Ansible Collections:
~~~
ansible-galaxy collection install -r ./collections/requirements.yml
~~~

3) Deploy hashicorp vault:
~~~
ansible-playbook deploy_vault.yml
~~~

**Cleanup:**
------
~~~
ansible-playbook delete_vault.yml
~~~
