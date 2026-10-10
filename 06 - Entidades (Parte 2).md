# 6.1 Auto incremente selectdb municipio

Para criar auto increment em campo chave primaria, abrir Widget Property do campo, e tirar Mandatory e adicionar 0, 0 em Min e Max length

Objetos criados por Modeled Entities herdam do pai, se quiser posso fazer ovelay para alterar o comportamento da trigger

trigger write
throws
variables
	numeric vMaxSeq
endvariables
	if ($storetype = 1) ;inserindo
		selectdb max(cd_municipio) from "vend_municipio" to vMaxSeq
		vMaxSeq += 1
		cd_municipio.vend_municipio = vMaxSeq
	endif
; This trigger is fired when Uniface writes the occurrences to the database, typically as part of a store.

  ; Your last moment field updates here, e.g.:
  ; TIMESTAMP.<$entname> = $datim

  write

end

# 6.2 Layout para numeric_data_datetime

Right Aligned
DateTime -> E mascara dd/mm/yyyy hh:mm:ss
Date -> D mascara dd/mm/yyyy
numeric -> N5 = ZZZZ9 (0)
numeric -> N13.2 Z.ZZZ.ZZZ.ZZ9K99 (0,00) 

# 6.3 Criando subtype_cliente_transp

As entidades subtype são especializações das modeled entities e atuam como aliases para tabelas relacionais. Não são geradas tabelas físicas para as subtypes. Os campos e relacionamentos da modeled entitie são reproduzidos na subtype. 
Os casos de utilização de entidades subtype incluem:  

Criar relacionamento da tabela muitos, mais de uma vez para a tabela um, conforme o exemplo do vídeo na tela de pedidos. 
Definir um relacionamento de um para muitos em que tanto a entidade um como a entidade muitos são a mesma entidade – por exemplo, um gerente é um empregado e também tem um relacionamento com vários outros empregados. 
Definir um conjunto de restrições numa entidade ou definir subconjuntos de dados. 
 

Link da documentação 

https://docs.rocketsoftware.com/bundle/uniface_104/page/lwa1703161539517.html 

# 6.4 Tarefa 7

Add auto increment nas tabelas:
VEND_MUNICIPIO
VEND_UNDMEDIDA
VEND_PRODUTO
VEND_PEDIDO
VEND_PARCEIRO

Todos compilando sem erros


## Script
;VEND_MUNICIPIO
trigger write
throws
variables
	numeric vMaxSeq
endvariables
	
	if ($storetype = 1) ;Inserindo
		selectdb max(cd_municipio) from "vend_municipio" to vMaxSeq
		vMaxSeq += 1
		cd_municipio.vend_municipio = vMaxSeq
	endif
	
end ;write


;VEND_UNDMEDIDA
trigger write
throws
variables
	numeric vMaxSeq
endvariables
	
	if ($storetype = 1) ;Inserindo
		selectdb max(cd_undmedida) from "vend_undmedida" to vMaxSeq
		vMaxSeq += 1
		cd_undmedida.vend_undmedida = vMaxSeq
	endif
	
end ;write


;VEND_PRODUTO
;add manualmente
trigger write
throws
variables
	numeric vMaxSeq
endvariables
	
	if ($storetype = 1) ;Inserindo
		selectdb max(cd_produto) from "vend_produto" to vMaxSeq
		vMaxSeq += 1
		cd_produto.vend_produto = vMaxSeq
	endif
	
end ;write


;VEND_PEDIDO
;add manualmente
trigger write
throws
variables
	numeric vMaxSeq
endvariables
	
	if ($storetype = 1) ;Inserindo
		selectdb max(nr_pedido) from "vend_pedido" to vMaxSeq
		vMaxSeq += 1
		nr_pedido.vend_pedido = vMaxSeq
	endif
	
end ;write





;VEND_PARCEIRO para esta tabela tem uma particularidade. Como as subtypes (VEND_CLIENTE_S1 e VEND_TRANSP_S1) herdam as triggers da VEND_PARCEIRO, precisamos usar 
;precompiler directive <$entname>, pois senão ao criarmos auto incremente para o parceiro, quando estivermos na tela de pedido, vai dar erro na tabela VEND_PARCEIRO.
;Documentação Precompiler Directive  https://docs.rocketsoftware.com/bundle/uniface_104/page/mlc1665702620662.html
trigger write
throws
variables
	numeric vMaxSeq
endvariables
	
	if ($storetype = 1) ;Inserindo
		selectdb max(nr_pedido) from "<$entname>" to vMaxSeq
		vMaxSeq += 1
		nr_pedido.<$entname> = vMaxSeq
	endif
	
end ;write