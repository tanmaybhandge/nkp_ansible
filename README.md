NKP Ansible Role
================

An Ansible role to automate the deployment of a Nutanix Kubernetes Platform (NKP) management cluster on a Nutanix environment.


Features
--------
This role performs the following tasks:

1. Image Validation & Download
   Checks if the NKP Rocky Linux image is available in Nutanix Prism Central.

2. Downloads the image if not present.
   Bastion VM Deployment

3. Deploys a new bastion VM on the target Nutanix cluster using the NKP Rocky image.
   Configures the bastion VM with required dependencies using cloud-init.

4. NKP Binaries Setup
   Downloads and extracts the required NKP binaries of the specified version on the bastion VM.

5. NKP Management Cluster Deployment
   Creates the NKP management cluster using settings defined in the role variables.

6. Cluster Access Information
   Once the cluster is successfully created, the role prints the dashboard URL along with credentials for login.


Variables:
----------
# vars file for nkp_deploy, all are mandatory
image_url:                                        # ddownload url for NKP rocky node OS image
SSH_PUBLIC_KEY:                                   # SSH public key of ansible control node
nkp_url:                                          # nkp binary download link for linux
NKP_VERSION:                                      # NKP version to install
CLUSTER_NAME:                                     # NKP cluster name. When using NKP Pro/Ultimate, this name is used to generate the license key
NUTANIX_USER:                                     # Prism Central username
NUTANIX_PASSWORD:                                 # Keep the password enclosed between single quotes - Ex: 'password'
NUTANIX_ENDPOINT:                                 # Prism Central IP address
NUTANIX_PORT:                                     # Prism Central port (default: 9440)
LB_IP_RANGE:                                      # Load balancer IP range - Ex: 10.42.236.204-10.42.236.204
CONTROL_PLANE_ENDPOINT_IP:                        # Kubernetes VIP. Must be in the same subnet as the VMs - Ex: 10.42.236.203
NUTANIX_MACHINE_TEMPLATE_IMAGE_NAME:              # Update with the NKP Rocky image name
NUTANIX_PRISM_ELEMENT_CLUSTER_NAME:               # Prism Element cluster name - Ex: PHX-POC207
NUTANIX_SUBNET_NAME:                              # Ex: primary
NUTANIX_STORAGE_CONTAINER_NAME:                   # Change to your preferred Prism storage container
REGISTRY_MIRROR_URL:                              # Required on Nutanix HPOC


Usage:
------
---
- hosts: all
  gather_facts: no
  roles:
    - nkp_deploy
  environment:
    ANSIBLE_HOST_KEY_CHECKING: "False"


