# Power BI - Passo a Passo para demonstra��o

## Get Data (Obter Dados)

No Power BI, ir para GetData e escolher a conex�o de Arquivo de Excel

![Caption for the picture.](./images/getdata.png)


O Power BI encontrar�, dentro do arquivo do Excel, algumas tabelas que podem ser utilizadas para carregar os dados dentro do modelo.

Existem formata��es de tabelas do Excel, range de dados ou abas inteiras do Excel

Note que podemos clicar em alguma das tabelas e visualizar um preview dos dados que ser�o carregados.

Neste caso, utilizaremos apenas as tabelas e range de dados:

Na caixa de sele��o, escolha:

* *DIM_Data*
* *DIM_Produtos*
* *FAT_Target*
* *FAT_VENDAS*
* *FAT_COMPRAS* (Segunda op��o duplicada na lista)
* *Vendedores* 

Clique em "Load"/"Carregar" ap�s selecionar as tabelas acima.

Ap�s a carga de dados, v� na terceira op��o no menu canto esquerdo do Power BI, onde vemos as rela��es entre as tabelas. Algumas delas o Power BI entende automaticamente, inclusive COD e ID.

## Edit Queries (Editar Consultas)

Navegue at� "Editar Consultas"/"Edit Queries" no menu superior central, alguns dados de FAT_COMPRAS vieram com um formato diferente do necess�rio para a visualiza��o

### FAT_COMPRAS 

Note que as colunas da "FAT_COMPRAS" vieram com nomes Coluna1, Coluna2... e a primeira linha da tabela � o nome de cada uma das colunas, portanto, na consulta de FAT_COMPRAS, clique em "Use First Row as Headers" na se��o "Transform" do menu superior, esse passo far� com que a primeira linha da tabela substitua o nome das colunas e apague esta linha da tabela.

As colunas da tabela s�o as datas em que temos compras. Estas colunas deveriam, na verdade, ser linhas, pois para fazer c�lculos, utiliza-se a coluna inteira, verticais, e n�o horizontais, portanto, selecione as duas primeiras colunas usando a tecla shift do teclado e procure pela op��o "unpivot other columns" na segunda aba do menu superior do edit queries. ("Transformas outras colunas em linhas" em portugu�s). Ap�s transformar as colunas em linhas, renomeie a coluna "atributo" para "data".

Agora temos uma coluna de data e outra de valor, de forma que cada data tenha um valor atribu�do na linha e n�o em v�rias colunas como estava da maneira antiga. Se desejar ver a transforma��o, na aba "steps"/"passos" no canto direito da consulta, navegue entre os passos para entender.

### Vendedores

A Consulta "Vendedores" deve ser renomeada para "DIM_Vendedores" para maior facilidade na cria��o das visualiza��es (modelo dimensional)

### DIM_DATA 

Na tabela de datas temos uma coluna chamada "full_data" que est� em modo de data. Este tipo de formata��o o Power BI entende internamente como "MM/dd/aaaa hh:mm:ss", o que faz com que algumas liga��es com colunas textuais (o caso da liga��o da tabela FAT_COMPRAS) se comprometa, portanto, � necess�rio modifica-la, mas sem perder uma coluna do tipo Date:

Na consulda de DIM_DATA, duplicar a coluna "full_data" e chama-la de "DateTime". Modificar a coluna "full_data" para textual, para isso, clique com o bot�o direito > "change type" > text. 

## Relationship (rela��o entre as tabelas)

Clique, no menu superior esquerdo, em fechar e aplicar. Ap�s a nova carga de dados, volte � aba de rela��es no menu esquerdo do Power BI, procure as tabelas de FAT_COMPRAS e DIM_DATA. Clique na coluna "full_data" da DIM_DATA e arraste at� a coluna de data na FAT_COMPRAS.

## Measures (medidas) e Hierarquias

Volte para a primeira op��o no menu da esquerda, na aba de visualiza��es

Clique com o bot�o direito em "FAT_VENDAS" e escolha criar uma nova medida
"Valor da Nota = sum(FAT_Vendas[Preco])*sum(FAT_Vendas[Quantidade_Vendida])"

Para criar uma hierarquia, basta arrastar uma coluna em outra, dentro da mesma tabela: Arraste NM_Produto para Nome_Departamento da tabela DIM_PRODUTOS

## Visualiza��es

### Objetivos da visualiza��o:

Descubra quem � o melhor vendedor com filtro de departamento e de data.
Qual produto tem a maior venda? E qual tem o menor?


### Criar visualiza��o

Na �rea de VISUALIZA��ES, escolha a visualiza��o para colocar filtros (a primeira op��o da 5� linha, da �rea de visualiza��es), depois, procure a coluna DateTime da tabela DIM_DATA e selecione o checkbox.

Clique fora da visualiza��o criada e adicione um novo filtro, com NM_Departamento desta vez.

Clique novamente fora da visualiza��o criada acima e selecione o gr�fico de colunas empilhadas.

Escolha a medida calculada criada no passo anterior (Valor da nota) e coloque-a no campo de Valor(coluna), se apenas clicar no checkbox, o Power BI entende essa coluna como num�rica e faz isso por voc�. No campo de eixo, adicione o nome dos vendedores da tabela DIM_Vendedores. Novamente, apenas clicar no checkbox funciona automaticamente.

Com os passos acima podemos filtrar datas e departamentos para descobrir quem vendeu mais nas datas e departamentos escolhidos.

Adicione outro gr�fico de colunas, desta vez, o gr�fico de colunas empilhadas e linha. Selecione valor da nota e nm_produto.

Na linha de valor, escolha a coluna Target_Value da tabela FAT_Target.

Agora podemos modificar com o filtro de data para alterar as visualiza��es criadas.

A partir da�, o c�u � o limite.


## Publica��o e compartilhamento

Ap�s criar as visualiza��es, clique em "Publicar" no menu inicial do Power BI

Quando abrir a caixa de di�logo, coloque seu email corporativo e senha.

Escolha o espa�o de trabalho pessoal e publique.

Clique no link para visualizar o relat�rio no site ou abra o "msit.powerbi.com"

Na op��o "Arquivo" podemos compartilhar este relat�rio na web ou SharePoint. Na op��o "Compartilhar" podemos compartilhar com um grupo ou usu�rio espec�fico.

### Teams

Abra o Teams na aba de teams. Escolha um time que gostaria de compartilhar o relat�rio criado e clique no sinal "+". Procure por Power BI na �rea de adicionar uma aba.	 Selecione o espa�o de trabalho em que o relat�rio foi publicado e selecione-o.

## Atualizando o relat�rio

Por fim, para atualizar o relat�rio no site do Power BI, podemos navegar at� o espa�o de trabalho, na �rea esquerda, procurar por Data Sources/Conjuntos de Dados, clicar na retic�ncias ao lado do conjunto de dados e clicar em "Atualizar Agora".

Note que este passo s� funcionar� se o arquivo utilizado estiver em algum servi�o online como SharePoint. Se estiver na m�quina f�sica, ser� necess�rio publica-lo novamente a partir do Power BI Desktop ou criar um gateway(n�o recomend�vel).