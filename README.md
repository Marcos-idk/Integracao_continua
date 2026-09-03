# Aula prática - Docker e GitHub Codespaces

## 1. Identificação
Nome do aluno: [Seu Nome Aqui]

## 2. Docker no Codespaces
Versão do Docker utilizada: Docker version 26.1.3, build b72b43f (ou a saída obtida no seu terminal)
O comando `docker info` executou com sucesso e confirmou o funcionamento do daemon Docker no ambiente.

## 3. Contêiner Nginx
Ao executar a imagem Nginx com mapeamento da porta 8080:80, o servidor respondeu na porta do Codespaces. O comando `docker exec` confirmou a presença do arquivo `index.html` no diretório `/usr/share/nginx/html`. Ao final, o contêiner foi encerrado e removido.

## 4. Imagem personalizada
Nome/Tag da imagem criada: `aula-docker:1.0`
Resultado de `docker run --rm aula-docker:1.0`:
`Olá! Esta imagem Docker foi criada na aula de Integração e Entrega Contínua.`

## 5. Docker Compose
Resultado de `docker compose ps`:
Serviços `aula-mysql` (porta 3306) e `aula-phpmyadmin` (porta 8080) em execução.
O acesso ao phpMyAdmin foi realizado com sucesso via aba PORTS com login `root` e senha `root_password`, confirmando o banco `aula_db`.

## 6. Persistência
O registro permaneceu no banco após a execução de `docker compose down` seguido de `docker compose up -d` porque os dados da pasta `/var/lib/mysql` foram associados ao volume gerenciado `mysql-data`, mantendo o armazenamento de dados desvinculado do ciclo de vida dos contêineres.

## 7. Perguntas e Respostas

1. **Qual é a diferença entre uma imagem Docker e um contêiner?**
   Uma imagem é um modelo/template imutável que contém o código, runtime e dependências. O contêiner é a instância em execução criada a partir dessa imagem.

2. **O que significa o mapeamento de portas 8080:80?**
   Significa redirecionar o tráfego da porta 8080 do ambiente hospedeiro (Codespaces) para a porta 80 interna do contêiner.

3. **Qual é a função do Dockerfile neste exercício?**
   Definir as instruções passo a passo para construir a imagem personalizada `aula-docker:1.0` a partir da imagem base do Ubuntu.

4. **Por que o serviço phpMyAdmin consegue acessar o MySQL usando PMA_HOST: mysql?**
   Porque o Docker Compose cria uma rede compartilhada onde os contêineres conseguem se comunicar utilizando o nome dos serviços como endereço de rede (DNS interno).

5. **Qual é a função do volume mysql-data?**
   Garantir a persistência dos dados do MySQL fora do contêiner, para que as informações do banco não sejam perdidas ao parar ou recriar o contêiner.

6. **O que aconteceria com os dados se o ambiente fosse encerrado com docker compose down -v?**
   A opção `-v` remove os volumes associados ao ambiente, destruindo o volume `mysql-data` e apagando permanentemente todos os dados armazenados no banco.