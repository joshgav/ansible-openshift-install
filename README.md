# Ansible for Kubernetes/OpenShift

## Kubernetes Collection
- https://docs.ansible.com/ansible/latest/collections/kubernetes/core/docsite/scenario_guide.html
- https://github.com/redhatci/ansible-collection-redhatci-ocp

## Commands

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