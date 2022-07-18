# hashi_vault_lab


**Control Node Requirements:**
- helm (https://github.com/helm/helm/releases)


**Variable Options:**
------
Kubernetes namespace can be set with the `vault_namespace` variable. By default this is set to `vault-lab`

For Example:
~~~
ansible-playbook deploy_vault.yml -e "vault_namespace=<my-namespace>"
~~~





