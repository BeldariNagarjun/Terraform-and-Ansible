# Terraform-and-Ansible

created multiple instances by using terraform and connected it through Elastic IP address and generated ping massages through ansible.

take Comand Prompt 

take new webpage and type Install terraform choose linux and select amzon linux server copy and paste below comands in comand prompt

sudo yum install -y yum-utils

sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo

sudo yum -y install terraform

mkdir terraform_scripts

cd terraform

create IAM User and give full access of EC2 and create access_key and security_key 

vi provider.tf
provider "aws" {
  access_key = "paste it here"
  secret_key = "paste it here"
  region     = "ap-south-1"
}

esc :wq --press enter


vi main.tf
resource "aws_instance" "node_1" {
  count                  = "1"
  ami                    = "ami-02b49a24cfb95941c"
  instance_type          = "t2.micro"
  key_name               = "Project_Terraform"
  subnet_id              = "subnet-07d4c408a9436e199"
  vpc_security_group_ids = ["sg-099df5061091c610d"]
}
resource "aws_instance" "node_2" {
  count                  = "1"
  ami                    = "ami-02b49a24cfb95941c"
  instance_type          = "t2.micro"
  key_name               = "Project_Terraform"
  subnet_id              = "subnet-07d4c408a9436e199"
  vpc_security_group_ids = ["sg-099df5061091c610d"]
}

esc :wq --press enter


terraform init

terraform fmt

terraform validate

terraform plan

terraform apply


mkdir ansibe

cd ansible

yum install pip

pip install ansible

vi host
[ansible_server]
node_1 ansible_host=192.138.8.117
node_2 ansible_host=192.138.9.42

[all:vars]
ansible_python_interpreter=/usr/bin/python3
esc :wq --press enter

cd .ssh


vi ansible_key
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA13YxqkXXhJBzt8P07jcoeMkqoD2IgQ1Ye14G4j/5FBbWpCui
1VpJwwTOwwm27hwc3dqXYdlf6VbBHBmNiAZgy+4Z+0wzfvpm+gQ5c3T72Syi5Au5
uVbNCh8yili5FacOQZ6xwoIXZgFgvr+fbn2cYKd9TDVIuZIaEiCTDlLcRw6fWNnX
LfSj1J8kriMCf7n/T5iJm/3BixmVZ07ZPjM6Pmo9xNoW7TmHxkSeDJKt1hz7pH1s
efuJSACF3PZ7dXi54KPcXHg+J26vGAUDyP8fDyunVgGzN94vrttULz46Bbov2OU1
qVjffPEpU95K60lVjCsyVU0UD0XbW2XJCD2TvQIDAQABAoIBAHeBaR6mSlmOvYBJ
wgp2sY39FhV2y8W4n0Ed7/eBwCdyW28HfPOVdqAihIQNWVdMZH5xBdIR/W6w3b82
NRgjYYD6+ZI2u8FMJd26hhsR4badWWPfVQ4FpQheMWwmtdHarL+cw7+85DmBviVO
p6FjLl81xvuD+mhjLu6q/qXNM7x8zPMGZX5XIiDyWYPjFc7mDlGBIoj0t2AMdthE
Q+zI5Z/y8nnCKCuRZ/RXuWlyZYzSmxPNWhdCfzesiky3LNj/0FSrFQuWWz0QRsix
hpqGoPckxMJDJ7YZnIjzz5R6N5FqvWLkJQQuThggDWeW1LPMoeWL8TLYAAxF/vTz
NbQYoIkCgYEA9oOsPJnmztHNSFHqxubkBqoxX5kX2xloepKX/yLnmhCJsZ7la7AV
v4A5L6qkB0IaS/3nvVLnMyymgdqSiYwtgtqIDAJMdMk/YH26lVPR4CjxCpDtUYxg
wB2LS0Wt/4ID5QkJTlPowibUHM1sQEJ+b5iI2CnvC/ECTiaf8SqKYNMCgYEA38Ch
38nI86VcTUCJsKyKxoUJ8or3lsW5ygS8vP/Ave95rf1/lBWlyvc2Kut9jY3aqA5O
QiunLAwHTpw4L2DUuF2Ysi1FeOq3kbK5/ep8AAY0VL6Z2pVL3X/Q972Iw1dtADgJ
e/kyvjrCQi203862/3V5NDCgc517WUuTYpjK3y8CgYEAr2Z7G9eJsaj4PrgCrCnH
H7LjVJkSr1PB0k0SF3iXgDi6MIbVyKzOnKa4ieEJuxxep6luxXgCh5gClayWzYXP
MCcb3CeajRJQpPBw3SV51Nxsvc7m/To78RZUcWeP6Zhx+vpWA8SSfeqwzBmiJ4ro
ebD31Y7oxv9iW4cCEM/rC/8CgYBVvUIKOA9p1a6l55obejJ/WdFzAG9ZdhD4aZJN
Ng+MeKx+0InHm/f463v1PGHTEU19YmX4kzOu/Dj8lX4uIYPB1hPCCvj5GbAYA42j
z+uOMtJwuszH5re4e9b+Z8F1YRXipJZ1zAr2vBteMpeBv3t+LmywZAXH58uxbvVe
LcBnfwKBgBg5xaHzOzsn/RoHAAlAyRtUJTbdexTyY6skR157p4G1o7Y+3ALpGtwV
vx6juHHLeD/nUrvnQMycVU7dUL9SAdi/7cZnrAlv2vku5NG5/ztrq1aAGr5cFchK
asRsVgNXWu7QTKqiShfRGRYtusWuWWYHqSx+GnbOGCxnRR2iV4Yt
-----END RSA PRIVATE KEY-----

esc :wq --press enter


ansible all -m ping


ansible all -m ping -i /home/ec2-user/ansible/host

yes

yes


ansible all -m ping -i /home/ec2-user/ansible/host --private-key=/home/ec2-user/.ssh/ansible_key
