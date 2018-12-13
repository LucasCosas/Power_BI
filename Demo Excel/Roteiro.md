# Power BI - Passo a Passo para demonstra��o

## Get Data (Obter Dados)

No Power BI, ir para GetData e escolher a conex�o de Arquivo de Excel

O Power BI encontrar�, dentro do arquivo do Excel, algumas tabelas que podem ser utilizadas para carregar os dados dentro do modelo.

Existem formata��es de tabelas do Excel, range de dados ou abas inteiras do Excel

Note que podemos clicar em alguma das tabelas e visualizar um preview dos dados que ser�o carregados.

Neste caso, utilizaremos apenas as tabelas e range de dados:

Na caixa de sele��o, escolha:

* *DIM_Data*
* *DIM_Produtos*
* *FAT_VENDAS*
* *FAT_COMPRAS* (Segunda op��o duplicada na lista)
* *Vendedores* 
* *FAT_Target*

Ap�s a carga de dados, v� na terceira op��o no menu canto esquerdo do Power BI, onde vemos as rela��es entre as tabelas. Algumas delas o Power BI entende automaticamente, inclusive COD e ID.

## Edit Queries (Editar Consultas)

Navegue at� "Editar Consultas"/"Edit Queries" no menu superior central, alguns dados de FAT_COMPRAS vieram com um formato diferente do necess�rio para a visualiza��o

* FAT_COMPRAS 
Note que as colunas da "FAT_COMPRAS" vieram com nomes Coluna1, Coluna2... e a primeira linha da tabela � o nome de cada uma das colunas, portanto, na consulta de FAT_COMPRAS, clique em "Use First Row as Headers", esse passo far� com que a primeira linha da tabela substitua o nome das colunas e apague esta linha da tabela.

As colunas da tabela s�o as datas em que temos compras. Estas colunas deveriam, na verdade, ser linhas, pois para fazer c�lculos, utiliza-se a coluna inteira, verticais, e n�o horizontais, portanto, selecione as duas primeiras colunas usando a tecla shift do teclado e procure pela op��o "unpivot other columns" na segunda aba do menu superior do edit queries. ("Transformas outras colunas em linhas" em portugu�s). Ap�s transformar as colunas em linhas, renomeie a coluna "atributo" para "data".

Agora temos uma coluna de data e outra de valor, de forma que cada data tenha um valor atribu�do na linha e n�o em v�rias colunas como estava da maneira antiga. Se desejar ver a transforma��o, na aba "steps"/"passos" no canto direito da consulta, navegue entre os passos para entender.

* Vendedores

A Consulta "Vendedores" deve ser renomeada para "DIM_Vendedores" para maior facilidade na cria��o das visualiza��es (modelo dimensional)

*DIM_DATA 

Na tabela de datas temos uma coluna chamada "full_data" que est� em modo de data. Este tipo de formata��o o Power BI entende internamente como "MM/dd/aaaa hh:mm:ss", o que faz com que algumas liga��es com colunas textuais (o caso da liga��o da tabela FAT_COMPRAS) se comprometa, portanto, � necess�rio modifica-la, mas sem perder uma coluna do tipo Date:

Na consulda de DIM_DATA, duplicar a coluna "full_data" e chama-la de "DateTime". Modificar a coluna "full_data" para textual. 

## Relationship (rela��o entre as tabelas)

Clique, no menu superior esquerdo, em fechar e aplicar. Ap�s a nova carga de dados, volte � aba de rela��es no menu esquerdo do Power BI, procure as tabelas de FAT_COMPRAS e DIM_DATA. Clique na coluna "full_data" da DIM_DATA e arraste at� a coluna de data na FAT_COMPRAS.

## Measures (medidas) e Hierarquias

Volte para a primeira op��o no menu da esquerda, na aba de visualiza��es

Clique com o bot�o direito em "FAT_VENDAS" e escolha criar uma nova medida
"Valor da Nota = sum(FAT_Vendas[Preco])*sum(FAT_Vendas[Quantidade_Vendida])"

Para criar uma hierarquia, basta arrastar uma coluna em outra, dentro da mesma tabela: Arraste NM_Departamento para NM_Produto

## Visualiza��es

Na �rea de VISUALIZA��ES (volte para a primeira op��o no menu da esquerda no Power BI), escolha a visualiza��o para colocar filtros (a primeira da 5� coluna), depois, procure a coluna DateTime da tabela DIM_DATA e selecione o checkbox.

Podemos visualizar o valor total de vendas por departamento, para isso:

Selecione o gr�fico de colunas empilhadas e linha.

Escolha a medida calculada criada no passo anterior e coloque-a no campo de Valor. Em eixo, escolha NM_Departamento da tabela DIM_PRODUTOS.

Na linha de trend, escolha a coluna Target_Value da tabela FAT_Target.

Agora podemos mexer com o filtro de data para alterar a visualiza��o criada.

A partir da�, o c�u � o limite.

## Objetivos da visualiza��o

Descubra quem � o melhor vendedor por departamento, utilizando as tecnicas de visualiza��o acima. Qual produto tem a maior venda? E qual tem o menor? Qual produto foi comprado mais do que vendido? 

## Publica��o e compartilhamento

Clique em "Publicar" na p�gina inicial do Power BI
Logue
Escolha o espa�o de trabalho pessoal
Clique em publicar novamente
Abra o "msit.powerbi.com"

