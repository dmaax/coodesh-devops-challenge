# Parte 2 - Infra as Code

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