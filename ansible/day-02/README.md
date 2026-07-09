Ad-hoc Commands
Ad-hoc Commands are commands which can be run individually to perform quick fixes. 
These ad-hoc Commands are not used for Configuration Management and deployment, because these Commands are of One time usage. 

-b = sudo 

su - ansible
ansible all -a "touch rajputfile"
ansible all -a "touch rajputfile"

There is no idempotency.

ansible demo -a "yum install httpd -y"
need root privilages
ansible demo -a "sudo yum install httpd -y"
check: which httpd

