# Projeto 2 - Final

## Motivação e Contexto

Lorem Ipsum

## Slides

### Apresentação Prévia
[PDF](./slides/apresentacao_previa.pdf)

### Apresentação Final
[PDF](./slides/apresentacao_final.pdf)

### Vídeo da apresentação
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
origem | [origem.csv](./data/processed/database/origem.csv) | Lorem Ipsum
receita | [receita.csv](./data/processed/database/receita.csv) | Lorem Ipsum
ingrediente | [ingrediente.csv](./data/processed/database/ingrediente.csv) | Lorem Ipsum
ingredientecomposto | [ingredientecomposto.csv](./data/processed/database/ingredientecomposto.csv) | Lorem Ipsum
sabor | [sabor.csv](./data/processed/database/sabor.csv) | Lorem Ipsum
classificacao | [classificacao.csv](./data/processed/database/classificacao.csv) | Lorem Ipsum
componente | [componente.csv](./data/processed/database/componente.csv) | Lorem Ipsum
orgaopublico | [orgaopublico.csv](./data/processed/database/orgaopublico.csv) | Lorem Ipsum
ingredientesdasreceitas | [ingredientesdasreceitas.csv](./data/processed/database/ingredientesdasreceitas.csv) | Lorem Ipsum
componentesdosingredientes | [componentesdosingredientes.csv](./data/processed/database/componentesdosingredientes.csv) | Lorem Ipsum
recomendacao | [recomendacao.csv](./data/processed/database/recomendacao.csv) | Lorem Ipsum

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