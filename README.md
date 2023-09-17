<h1 align="center">
  <br>
    <img src="https://rafaelangelin.com/perfil.jpg" alt="Rafael Angelin" width="200"></a>
<br> <br>
Rafael Angelin

  
</h1>
<p align="center">
  <a href="https://github.com/RafaAngelin">
    <img src="https://img.shields.io/badge/Follow-Lab%20Page-blue" alt="Lab">
  </a> 
</p>
 
<p align="center">
Rafael Angelin <a href="https://github.com/RafaAngelin" target="_blank">(Angelin, R.)</a>
</p>

<p align="center">  
<b>Profissão</b>: <a href="#" target="_blank">LAMIA - Laboratório de Aprendizado de Máquina e Imagens Aplicados à Indústria </a> <br>
<b>Email</b>: <a href="mailto:rafael.angelin@escola.pr.gov.br" target="_blank">rafael.angelin@escola.pr.gov.br</a> <br>
<b>Formação</b>: <a href="http://portal.utfpr.edu.br" target="_blank">Universidade Tecnológica Federal do Paraná</a>
<a href="https://portal.utfpr.edu.br/campus/franciscobeltrao" target="_blank"> - Campus Francisco Beltrão</a> <br>
</p>

<p align="center">
<br>
Status do Projeto: Em desenvolvimento :warning:
</p>

# Resumo
O projeto consiste em desenvolver um jogo digital com base em uma dinâmica de tabuleiro para uso em sala de aula para testar conhecimentos dos alunos de forma individual ou em grupo. O projeto possui os diferenciais de utilizar recursos de efeitos visuais da engine Unity e não utilizar conteúdos de aprendizado estáticos, sendo possível o professor customizar os conteúdos de conhecimento que são utilizados no jogo. 

## Objetivo
O objetivo principal do projeto E-Battle é o de estimular o aprendizado em sala de aula através da competitividade saudável entre os jogadores. O grande diferencial do projeto está justamente na total personalização do conteúdo das perguntas realizadas durante a partida, que ficará a cargo do aplicador/professor.


## Como Utilizar
Para clonar e executar a aplicação é necessário baixar a ferramenta Unity, uma das mais famosas game engine utilizadas atualmente. A versão utilizada da game engine para o desenvolvimento do projeto é a 2019.4.13f1.
O banco de dados utilizado para o desenvolvimento do projeto é o PostgreSQL, que atualmente ainda está hospedado localmente, portanto, para testar a versão atual também é necessário realizar o download do pgAdmin 4.

As configurações necessárias para realizar a criação do banco são as seguintes:

```bash
 "Server=127.0.0.1;" +
 "Database=e-battle;" +
 "User ID=postgres;" +
 "Password=senha;";
```

As tabelas existentes na versão atual do projeto são: <i>perguntas</i> e <i>temas</i>

tabela <i>perguntas</i>:

```bash
  CREATE TABLE public.perguntas
(
    id_pergunta SERIAL,
    id_tema integer NOT NULL,
    texto_pergunta text COLLATE pg_catalog."default" NOT NULL,
    alternativas text COLLATE pg_catalog."default",
    CONSTRAINT perguntas2_pkey PRIMARY KEY (id_pergunta)
)

TABLESPACE pg_default;

ALTER TABLE public.perguntas
    OWNER to postgres;

```

tabela <i>temas</i>:
```bash
  
CREATE TABLE public.temas
(
    id_tema SERIAL,
    nome text COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT temas_pkey PRIMARY KEY (id_tema)
)

TABLESPACE pg_default;

ALTER TABLE public.temas
    OWNER to postgres;
```

# Versão 2

Atualmente, o projeto está sendo organizado para que a segunda versão seja feita, e com isso, foi feito um novo banco de dados, que permite uma especificação maior do usuário, além de permitir a inserção de imagens para serem usadas nas perguntas. Para fazer a criação das tabelas acima, é necessário criar um <i>schema</i> novo chamado ebattle. O nome do database usado para esta versão 2 é <i>e-battle-2.0</i>.

Abaixo estão os scripts de criação das novas tabelas:

Tabela <i>ConjuntoPergunta</i>

```bash
CREATE TABLE ebattle."conjuntoPergunta"
(
    conj_perg_id integer NOT NULL,
    user_id integer,
    perguntas_id integer[],
    "id_temaProfundidade" integer,
    visibilidade boolean,
    nome_conjunto text COLLATE pg_catalog."default",
    CONSTRAINT "conjuntoPergunta_pkey" PRIMARY KEY (conj_perg_id)
)

TABLESPACE pg_default;

ALTER TABLE ebattle."conjuntoPergunta"
    OWNER to postgres;
```

Tabela <i>Pergunta</i>

```bash
CREATE TABLE ebattle.pergunta
(
    id_pergunta integer NOT NULL,
    descricao text COLLATE pg_catalog."default",
    alternativas text COLLATE pg_catalog."default",
    imagem bytea,
    dificuldade integer,
    tempo integer,
    CONSTRAINT pergunta_pkey PRIMARY KEY (id_pergunta)
)

TABLESPACE pg_default;

ALTER TABLE ebattle.pergunta
    OWNER to postgres;
```

Tabela <i>TemaGeral</i>

```bash

CREATE TABLE ebattle."temaGeral"
(
    id_tema integer NOT NULL,
    tema_descricao text COLLATE pg_catalog."default",
    CONSTRAINT "temaGeral_pkey" PRIMARY KEY (id_tema)
)

TABLESPACE pg_default;

ALTER TABLE ebattle."temaGeral"
    OWNER to postgres;

```
