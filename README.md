# hashi_vault_lab

**Purpose:**
------
This lab is intended for testing hashicorp vault integration with Ansible Automation Platform

**Control Node Requirements:**
------
- helm (https://github.com/helm/helm/releases)
- oc (https://docs.openshift.com/container-platform/4.6/cli_reference/openshift_cli/getting-started-cli.html)
- ansible 2.9+

**Variable Options:**
------
Kubernetes namespace can be set with the `vault_namespace` variable. By default this is set to the value of `oc whoami | cut -f1 -d"@" + '-' vault-lab`

~~~
ansible-playbook deploy_vault.yml -e "vault_namespace=<my-namespace>"
~~~

**Deploy Vault:**
------
1) Clone repo:
~~~
git clone https://github.com/benjdudas/hashi_vault_lab.git && cd ./hashi_vault_lab
~~~

2) Install required Ansible Collections:
~~~
ansible-galaxy collection install -r ./collections/requirements.yml
~~~

3) Deploy hashicorp vault:
~~~
ansible-playbook deploy_vault.yml
~~~

**Initial Vault Setup After Deployment:**
------
1) Verify installation using: 
~~~
oc get all -n vault-lab
~~~

2) Initialize Vault and save token/unseal keys to a local file `token_seal`:
~~~
oc exec -ti vault-0 -n vault-lab -- vault operator init |tee token_seal
~~~

3) Open Hashicorp Vault UI. To use the command below, json-query must be installed (`sudo dnf install jq`)
~~~
/bin/sh -c 'gio open http://$(oc get route vault-route -n vault-lab -o json | jq -r .spec.host)'
~~~

4) Using 3 of the unseal keys listed in step 2, unseal Vault and login using the "Initial Root Token"

**Cleanup Vault:**
------
~~~
ansible-playbook delete_vault.yml
~~~
