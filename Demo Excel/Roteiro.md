# Power BI - Passo a Passo para demonstração

## Get Data (Obter Dados)

No Power BI, ir para GetData e escolher a conexão de Arquivo de Excel

O Power BI encontrará, dentro do arquivo do Excel, algumas tabelas que podem ser utilizadas para carregar os dados dentro do modelo.

Existem formatações de tabelas do Excel, range de dados ou abas inteiras do Excel

Note que podemos clicar em alguma das tabelas e visualizar um preview dos dados que serão carregados.

Neste caso, utilizaremos apenas as tabelas e range de dados:

Na caixa de seleção, escolha:

* *DIM_Data*
* *DIM_Produtos*
* *FAT_VENDAS*
* *FAT_COMPRAS* (Segunda opção duplicada na lista)
* *Vendedores* 
* *FAT_Target*

Após a carga de dados, vá na terceira opção no menu canto esquerdo do Power BI, onde vemos as relações entre as tabelas. Algumas delas o Power BI entende automaticamente, inclusive COD e ID.

## Edit Queries (Editar Consultas)

Navegue até "Editar Consultas"/"Edit Queries" no menu superior central, alguns dados de FAT_COMPRAS vieram com um formato diferente do necessário para a visualização

* FAT_COMPRAS 
Note que as colunas da "FAT_COMPRAS" vieram com nomes Coluna1, Coluna2... e a primeira linha da tabela é o nome de cada uma das colunas, portanto, na consulta de FAT_COMPRAS, clique em "Use First Row as Headers", esse passo fará com que a primeira linha da tabela substitua o nome das colunas e apague esta linha da tabela.

As colunas da tabela são as datas em que temos compras. Estas colunas deveriam, na verdade, ser linhas, pois para fazer cálculos, utiliza-se a coluna inteira, verticais, e não horizontais, portanto, selecione as duas primeiras colunas usando a tecla shift do teclado e procure pela opção "unpivot other columns" na segunda aba do menu superior do edit queries. ("Transformas outras colunas em linhas" em português). Após transformar as colunas em linhas, renomeie a coluna "atributo" para "data".

Agora temos uma coluna de data e outra de valor, de forma que cada data tenha um valor atribuído na linha e não em várias colunas como estava da maneira antiga. Se desejar ver a transformação, na aba "steps"/"passos" no canto direito da consulta, navegue entre os passos para entender.

* Vendedores

A Consulta "Vendedores" deve ser renomeada para "DIM_Vendedores" para maior facilidade na criação das visualizações (modelo dimensional)

*DIM_DATA 

Na tabela de datas temos uma coluna chamada "full_data" que está em modo de data. Este tipo de formatação o Power BI entende internamente como "MM/dd/aaaa hh:mm:ss", o que faz com que algumas ligações com colunas textuais (o caso da ligação da tabela FAT_COMPRAS) se comprometa, portanto, é necessário modifica-la, mas sem perder uma coluna do tipo Date:

Na consulda de DIM_DATA, duplicar a coluna "full_data" e chama-la de "DateTime". Modificar a coluna "full_data" para textual. 

## Relationship (relação entre as tabelas)

Clique, no menu superior esquerdo, em fechar e aplicar. Após a nova carga de dados, volte à aba de relações no menu esquerdo do Power BI, procure as tabelas de FAT_COMPRAS e DIM_DATA. Clique na coluna "full_data" da DIM_DATA e arraste até a coluna de data na FAT_COMPRAS.

## Measures (medidas) e Hierarquias

Volte para a primeira opção no menu da esquerda, na aba de visualizações

Clique com o botão direito em "FAT_VENDAS" e escolha criar uma nova medida
"Valor da Nota = sum(FAT_Vendas[Preco])*sum(FAT_Vendas[Quantidade_Vendida])"

Para criar uma hierarquia, basta arrastar uma coluna em outra, dentro da mesma tabela: Arraste NM_Departamento para NM_Produto

## Visualizações

Na área de VISUALIZAÇÕES (volte para a primeira opção no menu da esquerda no Power BI), escolha a visualização para colocar filtros (a primeira da 5ª coluna), depois, procure a coluna DateTime da tabela DIM_DATA e selecione o checkbox.

Podemos visualizar o valor total de vendas por departamento, para isso:

Selecione o gráfico de colunas empilhadas e linha.

Escolha a medida calculada criada no passo anterior e coloque-a no campo de Valor. Em eixo, escolha NM_Departamento da tabela DIM_PRODUTOS.

Na linha de trend, escolha a coluna Target_Value da tabela FAT_Target.

Agora podemos mexer com o filtro de data para alterar a visualização criada.

A partir daí, o céu é o limite.

## Objetivos da visualização

Descubra quem é o melhor vendedor por departamento, utilizando as tecnicas de visualização acima. Qual produto tem a maior venda? E qual tem o menor? Qual produto foi comprado mais do que vendido? 

## Publicação e compartilhamento

Clique em "Publicar" na página inicial do Power BI
Logue
Escolha o espaço de trabalho pessoal
Clique em publicar novamente
Abra o "msit.powerbi.com"

