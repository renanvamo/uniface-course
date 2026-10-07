# 4.1 Modeled Objects Conceituação
Modeled Objects são objetos de desenvolvimento que podem ser herdados por outros objetos de desenvolvimento, que normalmente são criados usando o objeto modelado. Derived Objects herdam de Modeled Objects. Assim, uma entidade que é criada usando uma Modeled Entity é uma derived entity.

Nas versões anteriores do Uniface, apenas os objetos pertencentes ao modelo eram ocasionalmente chamados de Modeled Object. No Uniface 10, o termo foi ampliado e tornado mais consistente. Os Modeled Objects agora são:

Modeled Entities and fields — definições de entidades e campos que definem os dados que o aplicativo acessa, bem como objetos que não são de banco de dados, como botões reutilizáveis.
Modeled Properties — são valores nomeados de propriedades selecionadas de entidade e campo, como as propriedades Interface de campo , Layout de campo e Sintaxe de campo . no Uniface 9, eles eram conhecidos como templates.
Modeled Components — são componentes usados ​​para criar outros componentes com as mesmas propriedades de nível de componente e ProcScript. no Uniface 9, eles eram conhecidos como templates de componentes.
O conceito de “Model” não existe mais no Uniface 10 como um objeto separado. Em vez disso, é uma parte obrigatória do nome da entidade modelada e identifica o namespace da entidade. No entanto, o termo “Model” ainda pode ser usado para se referir a uma coleção de objetos modelados que compartilham o mesmo namespace.

MODELED COMPONENT 

As templates de componente das versões abaixo do 10, agora mudaram para para “Modeled Component”. Os modeled components trabalharão na forma de herança, em qualquer alteração no comportamento de um objeto modelado, será alterado o mesmo comportamento do objeto que recebeu a herança. As triggers criadas no Modeled Component não serão copiadas para o componente que o herdou como era na versão 9. Se quiser mudar o comportamento padrão de uma determinada trigger, é preciso copiar a trigger do Modeled Component, incluir a trigger no novo componente e alterar conforme necessidade. Mas também é possível criar um componente que não possua uma dependência de um objeto modelado.

MODELED FIELD

Modeled Fields é a nova terminologia referente ao que existia nas versões abaixo da versão 10, conhecido como Field Template. Quando fala de field template, não está se referindo a field interface, nem field syntax e nem field layout. Estes 3 últimos se encontram no menu “More Editors/Modeled”.

Quando fizemos a importação da versão do 9 para a versão 10.4 o uniface criou uma tabela Chamada V9TEMPLATE.V9TEMPLATE. Conforme a imagem abaixo, realmente é uma tabela com a propriedade Purpose = 