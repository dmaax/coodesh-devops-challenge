# Parte 1 - Configuração do Servidor

_Importante: Para a execução seguintes passos será assumido que a região do console será us_east_1 para padronizar as urls usadas._

## Criando uma VPC, sub-rede, internet gateway e route tables

Para criar a VPC é necessário:

1. Acessar o [console](https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1)
2. Acessar a [página de VPC](https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#Home:)
3. Clicar em Criar VPC
4. Selecionar Somente VPC
5. Preencher os dados:
- tag de nome (coodesh-vpc)
- CIDR IPv4 (10.0.0.0/16)
6. Clicar em Criar VPC

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

_Gifs de exemplo:_

<!-- TODO: Add gifs... -->

## Configurando um grupo de segurança na AWS

Para criar esse grupo de segurança é preciso:

1. Acessar o [console](https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1)
2. Acessar a [página do EC2](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Home:)
3. Navegar até a [paǵina de grupos de segurança](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#SecurityGroups:)
4. Clicar em Criar grupo de segurança
5. Preencher os dados:
- Nome
- Descrição
6. Alterar a VPC para a que foi criada anteriormente (coodesh-vpc)
7. Adcionar regras de entrada para permitir SSH, HTTP e HTTPS

## Configurando redes para o Servidor

## Criar a instância EC2 (Servidor Web)

## Instalando softwares adicionais

## Instalando NGINX

1. Configurar grupo de segurança na AWS
2. Configuração da redes para o Servidor
3. Configurar um servidor AWS (recomenda-se o freetier) executando uma versão Ubuntu LTS.
4. Instalar e configurar qualquer software que você recomendaria em uma configuração de servidor padrão sob as perspectivas de segurança, desempenho, backup e monitorização.
5. Instalar e configurar o nginx para servir uma página web HTML estática.