# Projeto 2 - Final

## Motivação e Contexto

> Lorem Ipsum

## Slides

### Apresentação Prévia
> [PDF](./slides/apresentacao_previa.pdf)

### Apresentação Final
> [PDF](./slides/apresentacao_final.pdf)

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
> Lorem Ipsum

## Evolução do Projeto
> Lorem Ipsum

## Perguntas de Pesquisa/Análise Combinadas e Respectivas Análises

### Perguntas/Análise com Resposta Implementada

#### Pergunta/Análise X
> * Quais os componentes químicos mais presentes nas receitas em cada região do mundo?
>   * VIEW QtdComponentesPorRegiao
> 
>   * ‘Korea’
>     *  Cholesterol
>     * L-Alanine
>     * Oleic acid
>     *  Nitrogen
>     * Sugars
>   * Agrupamento para todas as regiões também: Colesterol

Agrupamento para todas as regiões também: Colesterol

### Perguntas/Análise Propostas mas Não Implementadas

#### Pergunta/Análise X
> * Lorem Ipsum
>   
>   * Lorem Ipsum