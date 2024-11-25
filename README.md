# Ansible for Kubernetes/OpenShift

## Resources
- https://docs.ansible.com/ansible/latest/collections/kubernetes/core/docsite/scenario_guide.html
- https://github.com/redhatci/ansible-collection-redhatci-ocp
- https://github.com/ahmbas/ansible-ocp-virt/

## Commands

To generate an Assisted Installer draft cluster:

```bash
ansible-galaxy collection install -r requirements.yml
ansible-playbook -i inventory.yml playbooks/assisted-installer.yaml  -e @vars/all.yml -e @vars/secrets.yml
```

Stuff for a custom execution environment for OpenShift/oc:

```bash
ansible-builder build --tag k8s_ee

ansible-navigator run playbooks/playbook.yaml \
  --execution-environment-image k8s_ee \
  --mode stdout \
  --pull-policy missing \
  --container-options='--user=0'

playbook=openshift-install.yaml
ansible-navigator run ${playbook} \
  --execution-environment-image k8s_ee \
  --mode=stdout \
  --pull-policy missing \
  --eev ~/.kube/config:/runner/.kube/config \
  --senv KUBECONFIG=/runner/.kube/config

```