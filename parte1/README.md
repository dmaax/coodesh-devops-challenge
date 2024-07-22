# Parte 1 - Configuração do Servidor

_Importante: Para a execução dos seguintes passos será assumido que a região do console será us-east-1 para padronizar as urls usadas._

## Criando uma VPC, sub-rede, gateway da internet e tabela de rotas

Para criar a VPC é necessário:

1. Acessar o [console](https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1)
2. Acessar a [página de VPC](https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#Home:)
3. Clicar em Criar VPC
4. Selecionar Somente VPC
5. Preencher os dados:
- tag de nome (coodesh-vpc)
- CIDR IPv4 (10.0.0.0/16)
6. Clicar em Criar VPC

![](https://github.com/dmaax/coodesh-devops-challenge/blob/main/gifs/vpc.gif)

Para criar a sub-rede é necessário:

1. Acessar o [console](https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1)
2. Acessar a [página de VPC](https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#Home:)
3. Clicar em Sub-redes
4. Preencher os dados:
- ID da VPC (coodesh-vpc)
- Nome da sub-rede (coodesh-vpc-subnet)
- Zona de disponibilidade (us-east-1a)
- Bloco CIDR IPv4 da sub-rede (10.0.0.0/24)
6. Clicar em Criar sub-rede

<!-- TODO: Add gif... -->

Para criar o gateway da internet é preciso:

1. Acessar o [console](https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1)
2. Acessar a [página de VPC](https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#Home:)
3. Clicar em Gateways da Internet
4. Clicar em Criar gateway da Internet
5. Preencher os dados:
- Tag de nome (coodesh-ig)
6. Clicar em Criar gateway da Internet

<!-- TODO: Add gif... -->

Para aplicar o gateway da internet é necessário:

1. Acessar a [página de VPC](https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#Home:)
2. Clicar em Gateways da Internet
3. Selecionar o Gateway da Internet (coodesh-ig)
4. Clicar em Ações e Associar à VPC (coodesh-vpc)

<!-- TODO: Add gif... -->

Para atualizar a tabela de rotas é preciso:

1. Acessar a [página de VPC](https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#Home:)
2. Clicar em Tabelas de rotas
3. Selecionar a tabela da vpc coodesh-vpc
4. Clicar em Rotas
5. Clicar em Editar rotas
6. Clicar em Adicionar rota
7. Colocar a rota 0.0.0.0/0 apontando para o gateway da internet

<!-- TODO: Add gif... -->

_Gifs de exemplo:_

<!-- TODO: Add gifs... -->

## Configurando um grupo de segurança na AWS

Para criar esse grupo de segurança é preciso:

1. Acessar o [console](https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1)
2. Acessar a [página do EC2](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Home:)
3. Navegar até a [paǵina de grupos de segurança](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#SecurityGroups:)
4. Clicar em Criar grupo de segurança
5. Preencher os dados:
- Nome (coodesh-sg)
- Descrição
6. Alterar a VPC para a que foi criada anteriormente (coodesh-vpc)
7. Adcionar regras de entrada para permitir SSH, HTTP e HTTPS

<!-- TODO: Add gif... -->

## Criar a instância EC2 (Servidor Web)

Para criar a instância EC2 será necessário:

1. Acessar o [console](https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1)
2. Acessar a [página do EC2](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Home:)
3. Clicar em Executar instância
4. Preencher os dados:
- Nome
5. Selecionar a imagem do Ubuntu Server LTS
6. Escolher Criar novo par de chaves (ED25519) com o nome coodesh-keys
7. Clicar em Criar par de chaves (e baixar/salvar)
8. Editar Configurações de rede para a VPC criada (coodesh-vpc)
9. Habilitar Atribuir IP público automaticamente
10. Selecionar grupo de segurança existente (coodesh-sg)
11. Executar instância

<!-- TODO: Add gif... -->

## Instalando softwares adicionais

### Acessar a instância através do SSH
`ssh -i ~/.ssh/coodesh-keys.pem ubuntu@coodesh-vm-publicip`

### Atualizar os pacotes e instalar Docker
```
sudo apt update && sudo apt upgrade -y
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
sudo usermod -aG docker ubuntu
logout
```

<!-- TODO: Add gif... -->

### Fazer o deploy do prometheus e grafana com docker compose
_Copiar o arquivo prometheus.tar.gz para a máquina virtual_
```
scp -v -i ~/.ssh/coodesh-keys.pem ./files/prometheus.tar.gz ubuntu@coodesh-vm-publicip:~
```

<!-- TODO: Add gif... -->

_Criar a pasta containers com os containers necessários_
```
ssh -i ~/.ssh/coodesh-keys.pem ubuntu@coodesh-vm-publicip
mkdir containers
mv ~/prometheus.tar.gz containers/
cd containers
tar -xzvf prometheus.tar.gz
rm prometheus.tar.gz
cd prometheus
docker compose pull
docker network create grafana-network
docker volume create grafana-storage
docker compose up -d
```

<!-- TODO: Add gif... -->

_Editar as regras de entrada (security group) para permitir expor o grafana_

<!-- TODO: Add gif... -->

### Instalar e configurar o fail2ban
```
sudo apt update && sudo apt install fail2ban -y
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
# Configurar o fail2ban através do arquivo jail.local
sudo vim /etc/fail2ban/jail.local
```

<!-- TODO: Add gif... -->

### Instalar e configurar unattended-upgrades
```
sudo apt update && sudo apt install unattended-upgrades
sudo systemctl status unattended-upgrades
sudo vim /etc/apt/apt.conf.d/50unattended-upgrades
sudo vim /etc/apt/apt.conf.d/20auto-upgrades
sudo systemctl restart unattended-upgrades.service
sudo unattended-upgrades --dry-run --debug
```

<!-- TODO: Add gif... -->

## Instalando NGINX
```
sudo apt install nginx -y
sudo vim /etc/nginx/nginx.conf
sudo systemctl restart nginx
sudo systemctl status nginx
sudo mv /var/www/html/index.nginx-debian.html /var/www/html/oldnginx.html
sudo vim /var/www/html/index.html
curl http://localhost
```

<!-- TODO: Add gif... -->

1. Configurar grupo de segurança na AWS
2. Configuração da redes para o Servidor
3. Configurar um servidor AWS (recomenda-se o freetier) executando uma versão Ubuntu LTS.
4. Instalar e configurar qualquer software que você recomendaria em uma configuração de servidor padrão sob as perspectivas de segurança, desempenho, backup e monitorização.
5. Instalar e configurar o nginx para servir uma página web HTML estática.