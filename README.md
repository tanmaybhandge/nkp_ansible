# Ansible role to deploy NKP management cluster on Nutanix

## Overview
This role automates the deployment of a Nutanix Kubernetes Platform (NKP) management cluster 

## Tasks Performed

### 1. Image Validation & Download Checks
- Verifies if the NKP Rocky Linux image is available in Nutanix Prism Central.
- Downloads the image if it is not present.

### 2. Bastion VM Deployment
- Deploys a new bastion VM on the target Nutanix cluster using the NKP Rocky Linux image.
- Configures the bastion VM with required dependencies using cloud-init.

### 3. NKP Binaries Setup
- Downloads and extracts the required NKP binaries for the specified version on the bastion VM.

### 4. NKP Management Cluster Deployment
- Creates the NKP management cluster using settings defined in the role variables.

### 5. Cluster Access Information
- Once the cluster is successfully created, the role prints the dashboard URL along with credentials for login.

## Usage
Below is a sample playbook file to use this ansible role

```yaml
---
- hosts: all
  gather_facts: no
  roles:
    - nkp_deploy
  environment:
    ANSIBLE_HOST_KEY_CHECKING: "False"
  vars:
    image_url: ""  # ddownload url for NKP rocky node OS image
    SSH_PUBLIC_KEY: ""  # SSH public key of ansible control node
    nkp_url: ""  # nkp binary download link for linux
    NKP_VERSION: ""  # NKP version to install
    CLUSTER_NAME: ""  # NKP cluster name
    NUTANIX_USER: ""  # Prism Central username
    NUTANIX_PASSWORD: ''  # Keep the password enclosed between single quotes
    NUTANIX_ENDPOINT: ""  # Prism Central IP address
    NUTANIX_PORT: "9440"  # Prism Central port
    LB_IP_RANGE: ""  # Load balancer IP range
    CONTROL_PLANE_ENDPOINT_IP: ""  # Kubernetes VIP
    NUTANIX_MACHINE_TEMPLATE_IMAGE_NAME: ""  # NKP Rocky image name
    NUTANIX_PRISM_ELEMENT_CLUSTER_NAME: ""  # Prism Element cluster name
    NUTANIX_SUBNET_NAME: ""  # Ex: primary
    NUTANIX_STORAGE_CONTAINER_NAME: ""  # Prism storage container
    REGISTRY_MIRROR_URL: ""  # Required on Nutanix HPOC

```
## License
MIT
