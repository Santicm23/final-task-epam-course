# Installation steps

## Apply Terraform Configuration
```bash
terraform apply -auto-approve -var-file="<environment>.tfvars"
```

## Connect to the Bastion Host and forward SSH Agent
```bash
ssh -A -i <path-to-private-key> ubuntu@<bastion-host-ip>
```

## Install Ansible on the Bastion Host
```bash
sudo apt update
sudo apt install -y ansible
```
