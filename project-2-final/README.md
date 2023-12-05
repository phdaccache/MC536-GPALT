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
Lorem Ipsum

## Evolução do Projeto
Lorem Ipsum

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