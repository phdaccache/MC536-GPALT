# notebooks
Este diretório contém os notebooks em Jupyter para construção dos dados da base final, bem como para análises em SQL.

A numeração dos arquivos representa a ordem em que eles devem ser executados para construir os dados e realizar as análises. No entanto, os notebooks até o `08.02-GPALT-final-data.ipynb` (incluso) não precisam necessariamente ser executados, pois o repositório já contém os arquivos finais deles.

# Construção dos dados
Os primeiros notebooks são responsáveis por realizar a integração dos dados originais para formar o dataset final. Eles alternam comandos de Python e SQL.

Em alguns notebooks, a biblioteca Pandas é utilizada. Mais informações sobre essa biblioteca, bem como guias de instalação, podem ser encontrados no [site oficial](https://pandas.pydata.org/).

Como um dos objetivos do projeto é explorar recursos de Bancos de Dados e Queries, sempre que possível as construções são feitas em SQL. Nesse caso, quando necessário as bases apenas são pré-processadas em Python para permitir o uso de SQL mais fácil.

# Análises
As análises propostas sobre os dados finais seguem as perguntas elaboradas originalmente e exploram unicamente queries em SQL. O detalhamento de cada uma delas está presente no notebook de análises.
