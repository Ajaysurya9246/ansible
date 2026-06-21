## 🔧 What This Covers

**1. OS Patch Management (Multi-Distro)**
- `centos.yml` — Updates all packages on RHEL-based servers via `yum`, checks if a reboot is required using `needs-restarting -r`, and reboots only when necessary.
- `ubuntu.yml` — Updates packages on Debian-based servers via `apt`, checks `/var/run/reboot-required`, and conditionally reboots based on OS family detection (`ansible_facts['os_family']`).

**2. Apache (httpd) Role**
- Installs httpd package
- Deploys a templated `index.html` using Jinja2 (`index.html.j2`)
- Uses a handler to restart the service only when the template changes — avoids unnecessary restarts

**3. Nginx Deployment**
- Installs and starts the Nginx service on web servers, with `enabled: yes` for persistence across reboots

**4. File Management**
- `copy.yml` / `ssh.yaml` — Secure file copy tasks with explicit ownership (`owner`, `group`) and permission (`mode`) control, used for config file deployment

## 🛠️ Tech Stack

Ansible · YAML · Jinja2 · Linux (RHEL/CentOS, Ubuntu) · Apache (httpd) · Nginx · SSH

## 🚀 How to Run

```bash
ansible-playbook -i hosts centos.yml --check    # dry run
ansible-playbook -i hosts centos.yml            # apply
ansible-playbook -i hosts httpd/tasks/main.yml
```

## 📌 Environment

Built and tested on a home lab — Ansible control node (CentOS Stream 10) managing remote nodes (Rocky Linux, Ubuntu) over SSH key-based authentication.
