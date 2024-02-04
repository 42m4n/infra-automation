# Ansible Nmap Playbook

## Overview
This Ansible playbook is designed to automate Nmap scans on target hosts. It utilizes Ansible for orchestration and Nmap for network exploration and security auditing.

## Requirements

- Ansible installed on the control machine.
- Python installed on the target hosts.
- Nmap installed on the control machine (if not available, the playbook can install it).

## Usage

1. Clone this repository to your Ansible control machine:

   bash
   git clone https://github.com/yourusername/ansible-nmap-playbook.git
   cd ansible-nmap-playbook

1.Customize the inventory file ('inventory/hosts.yml') with your target hosts:
[target_hosts]
# Add more hosts as needed
---
2.Create scan.yml in inventory/Group_vars
# path:inventory/group_vars/var/scan.yml

structure 
# basic package list for installation
packages:
- nmap

3.Create roles scan 

4.create task for  Run and Install and Result  Nmap in scan roles:

structure for installation.yml file
# path:roles/scan/tasks/installation.yml

 apt:
    name: "{{ packages }}"
    state: present
    force_apt_get: yes
    update_cache: yes

-----
structure for run.yml file
# path:roles/scan/tasks/run.yml

- name: Run Nmap Scan
  command: "nmap {{ inventory_hostname }}"
  register: nmap_output

- name: Sort Nmap Scan Results
  command: "echo '{{ nmap_output.stdout_lines | join('\n') }}' | sort"
  register: sorted_nmap_output

- name: Display Nmap Scan Results
  debug: var=nmap_output.stdout_lines
# Customize Nmap scan options

nmap_output_dir: "/path/to/nmap/results"
# Customize the output directory for Nmap results

----
5.Run the playbook:

ansible-playbook -i inventory/hosts.yml nmap.playbook.yml
Replace nmap.playbook.yml with the actual name of your playbook file.

Playbook Structure

    nmap-playbook.yml : The main playbook file.
    inventory/hosts.yml: Inventory file containing target hosts.
    group_vars/all/scan.yml: Variable file with customizable options.
    tasks/: Directory containing Ansible tasks.
 

Author

Harimi gharimi.rh@gmail.com

License
This project is licensed under the MIT License - see the LICENSE file for details.

Feel free to customize the content based on your specific needs and project structure. Update the placeholders like `RH`, `Haimi`, `gharimi.rh@gmail.com`, and adjust the directory structure and playbook variables according to your requirements.


