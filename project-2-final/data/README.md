# data
Este diretório representa os arquivos de dados (bancos de dados primários e auxiliares) que foram usados no projeto. O diretório ```external``` contém dados de terceiros em formato usado para entrada na transformação. O diretório ```interim``` contém dados intermediários resultados das transformações. O diretório ```processed``` contém os dados finais que foram processados e usados para a realização do projeto. Por fim, o diretório ```raw``` contém os dados originais sem modificações e processamentos.

Muitos dos arquivos utilizados são muito grandes para o armazenamento do GitHub e, com isso, não foi possível armazená-los no GitHub.

# Git Large File Storage (LFS)
Uma alternativa para armazenar os dados foi o LFS. No entanto, no contexto do projeto, não foi possível armazenar os dados. Esse sistema apresenta um limite de 1GB de arquivos no total e, considerando o total das bases, não foi possível utilizar essa ferramenta.

Assim, os dados podem ser baixados a partir do seguinte [link]().

Para a execução dos notebooks de construção da base, os arquivos dessa pasta devem ser baixados e colocados dentro desse diretório ```data```. Isso não é necessário para a execução dos notebooks de SQL, porque os dados finais da base já estão disponíveis na subpasta ```processed```.
