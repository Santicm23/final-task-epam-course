# Installation steps

## Select workspace
```bash
cd terraform
terraform workspace select <environment>
```

## Apply Terraform Configuration
```bash
terraform apply -auto-approve -var-file="<environment>.tfvars"
```

## Connect to the Bastion Host and forward SSH Agent and transfer aws.env file for AWS credentials
```bash
cd ..
eval "$(ssh-agent)"
ssh-add ./secrets/ssh-keypair.pem
scp ./secrets/aws.env ubuntu@<bastion-host-public-ip>:~
scp ./secrets/db.env ubuntu@<bastion-host-public-ip>:~
scp ./secrets/ui.env ubuntu@<bastion-host-public-ip>:~
ssh -A ubuntu@<bastion-host-public-ip>
```

## Edit the db.env, and ui.env files on the Bastion Host to set the correct values.
```bash
set -a && source aws.env && source db.env && source ui.env && set +a
```

## Clone Ansible playbook repository
```bash
git clone https://github.com/Santicm23/final-task-epam-course-ansible.git
cd final-task-epam-course-ansible
```

## Run the install script to set up Ansible
```bash
./installation.sh
```
```bash
source ~/.bashrc
```

## Verify Ansible Inventory
```bash
ansible-inventory -i inventory/<environment>.aws_ec2.yml --graph
```

## Run Ansible Playbook to install dependencies
```bash
ansible-playbook -i inventory/<environment>.aws_ec2.yml ./playbooks/dependencies.yml
```
