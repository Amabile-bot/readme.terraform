# readme.terraform
# Infraestrutura AWS com Terraform

## Descrição

Este projeto utiliza o Terraform para provisionar uma infraestrutura básica na AWS, incluindo:

- **VPC** (Virtual Private Cloud) com uma subnet pública.
- **Internet Gateway** para acesso externo.
- **Tabela de Rotas** associada à subnet.
- **Grupo de Segurança** permitindo conexões SSH (porta 22).
- **Par de Chaves SSH** para acesso à instância.
- **Instância EC2** rodando Debian 12, com **Nginx** instalado automaticamente.

## Estrutura do Projeto

```
/
|-- main.tf  # Arquivo principal do Terraform
|-- README.md  # Documentação do projeto
```

## Recursos Criados

### 1. Configuração Inicial

- Define a região da AWS (`us-east-1`).
- Declara variáveis dinâmicas para personalização do projeto.

### 2. Rede

- **VPC:** Criada com o bloco `10.0.0.0/16`.
- **Subnet:** Criada dentro da VPC (`10.0.1.0/24`).
- **Internet Gateway:** Permite conexões externas.
- **Tabela de Rotas:** Direciona tráfego externo através do Internet Gateway.

### 3. Segurança

- **Grupo de Segurança:**
  - Permite conexão SSH (porta 22) a partir de IPs específicos (evitando `0.0.0.0/0`).
  - Permite todo o tráfego de saída.

### 4. Instância EC2

- Utiliza a imagem Debian 12 mais recente.
- Tipo da instância: `t2.micro` (grátis no AWS Free Tier).
- **Automatiza a instalação do Nginx** via `user_data`.
- Associa um IP público para acesso remoto.

## Melhorias Implementadas

- **Restrito o acesso SSH** apenas a IPs específicos para maior segurança.
- **Automatização do servidor web** com Nginx.
- **Organização por tags** para facilitar a gestão na AWS.

## Como Executar o Projeto

### 1. Instalar Dependências

- Terraform ([https://developer.hashicorp.com/terraform/downloads](https://developer.hashicorp.com/terraform/downloads))
- AWS CLI ([https://aws.amazon.com/cli/](https://aws.amazon.com/cli/))

### 2. Configurar Credenciais AWS

```sh
aws configure
```

### 3. Inicializar e Aplicar o Terraform

```sh
terraform init
terraform apply -auto-approve
```

### 4. Acessar a Instância via SSH

```sh
ssh -i chave_privada.pem ubuntu@IP_PUBLICO
```

### 5. Testar o Servidor Web

Abra o navegador e acesse:

```
http://IP_PUBLICO
```

Deverá aparecer a página padrão do Nginx.

## Como Destruir a Infraestrutura

```sh
terraform destroy -auto-approve
```

## Contribuição

Sinta-se à vontade para sugerir melhorias ou abrir PRs! 😊

## Autor

Amabile

