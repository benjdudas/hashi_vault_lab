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

**Usage:**
------
1) Verify installation using: `oc get all -n vault-lab`
2) Initialize Vault and save token/unseal keys to a local file `token_seal`:
~~~
# oc exec -ti vault-0 -n vault-lab -- vault operator init |tee token_seal
~~~
3) Open Hashicorp Vault UI. Route information can be retrieved from `oc get route vault-route -n vault-lab`
~~~
# gio open http://$(oc get route vault-route -n vault-lab -o json | jq -r .spec.host)
~~~

**Cleanup:**
------
~~~
ansible-playbook delete_vault.yml
~~~
