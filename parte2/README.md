# Parte 2 - Infra as Code

## Requisitos Iniciais

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) - Versão >= 2.15.3
- [awscli](https://aws.amazon.com/cli/) - Versão >= 2.13.3
- [Python](https://www.python.org/downloads) - Versão >= 3.9
- [Terraform](https://developer.hashicorp.com/terraform/downloads) - Versão >= 1.5.4

_Por favor instale todos os [requisitos](#requisitos-iniciais), sem eles o projeto não funcionará_.

## Configuração

1. Criar uma conta free tier na [AWS](https://aws.amazon.com/free)
2. Com sua conta da AWS criada, você deve [criar uma chave de acesso](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) para usar com a ferramenta [awscli](https://aws.amazon.com/cli/)
3. Instalar todos os [requisitos iniciais](#requisitos-iniciais)
4. Agora você precisa [configurar a awscli](https://docs.aws.amazon.com/cli/latest/reference/configure/) para usar a chave de acesso criada

```
aws configure
```

## Estrutura do projeto

- `ansible/`: Possui todos os arquivos usados pelo Ansible.
- `terraform/main/`: Possui todos os arquivos usados pelo Terraform.

## Clonando o repositório
```
git clone https://github.com/dmaax/coodesh-devops-challenge.git
cd coodesh-devops-challenge/parte2
```

## Configurando o Terraform

Antes de criar a infraestrutura na AWS será preciso criar uma nova chave ssh para interagir remotamente com o servidor:

```
ssh-keygen -t ed25519 -C seunome@coodesh
```

_Obs: essa chave deve ser salva no diretório padrão do linux (~/.ssh)_

Agora precisamos descobrir nosso endereço IP público para permitir o tráfego na porta 22 (SSH) e na porta 3000 (Grafana) da instância EC2. Para tal é possível usar o site [ipinfo](https://ipinfo.io). Com o IP anotado navegue até [esse arquivo](terraform/main/modules/security_group/main.tf) e altere as linhas 27 e 35 e coloque `seuip/32` no lugar do `0.0.0.0/0` exemplo: `123.234.132.21/32`. Essa configuração permite que só esse endereço IP consiga interagir através do SSH e com a aplicação Grafana dessa instância.

Por fim, navegue até o diretório `terraform/main/` e inicie a construção da infraestrutura:

```
terraform init
terraform plan
terraform apply
```

Para destruir a infraestrutura:
```
terraform destroy
```

## Configurando o Ansible

Depois de tudo criado, vamos configurar o Ansible para instalar alguns softwares e aplicações nessa instância. Lembra da chave ssh que [criamos anteriormente?](#configurando-o-terraform), precisamos configurar o Ansible para usar a mesma. Para isso, edite [esse arquivo](ansible/inventory/production.ini), mude o caminho da chave privada na linha 8, exemplo: `ansible_ssh_private_key_file=~/.ssh/minhachave-coodesh`. Também é necessário editar a linha 3 do mesmo arquivo para colocar o endereço IP público da instância, você consegue esse endereço ao terminar de [criar a infraestrutura com o terraform](#configurando-o-terraform).

### Instalando dependência do Ansible

Alguns roles usados pelo Ansible precisam da coleção `community.docker` para funcionar, para instalar é bem simples:

```
ansible-galaxy collection install community.docker
```

### Executando o playbook

Com tudo configurado e instalado, podemos executar o playbook:

```
cd ansible
ansible-playbook -i inventory/production.ini playbooks/coodesh.yml
```
