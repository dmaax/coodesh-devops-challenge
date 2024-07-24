# Como instalar as dependências do projeto?

As instruções a seguir foram validadas em uma vm Ubuntu 24.04 LTS zerada.

## Atualizando repositórios

```
sudo apt update
```

## Instalando pipx

```
sudo apt install pipx -y
pipx ensurepath
```

## Instalando Ansible e dependências

```
pipx install --include-deps ansible
ansible-galaxy collection install community.docker
```

## Instalando terraform

```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
```

## Instalando awscli

```
sudo apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

## Configurando awscli

Com a conta freetier criada na AWS, [crie uma chave de acesso](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) para usar com a ferramenta [awscli](https://aws.amazon.com/cli/)

```
aws configure
```
