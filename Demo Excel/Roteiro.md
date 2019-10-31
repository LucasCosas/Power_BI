# Power BI - Passo a Passo para demonstra��o

## Configurar Power BI

Antes de come�armos, importante certificar de que o Power BI est� em Portugu�s Brasileiro para o passo a passo abaixo.

Para isso, v� a File > Op��es e Configura��es > Op��es

![GetConfig.](./images/options.png)

Verifique na aba Configura��es Regionais se o idioma est� em Portugu�s Brasileiro.

![GetConfigreg.](./images/configreg.png)

## Get Data (Obter Dados)

Para o workshop, primeiramente navegue at� o link abaixo
https://github.com/LucasCosas/Power_BI/blob/master/Demo%20Excel/_OLD/Dados.xlsx.

Clique em "Download" e salve o arquivo de excel no diret�rio C:/ArquivoExcel

No Power BI Desktop, v� para GetData e escolha a conex�o de Arquivo de Excel

![GetData.](./images/getdata.png)
![GetDataExcel.](./images/getdataexcel.png)

Procure a tabela de Excel no diret�rio salvo no passo anterior.

O Power BI encontrar�, dentro do arquivo do Excel, algumas tabelas que podem ser utilizadas para carregar os dados dentro do modelo.

Note que podemos clicar em alguma das tabelas e visualizar um preview dos dados que ser�o carregados.

Neste caso, utilizaremos apenas os dados formatados nas abas dentro do arquivo excel:

Na caixa de sele��o, escolha:

* *Localizacao*
* *Fabricante*
* *Vendas* 
* *Produtos*


![tabelasexcel.](./images/tabelasexcel.png)


Clique em "Editar" ap�s selecionar as tabelas acima.

# Edit Queries (Editar Consultas)

Editar Consultas � o lugar onde voc� far� as edi��es nas tabelas que ser�o feitas as cargas para o modelo do Power BI. � importante fazer as modifica��es necess�rias antes da cria�ao das visualiza��es.

### Tabela Vendas

Alterar os tipos de dados das colunas:

Para alterar, clique no s�mbolo que aparece ao lado esquerdo da coluna, exemplo abaixo.

![alterandodate.](./images/alterandodate.png)

Date: Alterar para Data.
Valor Base: Decimal Fixo.
Valor da Venda: Decimal Fixo.

### Tabela Localiza��o

Selecione a tabela Endere�o. Na aba Transformar do menu superior, escolha Dividir Coluna por Delimitador

![delimitador.](./images/delimitador.png)

Na tela que abrir, escolha delimitador de v�rgula e clique OK.

Renomeie a coluna Endere�o.1 para Cidade e Endere�o.2 para Estado. Clique com o bot�o direito em cima do nome da coluna para renomea-la.

### Tabela Fabricante 



Ap�s a carga de dados, v� na terceira op��o no menu canto esquerdo do Power BI, onde vemos as rela��es entre as tabelas. 

## TODO 2: arrumar as identifica��es autom�ticas abaixo
A rela��o entre as tabelas foi identificada automaticamente pelo campo Owner, conforme imagem abaixo

![relationshipscopy.](./images/relationshipscopy.png)

## TODO 2: Revisar a demo abaixo


## Measures (medidas) e Hierarquias

Volte para a primeira op��o no menu da esquerda, na aba de visualiza��es

Clique com o bot�o direito em "VENDAS" e escolha criar uma nova medida

![vendasmedida.](./images/vendasmedida.png)

Copie o c�digo abaixo na aba que aparecer:

> Valor da Nota = sum(FAT_Vendas[Preco])*sum(FAT_Vendas[Quantidade_Vendida])


Para criar uma hierarquia, basta arrastar uma coluna em outra, dentro da mesma tabela: 

Arraste NM_Produto para Nome_Departamento da tabela PRODUTOS

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