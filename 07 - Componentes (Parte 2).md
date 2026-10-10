# 7.1 Criação tela_parceiro

Campos Boolean precisei deixar valor default 0

# 7.2 Tarefa 8

Tela criada

# 7.3 Criando tela pedido usando as sub types

Adicionar ValRep na tabela de pedido em ST_PEDIDO DropDown
1=Em Edição / 2=Fechado / 3=Cancelado

# 7.4 Operações Básicas

Metodos ficam a nivel de componente
Botao apenas chama o metodo call plCalcular()

Function nao exerga escopo antes, parecido com var no javascript
Entry enxerga em todos os escopos, parecido com let

# 7.5 Tarefa 9

Criado tabelas de exemplos de operações, tabela de Pedido ja havia sido criada na aula

Tabela VENDF007, VENDF008 com exemplos de operações via Function no botão e via Trigger no changedValue

# 7.6 Operações basicas parametro na tela

function plCalcular
    params 
        numeric p_tp_operacao :in
        numeric p_vl_valor1 :in
        numeric p_vl_valor2 :in
        numeric p_vl_resultado :out
    endparams

    selectcase p_tp_operacao
        case 1
            call plSomar(p_vl_valor1, p_vl_valor2, p_vl_resultado)
        case 2
            call plSubtriar(p_vl_valor1, p_vl_valor2, p_vl_resultado)
        case 2
            call plMultiplicar(p_vl_valor1, p_vl_valor2, p_vl_resultado)
        case 2
            call plDividir(p_vl_valor1, p_vl_valor2, p_vl_resultado)
    endselectcase
end ;plCalcular

entry plSomar
    params 
        numeric p_vl_valor1 :in
        numeric p_vl_valor2 :in
        numeric p_vl_resultado :out
    endparams

    p_vl_resultado = p_vl_valor1 + p_vl_valor2
end ;plSomar

entry plSubtriar
    params 
        numeric p_vl_valor1 :in
        numeric p_vl_valor2 :in
        numeric p_vl_resultado :out
    endparams

    p_vl_resultado = p_vl_valor1 - p_vl_valor2
end ;plSomar

entry plMultiplicar
    params 
        numeric p_vl_valor1 :in
        numeric p_vl_valor2 :in
        numeric p_vl_resultado :out
    endparams

    p_vl_resultado = p_vl_valor1 * p_vl_valor2
end ;plSomar

entry plDividir
    params 
        numeric p_vl_valor1 :in
        numeric p_vl_valor2 :in
        numeric p_vl_resultado :out
    endparams

    p_vl_resultado = p_vl_valor1 / p_vl_valor2
end ;plSomar

# 7.7 Operações basicas usando serviço

Em services, não tem visibilidade de function

usar "operation" porque é public

Para usar debug, é só chamar a linha "debug" no codigo

Existem variaveis globais que nao sao mais utilizadas

$1 ao $99

# 7.8 Operações basicas usando serviço e listas

trigger valueChanged
	variables
		string lista_entrada
		string lista_saida
	endvariables

	putitem/id lista_entrada, "VALOR_1", vl_valor_1.dummy
	putitem/id lista_entrada, "VALOR_2", vl_valor_2.dummy
	putitem/id lista_entrada, "TP_OPERACAO", tp_operacao.dummy
	
	activate "VENDS002".operacoesBasicasComListas(lista_entrada, lista_saida)
	
	vl_resultado.dummy = $item("RESULTADO", lista_saida)
	

end

operation operacoesBasicasComListas
    params 
        string p_lista_entrada :in
        string p_lista_saida :out
    endparams
    selectcase $item("TP_OPERACAO", p_lista_entrada)
        case 1
            call plSomar(p_lista_entrada, p_lista_saida)
        case 2
            call plSubtriar(p_lista_entrada, p_lista_saida)
        case 3
            call plMultiplicar(p_lista_entrada, p_lista_saida)
        case 4
            call plDividir(p_lista_entrada, p_lista_saida)
    endselectcase
end ;plCalcularoperation operacoesBasicasComListas
    params 
        string p_lista_entrada :in
        string p_lista_saida :out
    endparams
    selectcase $item("TP_OPERACAO", p_lista_entrada)
        case 1
            call plSomar(p_lista_entrada, p_lista_saida)
        case 2
            call plSubtriar(p_lista_entrada, p_lista_saida)
        case 3
            call plMultiplicar(p_lista_entrada, p_lista_saida)
        case 4
            call plDividir(p_lista_entrada, p_lista_saida)
    endselectcase
end ;plCalcular