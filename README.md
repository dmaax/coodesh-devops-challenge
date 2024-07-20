<p align="center">
    <h1 align="center">Infra Challenge 20240202 - Coodesh</h1>
</p>

<p align="center">
  <a aria-label="Ansible version" href="https://www.ansible.com/">
    <img src="https://img.shields.io/badge/v2.15.3-000.svg?logo=Ansible&labelColor=000&style=for-the-badge">
  </a>
  <a aria-label="awscli version" href="https://aws.amazon.com/cli/">
    <img src="https://img.shields.io/badge/2.13.3-000?style=for-the-badge&logo=amazonwebservices&logoColor=white">
  </a>
  <a aria-label="Python version" href="https://www.python.org/">
    <img alt="" src="https://img.shields.io/badge/v3.9-000.svg?logo=python&style=for-the-badge">
  </a>
  <a aria-label="Terraform version" href="https://www.terraform.io/">
    <img alt="" src="https://img.shields.io/badge/v1.5.4-000.svg?logo=terraform&logoColor=7B42BC&style=for-the-badge">
  </a>
</p>

## Descrição
Esse repositório possui códigos para configurar de forma declarativa uma infraestrutura básica na AWS (EC2), bem como um servidor Web.

## Requisitos Iniciais

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) - Versão >= 2.15.3
- [awscli](https://aws.amazon.com/cli/) - Versão >= 2.13.3
- [Python](https://www.python.org/downloads) - Versão >= 3.9
- [Terraform](https://developer.hashicorp.com/terraform/downloads) - Versão >= 1.5.4

## Configuração

1. Criar uma conta free tier na [AWS](https://aws.amazon.com/free)
2. Com sua conta da AWS criada, você deve [criar uma chave de acesso](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) para usar com a ferramenta [awscli](https://aws.amazon.com/cli/)
3. Instalar todos os [requisitos iniciais](#requisitos-iniciais)
4. Agora você precisa [configurar a awscli](https://docs.aws.amazon.com/cli/latest/reference/configure/) para usar a chave de acesso criada

