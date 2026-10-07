# 3.1 Criando a primeira tabela no Uniface
Campos importantes na criação de colunas

Is_External 
True = Cria campo na tabela
False = Campo de visualização apenas

Field Syntax
Uppercase/Mandatory/Min lengh (Não precisa max pq o varchar40 ja determina)
Form Widget Property
Double Click -> Detail para que o duplo clique acione o evento de detalhes

Packing Code
N -> Numeric
VC / C -> VarChar / Char
D -> Date
E -> DateTime
B -> Boolean

Define Keys
PK
Unique = Candidate

# 3.2 Tarefa 1

Tabela VEND_UF.VEND criada

.VEND não é obrigatório é convenção de acordo com modulo, poderia ser .RH .FINAN .COMPR

# 3.3 Criando Relacionamento UF Municipio

Importante, pra criar relacionamento sempre abrir a tabela filha e arrastar a tabela pai até ela na aba "Define Relationships"

Delete Constraint -> Restricted impede de apagar se existir algun registro relacionado ao registro que esta sendo apagado

Index on FK -> Cria o index na tabela filho, para a FK ter um index

Referencial Integrity -> True (cria constriant)
Procedure nome do referencial, geralmente nome das tabelas unidas vend_uf_vend_municipio

# 3.4 Tarefa 02

Criada tabela com relacionamento e compilado

# 3.5 Criando script relacionamento uf_municipio

/gensql createTable vend_uf.vend sle c:\uniface\vend_uf.sql
ou
/gensql createTable *.vend sle c:\uniface\vend.sql

sle = drive sqlite

# 3.6 Tarefa 03 

Tabelas criadas em DB Browser for SQLite

Arquivos gerados ficam em:
C:\uniface\vend_uf.vend

criei arquivo que vai conter o db e os dados em SQLite
C:\Users\Suporte\Rocket Uniface 10 Community Edition\project\dbms\userdata.db