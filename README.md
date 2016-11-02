# Sistem SOL

Sistema de Gerenciamento Interno.

## Como desenvolver?

1. Crie o banco de dados no mysql.
2. Clone o repositório.
3. Baixe o brach master do projeto para sua máquina.
4. Inicie o projeto usando o git-flow.
5. Crie o branch em que vai trabalhar.
6. Rode o seu projeto.

```console
$ mysql -u root -p
mysql> CREATE DATABASE IF NOT EXISTS sisconstructiondb;
mysql> exit
$ git clone --recursive https://github.com/onedreams/sistema-sol.git
$ cd sistema-sol
$ git branch master origin/master
$ git flow init -d
$ git flow feature start <sua feature>
$ grails run-app
```
