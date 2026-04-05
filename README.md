# Ansible Experimentation

Ansible and terraform are considered as tools enabling infrastructure engineers on IaC, **Infrastructure as Code** by leveraging SSH connectivity. Running on Python, ability to connect throuhg SSH provides you with lots of possibilities to manage the target host. The approach is about having everything as code.


> ┌────────────────────────────────────────────────────────┐
> │                   CONTROL NODE (The Hub)               │
> │                                                        │
> │  ┌──────────────┐     ┌─────────────┐      ┌────────┐  │
> │  │  Playbooks   │   + │  Inventory  │ ───▶ │ Engine │  │
> │  └──────────────┘     └─────────────┘      └────────┘  │
> └──────────────────────────────┬─────────────────────────┘
>                                │
>                        (SSH / WinRM Push)
>                                │
>          ______________________V______________________
>         │                      │                      │
> ┌───────┴───────┐      ┌───────┴───────┐      ┌───────┴───────┐
> │  Managed Node │      │  Managed Node │      │  Managed Node │
> │     (Web)     │      │      (DB)     │      │     (App)     │
> └───────────────┘      └───────────────┘      └───────────────┘
>

## Terms

- **Control Node** The machine where Ansible is installed. You run commands and playbooks from here.
- **Managed Nodes** The network devices or servers you are managing. They do not require an Ansible agent.
- **Inventory** A file (usually hosts.ini or hosts.yml) that lists the IP addresses or hostnames.
- **Modules** The "tools" in the toolkit to do a specific work.
- **Playbooks**	YAML files that express configurations, deployment, and orchestration. 

## What you can achieve using Ansible

- **Idenpodency** running the same playbook again should not create any harm!
- **Predictability** With having everyhthing as code you expect the same result everytime
- **Scalability** You can easily extend the number of target hosts

## Getting Started

Considering running ansible playbooks from Control Node, the control Node itself requires packages and insttallations
 which makes the activity a bit risky when it comes to shared environments. The approved solution from ansible is hav
ing Ansible EE, **Execution Environments** where you can ensure that there is no dependency class on control Node.

Installation could be achieved using the following command. That means that ansible requires Python for installation and executiuon.

```
sudo dnf install -y podman python3 python3-pip
pip3 install ansible-navigator
pip3 install ansible-builder
pip3 install ansible

ansible-navigator --version
ansible-builder --version

```

## Project Files

### Inventory

Invertories define which target hosts you would like to manage. You can specify inventory files both in YAML and INI format. 

### Playbooks

- **Playbooks** define how do would like to manage nodes in the inventory. It contains a set of tasks to be executed from top to bottom to achieve the overall goal.
- **Play** An ordered list of tasks that maps to managed nodes in an inventory.
- **Task** A reference to a single module that defines the operations that Ansible performs.
- **Module** A unit of code or binary that Ansible runs on managed nodes. Ansible modules are grouped in collections with a Fully Qualified Collection Name (FQCN) for each module.
- **Plugins** Exntension for Ansible

## Ansible Execution Environments

Considering running ansible playbooks from Control Node, the control Node itself requires packages and insttallations which makes the activity a bit risky when it comes to shared environments. The approved solution from ansible is having Ansible EE, **Execution Environments** where you can ensure that there is no dependency class on control Node.

## Running Playbooks

```
ansible-inventory -i inventory.yaml --list
ansible raspberrypi -m ping -i inventory.yaml
ansible-playbook -i inventory.ini playbook.yaml
```


## More Info

| Technology | Link |
|------------|------|
| Ansible    | https://docs.ansible.com |



