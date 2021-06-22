# •	Linguagem SQL

Structured Query Language, ou Linguagem de Consulta Estruturada ou SQL, é a linguagem de pesquisa declarativa padrão para banco de dados relacional (base de dados relacional).

![bancoDedados](https://github.com/augusto-vieira/Linguagem_SQL/blob/master/img/DescricaoDB.png)

![bancoDedados](https://github.com/augusto-vieira/Linguagem_SQL/blob/master/Gif/BancoDeDados.gif)


A linguagem SQL é dividida em subconjuntos de acordo com as operações que queremos efetuar sobre um banco de dados. 

1. **Podemos dividir em 3 partes:**
    - DDL - Linguagem de **Definição** de Dados
    - DML - Linguagem de **Manipulação** de Dados
    - DCL - Linguagem de **Controle** de Dados


1. **Comandos DDL:**
    - CREATE TABLE
    - CREATE INDEX
    - CREATE VIEW
    - ALTER TABLE
    - ALTER INDEX
    - DROP INDEX
    - DROP VIEW


2. **Comandos DML:**
    - SELECT
    - INSERT
    - UPDATE
    - DELETE

2. **Comandos LCD:**
    - GRANT
    - REVOKE 
    - DELETE

# Comandos:


**Criar um Banco de Dados :**
``` SQL
CREATE DATABASE cadastro;
```
**Crir um Banco de Dados Configurado :**
``` SQL
# Codificação de caracter padrão(que tem acentuação)
CREATE DATABASE cadastro
DEFAULT CHARACTER SET utf8
DEFAULT COLLATE utf8_general_ci;
```

**Selecionar o DB :**
``` SQL
# Abre o Database “cadastro”
- USE cadastro;
```

**Criar uma Tabela :**
``` SQL
CREATE TABLE pessoas (
Nome varchar(30),
Idade tinyist,
Sexo char
Peso float,
Altura float,
Nacionalidade varchar()
);
```
**Criar uma Tabela Melhorada :**
``` SQL
CREATE TABLE pessoas(
id int not null auto_increment,
nome varchar(30) not null,
nascimento date,
sexo enum('M','F’),
peso decimal(5,2),
altura decimal(3,2),
nacionalidade varchar(20) default 'Brasil’,
primary key (id)
)default charset=utf8; 
```


**Mostrar uma Tabela :**
``` SQL
# Descreve a Tabela pessoas, mostra com é a estrutura da tabela.
DESCRIBE pessoas;
```

**Status do Banco :**
``` SQL
# Verifica qual banco de dados está aberto
STATUS;
```

**Apagar um Banco de Dados :**
``` SQL
DROP DATABASE cadastro;
```

**Inserir dados em uma Tabela :**
``` SQL
# Inserir Linhas
INSERT INTO pessoas VALUES(
default, 'Carlos', '1920-12-30', 'M', '65.0', '1.94', 'Italia');
```

**Mostrar os dados da Tabela :**
``` SQL
SELECT * FROM pessoas;
```

**Adicionar uma Coluna na Tabela :**
``` SQL
# Inserção automática na última coluna da Tabela
ALTER TABLE pessoas
ADD COLUMN profissao varchar(10);
```

**Remover uma Coluna :**
``` SQL
ALTER TABLE pessoas
DROP COLUMN profissao;
```


**Adicionar uma Coluna  em local específico da Tabela :**
``` SQL
# Adicionada antes da Coluna 'nome'
ALTER TABLE pessoas
ADD COLUMN profissao varchar(10) AFTER nome; 
```


**Adicionar uma Coluna na primeira posição da Tabela  :**
``` SQL
ALTER TABLE pessoas
ADD COLUMN codigo int FIRST;
```


**Modificar Definições :**
``` SQL
## Modifica a coluna prosissão(varchar(10)) para varchar(50)
ALTER TABLE pessoas
MODIFY COLUMN profissao varchar(50);
```


**Renomear uma Coluna :**
``` SQL
# De 'profissao' para 'prof'
ALTER TABLE pessoas
CHANGE COLUMN profissao prof varchar(50);
```


**Renomear uma Tabela :**
``` SQL
ALTER TABLE pessoas
RENAME TO Empresa;
```


**Apagar uma Tabela :**
``` SQL
DROP TABLE cursos:
```

**Parâmetro "IF NOT EXISTS" :**
``` SQL
# significa que só vai criar a tabela caso ela não exista
# sem esse parâmetro a tabela iria ser sobrescrita(perdendo os dados)
CREATE TABLE IF NOT EXISTS cursos(
nome varchar(30) not null,
descriçao text,
)default charset=utf8; 

```
**Adicionar Chave Primaria na Tabela :**
``` SQL
# Tabela já existente, necessário dois comandos.
ALTER TABLE cursos
ADD COLUMN idcurso int FIRST;

ALTER TABLE cursos
ADD PRIMARY KEY(idcursos);
```


### Manipulando Linhas (UPDATE, DELETE e TRUNCATE)
Algumas literaturas podem se referir como Maninupalçao de Registros ou Manipulação de Tuplas.

**Tabela com linhas a ser modificadas:**
![TabelaCursos](https://github.com/augusto-vieira/Linguagem_SQL/blob/master/Gif/TabelaCursos.gif)

**Alterar o nome da linha 1 :** 
``` SQL
# A chave primaria(idCurso) identifica cada linha
update cursos 
set nome = 'HTML5'
where idCurso = '1'; 
```
![AlterarUmaLinha](https://github.com/augusto-vieira/Linguagem_SQL/blob/master/Gif/AlterarUmaLinha.gif)


Não é possível manipular várias linhas ao mesmo tempo(um comando para uma linha), mas é possível mexer dentro uma linha em diversas colunas ao mesmo tempo. 

**Modificar duas colunas com um unico comando :** 
``` SQL
update cursos 
set nome = 'PHP', ano = '2015'
where idCurso = '4';
```
![AlterarDuasColunas](https://github.com/augusto-vieira/Linguagem_SQL/blob/master/Gif/AlterarDuasColunas.gif)

É possível que em alguns casos o comando possa apagar mais de uma linha, por
precaução é conveniente usar o parâmetro LIMIT.

**Parâmetro LIMIT :** 
``` SQL
# Limita a quantidade de linhas que irá ser modificada(uma proteção)
update cursos 
set nome = 'Java',carga = '40', ano = '2015'
where idCurso = '5'
LIMIT 1;
```
![AlterarDuasColunas](https://github.com/augusto-vieira/Linguagem_SQL/blob/master/Gif/ParametroLimit.gif)

**Remover uma linha específica :** 
``` SQL 
DELETE FROM cursos
WHERE idCurso = '8';
```

**Remover diversas linhas de uma vez :** 
``` SQL 
# Coluna ano, onde tiver o valor 2018 será apagado
DELETE FROM cursos
WHERE ano ='2018'
LIMIT 3;
```
**Remover TODAS as linhas :** 
``` SQL
TRUNCATE TABLE cursos;
```

### Gerenciando Cópias de Segurança MySQL

1. **Exportar um Dump do Banco de Dados(Workbench):**
    - Click em "Server" :
        - Click em "Data **Export**"
    - Selecione os Bancos de Dados
    - Selecione as opções de exportação:
        - Dump Structure and Data
        - Dump Data Only
        - Dump Structure Only
    - Selecione as opções de exportação do Projeto:
        - Export to Dump Project Folder
        - Export to Self-Contained File
    - Selecione:
        - Include Create Schema(Cria o banco automático)
    - Selecione:
        - Start Export
    - Saída:
        - Dump20210209.sql

![ExportDump](https://github.com/augusto-vieira/Linguagem_SQL/blob/master/Gif/DumpExport.gif)


1. **Importar um Dump para o Banco de Dados(Workbench):**
    - Click em "Server" :
        - Click em "Data **Import**"
    - Selecione a opção de importação:
        - Import from Dump Project Folder
        - Import from Self-Contained File
            - Selecione o Dump(Dump20210209.sql)
    - Selecione:
        - Start Import

![ImportDump](https://github.com/augusto-vieira/Linguagem_SQL/blob/master/Gif/DumpImport.gif)

### Referência:
- https://www.youtube.com/watch?v=Ofktsne-utM&list=PLHz_AreHm4dkBs-795Dsgvau_ekxg8g1r&ab_channel=CursoemV%C3%ADdeo
    
    - contato@cursoemvideo.com
- https://www.mysql.com/
- https://pt.wikipedia.org/wiki/SQL


















