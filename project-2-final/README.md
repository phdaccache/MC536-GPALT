# Projeto 2 - Final

## Motivação e Contexto

Num contexto global de alto acesso à informação livre e disponível pela internet, é essencial que saibamos utilizar essas informações para extrair dados brutos e realizar análises que sirvam para estudarmos possíveis padrões acerca de tópicos variados. Além disso, é importante que consigamos contribuir, utilizando estratégias de engenharia de dados, para que esses dados disponíveis se tornem, cada vez mais, dados de alta qualidade, sem inconsistências e bem organizados.

Tendo isso em vista, extraímos, para esse projeto, diversos dados relacionadas à alimentação. Os dados que extraímos foram encontrados na internet, são disponíveis gratuitamente e podem ser acessados neste mesmo diretório. Eles englobam dados relacionados a receitas (com ingredientes e quantidades), alimentos, componentes químicos desses alimentos, nutrientes presentes neles e recomendações nutricionais diárias recomendadas por órgãos de saúde.

Reunimos essas bases e montamos um dataset que integrasse todas elas. Com esses novos dados montados, fomos capazes de levantar e reunir, em modelos de bancos de dados, diversas informações que extraímos das bases utilizadas sem dados imprecisos e incorretos, sem recortes significativos dos dados originais, sem inconsistências, com padronizações de medidas e unidades e com uma documentação acessível e executável em ambiente [Jupyter](https://jupyter.org/).

Além de agruparmos e refinarmos essas informações, realizamos análises para tentarmos levantar alguns padrões sobre o contexto global, pessoal e químico sobre alimentação. Realizamos, primeiramente, análises num modelo de banco de dados relacional utilizando a linguagem de consulta SQL.

Além disso, também criamos um banco de dados em grafos para podermos realizar análises que são mais apropriados nesse modelo. Essas análises foram importantes também para mostrarmos a flexibilidade de nossos dados, que facilmente podem ser convertidos em diversos modelos de bancos de dados, para que, por exemplo, mais análises se tornem possíveis. As análises realizadas, nos dois modelos citados, estão documentadas no repositório.

## Slides

### Apresentação Prévia
Estes slides representam a proposta original do projeto.

[PDF](./slides/apresentacao_previa.pdf)

### Apresentação Final
Estes slides representam o resultado final do projeto.

[PDF](./slides/apresentacao_final.pdf)

### Vídeo da apresentação (link do YouTube)
[![Apresentação Projeto Final GPALT](./assets/video_cover.png)](https://www.youtube.com/watch?v=Owbyjcj-Lg4&feature=youtu.be "Apresentação Projeto Final GPALT")

## Modelo Conceitual

![Modelo Conceitual ER](./assets/modelo_conceitual_er.png)

## Modelos Lógicos

### Modelo Lógico Relacional

~~~
ORIGEM(_Nome_, Tipo)

RECEITA(_Id_, _BancoOriginal_, Nome, Origem)
	Origem chave estrangeira -> ORIGEM(Nome)

INGREDIENTE(_Nome_, Classificacao)
	Classificacao chave estrangeira -> CLASSIFICACAO(Nome)

INGREDIENTECOMPOSTO(_IngredienteComposto_, _IngredienteOriginal_)
	IngredienteComposto chave estrangeira -> INGREDIENTE(Nome)
	IngredienteOriginal chave estrangeira -> INGREDIENTE(Nome)

SABOR(_Id_, Ingrediente1, Ingrediente2, Quantidade)
	Ingrediente1 chave estrangeira -> INGREDIENTE(Nome)
	Ingrediente2 chave estrangeira -> INGREDIENTE(Nome)

CLASSIFICACAO(_Nome_, CategoriaSuperior)

COMPONENTE(_Id_, _Tipo_, Nome)

ORGAOPUBLICO(_Nome_)

INGREDIENTESDASRECEITAS(_IdReceita_, _Banco_, _Ingrediente_, _Unidade_, Quantidade)
	(IdReceita, Banco) chave estrangeira -> RECEITA(Id, BancoOriginal)
    Ingrediente chave estrangeira -> INGREDIENTE(Nome)

COMPONENTESDOSINGREDIENTES(_Ingrediente_, _IdComponente_, _Tipo_, _Unidade_, Quantidade)
	Ingrediente chave estrangeira -> INGREDIENTE(Nome)
	(IdComponente, Tipo) chave estrangeira -> COMPONENTE(Id, Tipo)

RECOMENDACAO(_Orgao_, _IdComponente_, _Tipo_, _FaixaEtaria_, QuantidadeMg)
	Orgao chave estrangeira -> ORGAO(Nome)
	(IdComponente, Tipo) chave estrangeira -> COMPONENTE(Id, Tipo)
~~~

### Modelo Lógico de Grafos

![Modelo Lógico de Grafos](./assets/modelo_logico_grafos.png)

## Dataset Publicado

título do arquivo/base | link | breve descrição
----- | ----- | -----
origem | [origem.csv](./data/processed/database/origem.csv) | Locais de origem das receitas
receita | [receita.csv](./data/processed/database/receita.csv) | Receitas com suas origens e bancos originais
ingrediente | [ingrediente.csv](./data/processed/database/ingrediente.csv) | Ingredientes com suas respectivas classificações
ingredientecomposto | [ingredientecomposto.csv](./data/processed/database/ingredientecomposto.csv) | Composição de ingredientes formados por pelo menos 2 ingredientes
sabor | [sabor.csv](./data/processed/database/sabor.csv) | Quantidade de componentes em comum entre dois ingredientes
classificacao | [classificacao.csv](./data/processed/database/classificacao.csv) | Classificações e seus subtipos
componente | [componente.csv](./data/processed/database/componente.csv) | Componentes dos ingredientes (componentes químicos e nutrientes)
orgaopublico | [orgaopublico.csv](./data/processed/database/orgaopublico.csv) | Nome do órgão público responsável pelas recomendações
ingredientesdasreceitas | [ingredientesdasreceitas.csv](./data/processed/database/ingredientesdasreceitas.csv) | Ingredientes e suas quantidades para cada receita
componentesdosingredientes | [componentesdosingredientes.csv](./data/processed/database/componentesdosingredientes.csv) | Componentes, seus tipos e quantidades para cada ingrediente
recomendacao | [recomendacao.csv](./data/processed/database/recomendacao.csv) | Recomendações de quantidades dos componentes separadas por faixa etária

## Bases de Dados
título da base | link | breve descrição
----- | ----- | -----
FooDB | [link](https://foodb.ca/) | Dados sobre alimentos, sua química, seus ingredientes e nutrientes.
Flavor network and the principles of food pairing | [link](https://doi.org/10.1038/srep00196) | Artigo que disponibiliza dados sobre diversos sabores, além de uma lista de receitas por região do mundo.
RecipeNLG | [link](https://recipenlg.cs.put.poznan.pl/) | Receitas e as devidas quantidades dos ingredientes utilizados em cada uma delas.
CulinaryDB | [link](https://cosylab.iiitd.edu.in/culinarydb/) | Dados de receitas e ingredientes associados a 22 regiões do mundo diferentes.
Nutrient Recommendations: Dietary Reference Intakes (DRI) | [link](https://ods.od.nih.gov/HealthInformation/nutrientrecommendations.aspx) | Recomendações diárias de consumo de diversos nutrientes, divididos por faixa etária.

## Detalhamento do Projeto

##### Convertendo dados disponíveis online

Inicialmente, foi necessário extrair os dados da página web da base [DRI](https://ods.od.nih.gov/HealthInformation/nutrientrecommendations.aspx), pois esses dados estão apenas disponíveis na forma de tabelas sem nenhum modelo lógico. Como os dados de componentes e nutrientes da base do FooDB estão, em sua grande maioria, disponibilizados todos com medidas de massa (miligramas, gramas, ...), houve um cuidado nessa etapa de realizar as conversões necessárias a partir dos dados disponíveis para que todas as medidas estivessem em miligramas.

O tratamento das medidas, principalmente considerando as unidades, foi essencial para produzir um dataset que atingisse os objetivos propostos. Um exemplo dessa conversão pode ser visto no seguinte trecho do código em python utilizado, que mapeava diferentes medidas para referências em litros e kg, respectivamente:

~~~python
weight = {
        "gram": 0.001,
        "ounce" : 0.0283495,
        "pond" :  0.45359237,
        "kilogram" : 1,
    }
volumn = {
        "cup": 0.236588,
        "tablespoon" : 0.0147868,
        "teaspoon" : 0.00492892,
        "quart": 0.946353,
        "galon": 3.78541,
        "liters": 1,
        "mililiter": 0.001,
        "can": 0.3548824,
        "stick": 0.12,
        'pint': 0.473176,
    }
~~~

##### Integrando ingredientes

Em relação ao processo de integração das bases, houve um cuidado especial na integração de ingredientes diferentes de outras bases. A elaboração de um único arquivo csv `associacaofinal.csv`, que pode ser baixado na versão completa da pasta `data`, foi crucial para integrar informações de bases distintas.

Nesse caso, esse arquivo foi elaborado em duas colunas, `nome_ingrediente`, que representa o nome de algum ingrediente em qualquer uma das bases de receitas em letras minúsculas, e `nome_foodb`, que representa o nome do ingrediente na base do FooDB. É importante ressaltar, também, que há menções a ingredientes compostos da base do CulinaryDB nesse arquivo.

A consideração de apenas letras minúsculas na associação de ingredientes, com subsequente conversão dos nomes de todos ingredientes originais das bases para letras minúsculas possibilitou uma integração ainda maior.

Esse processo de integração dos nomes dos ingredientes foi feito de maneira completamente manual. Mais detalhes sobre esse processo estão disponíveis no notebook Jupyter `00`.

##### Tratamento e transformação de dados sobre quantidades

Nas bases consideradas, grande parte das receitas têm informações sobre quantidades dos ingredientes associados a cada uma delas. No entanto, esses dados estão disponíveis dentro de uma única string, contendo dados sobre a quantidade, a unidade (não padronizada) e o nome do ingrediente.

Para construir um dataset mais rico, foi necessário tratar esses dados. Assim, um processo cuidadoso de tratamento de dados foi feito em Python para separar unidades, quantidades e ingredientes desses dados da forma como foi proposto nos modelos.

Houve um cuidado grande em converter as medidas de, por exemplo, `1 cup` para algo quantificável de maneira mais fácil: `236.588 mililitros`. Isso tem o objetivo de padronizar melhor as unidades e quantidades do dataset, o que facilita análises e pesquisas sobre esses dados.

~~~
"1/2 cup canola oil, divided"
               |
               V
(ingrediente, quantidade, unidade)
"canola oil","118.294","mililitro"
~~~

##### Lidando com informações inconsistentes

No processo de construção do dataset, foi possível identificar algumas informações inconsistentes nas bases originais.

A base do FooDB, por exemplo, associa alguns componentes a ingredientes que não estão catalogados em lugar nenhum. Algumas informações sobre categorias dos ingredientes também apresentam algumas inconsistências.

Um tratamento foi realizado em todos esses dados.

##### Notebooks Jupyter

Todo esse processo discutido está mais detalhado em notebooks Jupyter, disponíveis na pasta `notebooks`.

Foram elaborados `7` notebooks de processamento dos dados originais para dados intermediários e `2` notebooks detalhando a construção final do dataset, integrando dados intermediários, além de outro notebook realizando análises em SQL.

Os dados do dataset final estão disponíveis em `data/processed/database`. Os dados originais da base, bem como intermediários, estão disponíveis no seguinte [link](https://drive.google.com/drive/folders/1HDvjRKjUg5BNV-Lmlv3nzuP9vkPdmGYo?usp=sharing) (também disponível no README da pasta data).

O processo cuidadoso de tratamento de dados permitiu integrar a maior quantidade possível de dados e construir um dataset final com informações úteis para análises sofisticadas.

## Evolução do Projeto

A modelagem cuidadosa na primeira etapa do projeto foi indiscutivelmente necessária para o andamento do projeto. Ao se saber exatamente onde se deseja chegar, basta apenas pensar no passo a passo de como fazer isso.

As principais dificuldades enfrentadas estão relacionadas à grande quantidade de dados. O projeto inteiro foi elaborado para ser executado no [BeakerX](http://beakerx.com/), mas mesmo executando os arquivos localmente houve grande dificuldade em lidar com os dados.

A execução do BeakerX via [Docker](https://www.docker.com/) foi a maneira de construção do dataset final e das análises. O sistema permite aumentar, manualmente, o Heap Size. Os notebooks foram executados com aproximadamente `6 GB`, por ser o limite que os computadores conseguiam tolerar. Mesmo assim, em alguns casos, houve diversos problemas de 'Out of memory'.

As soluções encontradas para isso foram diversas, e a discussão de cada um dos pontos onde houve problemas, bem como as soluções elencadas e a escolhida, são discutidos em mais detalhes nos notebooks. Em linhas gerais, as soluções foram, principalmente, realizar os comandos de ler CSV e filtrar os dados concomitantemente:

~~~SQL
SELECT ...
FROM CSVREAD('...')
WHERE/GROUP BY ...;
~~~

Simplificadamente, essa construção permite filtrar os dados à medida que eles estão lendo lidos dos arquivos CSV, o que evita que todos esses dados sejam importados. Mesmo assim, o tamanho do Heap precisou ser aumentado consideravalmente, principalmente para as análises com o dataset final, que contém mais de `1.8` milhão de associações entre ingredientes e as diversas receitas.

Para as análises disponibilizadas, há o seguinte filtro na importação desses dados:

~~~SQL
WHERE UNIDADE <> 'desconhecida'
      AND UNIDADE <> 'unidade'
      AND ID < 25000;
~~~

Assim, a visualização dos dados no notebook `09` considera apenas a importação de receitas cuja unidade esteja definida em `gramas` ou em `mililitros` e receitas com ID no máximo `25000`.

Os resultados com todos os dados finais do dataset podem ser vistos, claramente, apagando essa linha dos imports iniciais. No entanto, as operações de análise são custosas e podem demorar e requerer um alto Heap Size.

O modelo final também sofreu algumas alterações, que dizem respeito a principalmente associar receitas a partir do ID, e não pelo nome. Alguns nomes de receitas são muito extensos, e a propagação de dados tão extensos foi evitada justamente para que os arquivos do dataset ocupassem menos memória. Ao se utilizar um ID, o valor não ultrapassa mais de 5 dígitos.

~~~
"Cuban Via Miami Feast: Mashed Plantains with Oh, Baby!
 Garlic-Tomato Shrimp on Top, Grilled Flank Steak with
 Lime and Onions, Quick Rice with Black Beans"
                      |
                      V
                   "20805"
~~~

Assim, as principais dificuldades encontradas estão associadas a como lidar com grandes quantidades de dados. Em relação aos processamentos em Python relacionados, houve uma necessidade de dividir as entradas da base do RecipeNLG, que está disponível em um único arquivo csv com mais de 2GB de tamanho.

Essa divisão permitiu que os processamentos não importassem todos os dados em memória diretamente, e foi a solução para tratar as quantidades, que precisavam de tratamento.

Os detalhamentos de dificuldades e soluções pensadas, escolhas durante o processo e explicações estão disponíveis em todos os notebooks Jupyter. Houve um cuidado grande em documentar bem todo o processo, e em mantê-lo reproduzível.

Assim, caso alterações sejam realizadas em qualquer um dos notebooks, basta apenas executá-los todos na ordem em que aparecem para reconstruir o dataset como desejado e realizar as análises.

## Perguntas de Pesquisa/Análise Combinadas e Respectivas Análises

### Perguntas/Análise com Resposta Implementada Modelo Relacional

#### Pergunta/Análise 1

* Quais os componentes químicos mais presentes nas receitas em cada região do mundo?
  * VIEW QtdComponentesPorRegiao

  * ‘Korea’
    *  Cholesterol
    * L-Alanine
    * Oleic acid
    *  Nitrogen
    * Sugars
  * Agrupamento para todas as regiões também: Colesterol

#### Pergunta/Análise 2

* Quais são as regiões do mundo que utilizam mais de um certo ingrediente?
  * Análise por frequência
  * VIEW MaiorUsoAlhoRegioes

  * ‘Garlic’
    * NorthAmerican
    * SouthernEuropean
    * LatinAmerican
    * EastAsian
    * Indian Subcontinent

#### Pergunta/Análise 3

* A partir de uma necessidade alimentar de componentes químicos, quais são os pratos que têm ingredientes com as maiores quantidades de todos eles?
  * VIEW ComponentesDasReceitas

  * Menos de 2000 mg de Sodium - VIEW ReceitaSodio
  * De 0.01 mg a 0.03 mg de Vitamin D - VIEW ReceitaVitaminaD

  * Considerar separadamente e depois pegar a interseção entre as views
    * ID 2616, CulinaryDB - Congo Tofu
    * ID 3076, CulinaryDB - Easy Moo Shu Pork
    * ID 3558, CulinaryDB - Goat Shoulder Braised with Prunes and Preserved Lemons
    * ID 3847, CulinaryDB - Vietnamese Style Vegetarian Curry Soup
    * ID 4172, CulinaryDB - Spicy Goat Curried Rice Pilaf

#### Pergunta/Análise 4

* Quanto é necessário consumir de um alimento X para conseguir uma quantidade Y de um nutriente?
  * VIEW ComponentesDasReceitas (de novo)

  *Nutriente: ‘Proteins’
  *Quantidade: 10000 mg
  *Receita: ID 6220, RecipeNLG (Sugar-Free Apple Pie)

  *Necessidade
    * 7.81 receitas

#### Pergunta/Análise 5

* Dado um grupo de classificação de ingredientes, qual país tem mais receitas com ingredientes desse grupo?
  * Análises por frequência total e por porcentagem
  * VIEW FreqGrupoIngredientesPorRegiao
  * VIEW PorcentagemClassificacaoPorPais

  * Categoria: ‘Herbs’
    * Frequência e porcentagem apresentaram resultados diferentes
    * Quantidade de receitas disponível influencia os dados - qual a métrica mais adequada?

#### Pergunta/Análise 6

* Qual região do mundo é mais propensa a ter problemas de altos consumos de sódio?
  * VIEW NaMedioPorRefeicaoEmMgPorRegiao
  * Recomendações do NIH-US

  * A média de sódio em uma receita de cada região ultrapassa a recomendação máxima permitida?
    * Em geral, SIM!
    * Estima-se que mais de 2 milhões de pessoas morrem, por ano, devido a altos consumos de sódio

### Perguntas/Análise com Resposta Implementada Modelo de Grafos

#### Pergunta/Análise 1

* Quais são os ingredientes mais centrais nas culinárias de diferentes regiões do mundo?

#### Pergunta/Análise 2

* É possível definir grupos de alimentos que caracterizam a culinária de uma região do mundo?

### Perguntas/Análise Propostas mas Não Implementadas

#### Pergunta/Análise 1

* Quais os componentes químicos mais presentes na dieta média de um morador de um país X? E os menos presentes?
  * Analisando as principais receitas de um país específico, é possível fazer uma estimativa do consumo nutricional médio, mostrando os pontos de maior déficit nutricional do local

#### Pergunta/Análise 2

* Quais são os países com as alimentações mais balanceadas nutricionalmente? E quais são os com as menos balanceadas?
  * Analisando o banco de dados é possível ter uma estimativa média nutricional dos países e com isso podemos comparar o padrão alimentar de diversos países diferentes

#### Pergunta/Análise 3

* Os pares de ingredientes mais comuns em uma determinada região do mundo se complementam nutricionalmente?
  * Com essa análise é possível entender como os sabores principais de uma culinária são formados e em como eles impactam nutricionalmente a dieta de uma região.

#### Pergunta/Análise 4

* Quais os componentes químicos presentes nos sabores mais comuns ao redor do mundo?
  * Com a análise é possível entender melhor que forma os principais sabores do mundo são compostos.
