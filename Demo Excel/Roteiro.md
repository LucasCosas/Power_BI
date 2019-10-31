# Power BI - Passo a Passo para demonstração

## Configurar Power BI

Antes de começarmos, importante certificar de que o Power BI está em Português Brasileiro para o passo a passo abaixo.

Para isso, vá a File > Opções e Configurações > Opções

![GetConfig.](./images/options.png)

Verifique na aba Configurações Regionais se o idioma está em Português Brasileiro.

![GetConfigreg.](./images/configreg.png)

## Get Data (Obter Dados)

Para o workshop, primeiramente navegue até o link abaixo
https://github.com/LucasCosas/Power_BI/blob/master/Demo%20Excel/_OLD/Dados.xlsx.

Clique em "Download" e salve o arquivo de excel no diretório C:/ArquivoExcel

No Power BI Desktop, vá para GetData e escolha a conexão de Arquivo de Excel

![GetData.](./images/getdata.png)
![GetDataExcel.](./images/getdataexcel.png)

Procure a tabela de Excel no diretório salvo no passo anterior.

O Power BI encontrará, dentro do arquivo do Excel, algumas tabelas que podem ser utilizadas para carregar os dados dentro do modelo.

Note que podemos clicar em alguma das tabelas e visualizar um preview dos dados que serão carregados.

Neste caso, utilizaremos apenas os dados formatados nas abas dentro do arquivo excel:

Na caixa de seleção, escolha:

* *Localizacao*
* *Fabricante*
* *Vendas* 
* *Produtos*


![tabelasexcel.](./images/tabelasexcel.png)


Clique em "Transformar Dados" após selecionar as tabelas acima. 

Caso as tabelas já estejam carregadas, pode-se ir ao menu de edições clicando em Editar Consultas do menu superior na página principal do Power BI

# Edit Queries (Editar Consultas)

Editar Consultas é o lugar onde você fará as edições nas tabelas que serão feitas as cargas para o modelo do Power BI. É importante fazer as modificações necessárias antes da criaçao das visualizações.

### Tabela Vendas

Alterar os tipos de dados das colunas:

Para alterar, clique no símbolo que aparece ao lado esquerdo da coluna, exemplo abaixo.

![alterandodate.](./images/alterandodate.png)

Date: Alterar para Data.
Valor Base: Decimal Fixo.

### Tabela Localização

Selecione a tabela Endereço. Na aba Transformar do menu superior, escolha Dividir Coluna por Delimitador

![delimitador.](./images/delimitador.png)

Na tela que abrir, escolha delimitador de vírgula e clique OK.

Renomeie a coluna Endereço.1 para Cidade e Endereço.2 para Estado. Clique com o botão direito em cima do nome da coluna para renomea-la.

### Tabela Fabricante 

A coluna Fabricante está num formato onde as colunas são as linhas, portanto, precisamos transpor os dados.

Na aba de Transformação, clique em Transpor:

![transpor.](./images/transpor.png)

Clique também em "Usar a Primeira Linha como Cabeçalho".

A Tabela ficará parecida com isso:

![fabricante.](./images/fabricante.png)

Volte para a Aba "Página Inicial" no menu superior e clique em "Fechar e Aplicar"

Isso fará com que as Mudanças nas Consultas sejam aplicadas no Modelo para visualizações.


# Relacionamento das Tabelas

Na página principal do Power BI, escolha a terceira opção do menu lateral esquerdo, para ver as relações entre as tabelas.

As relações entre as tabelas foi identificada automaticamente pelo campo CEP (Localização) e ID (Produto), conforme imagem abaixo

![relationshipspower.](./images/relationshipspower.png)

Porém, a relação entre Fabricante e Produtos não foi identificada. Para tanto, podemos fazê-la de duas formas diferentes:

A primeira é simplesmente clicar no campo "ManufacturerID" e arrasta-lo até "Fabricante - No".

Outra forma, no menu superior, procurar por "Gerenciar Relações" e criar a nova relação na caixa de diálogo.

Resultado esperado:

![relacionamento.](./images/relacionamento.png)

# Measures (medidas) e Hierarquias

Volte para a primeira opção no menu da esquerda, na aba de visualizações

Clique com o botão direito na tabela "Vendas" e escolha criar uma "Nova Coluna"

![vendascol.](./images/vendascol.png)

Copie o código abaixo na aba que aparecer:

> Valor da Nota = Vendas[Valor Base] * Vendas[Unidades]

Isso criará uma Coluna na tabela, que multiplica a quantidade de unidades vendida pelo valor base de cada unidade, resultando no preço final da Nota.

Para criar uma nova Medida, clique com o botão direito na tabela Vendas e "Nova Medida".

Copie o código abaixo e cole na aba que aparecer:

> Valor Total de Vendas = Vendas[Valor da Nota]

Isso criará uma medida que agrega todos os valores das notas, para calcular o valor total das vendas num determinado período ou por um produto específico.


Para criar uma hierarquia, basta arrastar uma coluna em outra, dentro da mesma tabela: 

Na tabela Produtos, arraste Produto para Fabricante, criando uma hierarquia entre Fabricante > Produto.

![hierarquia.](./images/hierarquia.png)

Para o Power BI então qual o tipo da coluna de localização, precisaremos colocar labels em cada coluna:

Na tabela Localização, clique na coluna CEP, procure por Categoria de dados e selecione CEP na lista suspensa:

![cep.](./images/cep.png)

Faça o mesmo para as seguintes colunas:

* * Cidade: Cidade *
* * Estado: Estado ou Província *
* * País: País/Região *


# Visualizações

## Objetivos da visualização:

Descubra quem é o melhor vendedor com filtro de departamento e de data.
Qual produto tem a maior venda? E qual tem o menor?


## Criar visualização

Na área de VISUALIZAÇÕES, escolha a visualização para colocar filtros (a primeira opção da 5ª linha, da área de visualizações), depois, procure a coluna DateTime da tabela DIM_DATA e selecione o checkbox.

Clique fora da visualização criada e adicione um novo filtro, com NM_Departamento desta vez.

Clique novamente fora da visualização criada acima e selecione o gráfico de colunas empilhadas.

Escolha a medida calculada criada no passo anterior (Valor da nota) e coloque-a no campo de Valor(coluna), se apenas clicar no checkbox, o Power BI entende essa coluna como numérica e faz isso por você. No campo de eixo, adicione o nome dos vendedores da tabela DIM_Vendedores. Novamente, apenas clicar no checkbox funciona automaticamente.

Com os passos acima podemos filtrar datas e departamentos para descobrir quem vendeu mais nas datas e departamentos escolhidos.

Adicione outro gráfico de colunas, desta vez, o gráfico de colunas empilhadas e linha. Selecione valor da nota e nm_produto.

Na linha de valor, escolha a coluna Target_Value da tabela FAT_Target.

Agora podemos modificar com o filtro de data para alterar as visualizações criadas.

A partir daí, o céu é o limite.


# Publicação e compartilhamento

Após criar as visualizações, clique em "Publicar" no menu inicial do Power BI

Quando abrir a caixa de diálogo, coloque seu email corporativo e senha.

Escolha o espaço de trabalho pessoal e publique.

Clique no link para visualizar o relatório no site ou abra o "msit.powerbi.com"

Na opção "Arquivo" podemos compartilhar este relatório na web ou SharePoint. Na opção "Compartilhar" podemos compartilhar com um grupo ou usuário específico.

## Teams

Abra o Teams na aba de teams. Escolha um time que gostaria de compartilhar o relatório criado e clique no sinal "+". Procure por Power BI na área de adicionar uma aba.	 Selecione o espaço de trabalho em que o relatório foi publicado e selecione-o.

# Atualizando o relatório

Por fim, para atualizar o relatório no site do Power BI, podemos navegar até o espaço de trabalho, na área esquerda, procurar por Data Sources/Conjuntos de Dados, clicar na reticências ao lado do conjunto de dados e clicar em "Atualizar Agora".

Note que este passo só funcionará se o arquivo utilizado estiver em algum serviço online como SharePoint. Se estiver na máquina física, será necessário publica-lo novamente a partir do Power BI Desktop ou criar um gateway(não recomendável).