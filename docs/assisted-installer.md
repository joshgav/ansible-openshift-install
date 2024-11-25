# Assisted Installer

- Use collection from <https://github.com/rhpds/assisted_installer>. E.g. add to requirements.yml:

```yaml
- name: rhpds.install_openshift
  type: git
  source: https://github.com/rhpds/assisted_installer
```

- Update secrets in `vars/secrets.yaml` with pull secret, offline token and SSH public key.
  - Get pull secret and offline token from <https://console.redhat.com/openshift/downloads>
  - Note that it may be necessary to format the pull secret differently, following are a couple examples of how to do this:

```yaml
pull_secret_path: "/tmp/pull-secret.txt"
pull_secret: "{{ lookup('ansible.builtin.file', pull_secret_path) | to_json }}"

pull_secret_raw: ""{\"auths\":{\"cloud.openshift.com\":{\"auth\":\"b3BlbnNoaWZ0LXJl...."
pull_secret: "{{ pull_secret_raw | to_json }}"
```

- Generate an Assisted Installer draft cluster and output the ISO download URL:

```bash
ansible-galaxy collection install -r requirements.yml
ansible-playbook -i inventory.yml playbooks/assisted-installer.yaml  -e @vars/all.yml -e @vars/secrets.yml
```
