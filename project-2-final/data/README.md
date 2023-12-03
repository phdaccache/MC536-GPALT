# data
Este diretório contém os arquivos de dados (bancos de dados primários e auxiliares) que foram usados no projeto. O diretório ```external``` contém dados de terceiros em formato usado para entrada na transformação. O diretório ```interim``` contém dados intermediários resultados das transformações. O diretório ```processed``` contém os dados finais que foram processados e usados para a realização do projeto. Por fim, o diretório ```raw``` contém os dados originais sem modificações e processamentos.

Como alguns arquivos utilizados eram muito grandes (+300MB), utilizamos o Git Large File Storage para armazená-los eficientemente. Uma breve introdução e um breve tutorial sobre esse método serão apresentados.

# Git Large File Storage (LFS)
Git Large File Storage substitui arquivos que ocupam grandes tamanhos de memória em um repositório Git, como os bancos de dados originais que estão em ```./raw```, por arquivos de texto que funcionam como ponteiros dentro do repositório. O conteúdo dos arquivos é guardado em servidores remotos para que a manutenção e clonagem do repositório permaneça eficiente. 

A seguir, mostraremos como podemos instalar o Git LFS em distribuições Linux como Ubuntu e Debian para substituirmos os ponteiros que estão no diretório pelo conteúdo original dos arquivos, que estão armazenados nos servidores do Git LFS. Mais informações sobre o Git LFS e sobre a instalação em mais sistemas operacionais podem ser encontradas no [site oficial](https://git-lfs.com/).
#Instalação:
Execute o seguinte comando no terminal para instalar o Git LFS:
```console
$ sudo apt-get install git-lfs
```
Após isso, execute o seguinte comando para ativar o Git LFS:
```console
$ git lfs install
```
Dentro de um repositório usando Git LFS, alguns arquivos serão apenas ponteiros para os arquivos originais. Por exemplo, os arquivos em ```./raw``` são ponteiros. Com Git LFS instalado, podemos obter os arquivos originais executando o seguinte comando no repositório:
```console
$ git lfs pull
```
Esse comando irá obter os arquivos originais do repositório. Os arquivos estarão na localização original, e os ponteiros sumirão.
