# 5.1 Criação de Panels
O que está em More Editors nao precisa de um projeto pra ser criado pois estão vinculados a Libs

Botões:
Clear: Limpar form
Separator: Cria um separador entre botões
Retrieve: Consulta no BD
Store: Grava alterações no banco

Ao finalizar a criação do Panel para utiliza-lo como default
ir em ide.asn e descomentar a linha que 

# 5.2 Tarefa 4 

Criação de Panel e configuração de ide.asn com
$LANGUAGE = BRZ
$VARIATION = TREINAMENTO

# 5.3 Criação de tela UF

Ao criar componente, campos que podemos editar

Description: Descrição
Library: TREINAMENTO (Library criada na aula 5.1)
Title:
Panel:
Panel Position: 

Criada tela de cadastro de UF, cadastrei 3 UF's de teste

Atalhos: Ctrl + Arrastar pode levar labels para fora do componente

# 5.4 Criação tela municipio_relac_entidade_uf

Primeiro passo adicionar trigger na UENTDB.MODEL, para herdar para os filhos

Quando pinta tabela pai em cima da filha, colocar como Locking: No Updates porque não quero que a tabela pai permita inclusão de registros, é apenas consulta

# 5.5 Tarefa 5

Trigger corrigida, com melhor legibilidade com switchcase ao inves de if else.
trigger leaveModifiedKey
  retrieve/o
  
  selectcase $status
    case -15
      message/warning/nobeep "The entity is an Up entity and multiple hits were found during the database lookup."
    case -14
      message/warning/nobeep "The entity is a normal Down entity and multiple hits were found during the database lookup (ambiguous key)."
    case -07
      retrieve/x
    case -02
      message/warning/nobeep "Errors during database I/O."
    case 1
      message/warning/nobeep "The entity is painted as an up (foreign) entity with code in the writeUp trigger and the key value was not found during the database lookup. It is assumed that this is a new occurrence."
    case 2
      retrieve/e
      if ($status < 0) message/warning/nobeep "Record not found."
    case 3
      message/warning/nobeep "The occurrence was found among the removed occurrences; it was unremoved."
    case 4
      message/warning/nobeep "The occurrence was found in the component. The current occurrence is removed and the cursor repositioned on the found occurrence."
  endselectcase

  return ($status)
end

A regra geral do Uniface para os números no $status é:
• Valores Maiores ou Iguais a 0 (>= 0): Significam Sucesso (a operação funcionou, mas com comportamentos diferentes).
• Valores Menores que 0 (< 0): Significam Erros ou Avisos Críticos (algo falhou ou não foi encontrado).
Olha o que cada número do seu script significa na prática para o comando retrieve:

Os Status de Erro/Aviso (< 0):

• -02 (Erro de I/O): Erro físico no banco. O banco caiu, a rede falhou ou a tabela não existe.
• -07 (Chave trocada): Você tentou recuperar dados, mas os campos chave mudaram de uma forma que o Uniface precisa de um tratamento especial (retrieve/x).
• -14 e -15 (Registros Duplicados): Você tentou buscar um registro usando uma chave que deveria ser única, mas o banco de dados retornou mais de um resultado. O sistema não sabe qual trazer e avisa que a chave está ambígua.

Os Status de Sucesso com Condição (> 0):

• 0 (Sucesso absoluto): O registro foi encontrado perfeitamente e trazido para a tela. (Por isso seu script nem precisa tratar o 0, ele só deixa o fluxo seguir).
• 1 (Novo registro presumido): O Uniface olhou na tabela estrangeira (Up Entity), não achou nada e assumiu: "Ok, o usuário deve estar digitando um código novo que ainda vai ser cadastrado".
• 2 (Necessita busca externa): Ele achou uma pista, mas precisa que você execute um segundo comando (retrieve/e) para trazer os dados completos do registro.
• 3 (Registro "Des-removido"): Você digitou o código de um registro que tinha acabado de deletar nesta mesma sessão. O Uniface é inteligente e recupera ele da memória temporária em vez de ir ao banco.
• 4 (Já está na tela): Você digitou o código de um registro que já estava aberto em outra linha ou parte do componente. O cursor simplesmente pula para ele.

# 5.6 Criação tela uf_municipio_master_detail

Criação da tela master, onde tabela pai por fora e filho por dentro, aqui podemos salvar UF e Municipio

Cadastro de Municipio onde pai foi por cima de filho, NO UPDATE     

# 5.7 Criação tela uf_municipio_dropdown_list

Adicionar trigger para carregar campo FK

operation exec
throws
variables
string vLstUfs
endvariables
 
 
  clear/e "vend_uf"
  retrieve/e "vend_uf"
  ;Comentar a linha abaixo quando for fazer manual
  putlistitems/id $valrep(cd_uf.vend_municipio), cd_uf.vend_uf, nm_uf.vend_uf
 
  ;Fazendo Dropdowlist manualmente, não esqueçam de tirar o comentário dos comandos abaixo
  ;forentity "vend_uf"
    ;putitem/id vLstUfs, cd_uf.vend_uf, “%%(cd_uf.vend_uf)%%%-%%(nm_uf.vend_uf)”
  ;endfor
  
  ;$valrep(cd_uf.vend_municipio) = vLstUfs
  
  edit
 
  return 0
 
end

# 5.8 Tarefa 6

Criado novo componente com dropdown list, teste com trigger com campo em string literal