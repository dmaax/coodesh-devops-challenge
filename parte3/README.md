# Parte 3 – Continuous Delivery

A pipeline pode ser visualizada [nesse arquivo](../diagramas/devops-flow.drawio.png). [A pipeline](../.github/workflows/main.yml) consiste em aguardar um novo commit na branch main do repositório, com esse novo commit é disparado um checkout no código para pegar a última versão do mesmo, depois é configurado as credenciais da AWS para poder subir a infraestrutura na AWS.

Depois, é configurado o terraform para criar a infraestrutura (são executados os comandos de init, plan e apply). O próximo passo é conseguir o endereço IP público da instância EC2 criada, isso será usado nos próximos passos para configurar o SSH e o Ansible.

Após isso, é configurado o Python para o funcionamento do Ansible. O Ansible é instalado logo em seguida e a chave ssh privada é configurada no worker. Quase finalizando, é adicionado o host da instância no arquivo known_hosts.

Por último o [playbook](../parte2/ansible/playbooks/coodesh.yml) é executado.

Aqui estão os passos em ordem:

1. Checkout Code
2. Configure AWS Credentials
3. Setup Terraform
4. Terraform Init
5. Terraform Apply
6. Get Instance Public IP
7. Setup Python
8. Install Ansible
9. Install SSH Key
10. Adding Known Hosts
11. Run Ansible Playbook

_Atualmente a parte de automação do Ansible não está funcionando, apenas a criação da infraestrutura com o Terraform._
