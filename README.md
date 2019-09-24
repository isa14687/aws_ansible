# aws_ansible

利用Ansible在AWS中建立VPC、EC2以及RDS

## Requirements
1. boto
1. boto3
1. botocore
1. python >= 2.6

## Usage
透過以下指令，並輸入密碼執行playbook<br>

    ansible-playbook -i hosts.inventory aws.yaml --ask-vault-pass
    
其中var/vault.yaml 中的內容為透過Ansible中的Ansible Vault進行加密功能，對敏感資料進行加密，aws_access_id以及aws_secret_access_key等
可以透過 --ask-vault-pass，--vault-password-file或者--vault-id指令，指定密碼的位置或是提示使用者輸入密碼

而存取AWS所需要的aws_access_id以及_asw_secret_access_key可依照
[管理IAM使用者的存取金鑰](https://docs.aws.amazon.com/zh_tw/IAM/latest/UserGuide/id_credentials_access-keys.html)建立
，並且將透過 ansible-vault create vault.yaml 自行建立文件

    vault_aws_access_id: "aaaaaaaaaaa"
    vault_aws_secret_access_key: "bbbbbbbbbbbbb"
     
 task/aws_ec2.yaml，中的instance_profile_name需要先在IAM中的Role進行設定，詳細步驟如 [官方文件](https://docs.aws.amazon.com/en_us/AmazonCloudWatch/latest/monitoring/create-iam-roles-for-cloudwatch-agent.html)

    instance_profile_name: CloudWatchAgentServerRole
