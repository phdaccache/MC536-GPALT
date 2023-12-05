# Executando os notebooks

Os notebooks podem ser executados diretamente a partir do [Docker](https://www.docker.com/), utilizando o [BeakerX](http://beakerx.com/).

Tendo o Docker instalado, após clonar o repositório localmente é possível executá-lo a partir do seguinte comando:

`sudo docker run -p 8888:8888 -v /home/your_home/git/MC536-GPALT/:/home/beakerx/MC536-GPALT beakerx/beakerx`

O caminho é o caminho até a pasta do repositório. Após executar esse comando, um link será gerado:

~
http://04d735361a78:8888/?token=8cfaf01d9c80f901ce0fac3146eeb0631313f5e97d5087d3&token=8cfaf01d9c80f901ce0fac3146eeb0631313f5e97d5087d3
~

Basta alterar a parte até o `:` por `localhost` e abrir em um navegador:

~
http://localhost:8888/?token=8cfaf01d9c80f901ce0fac3146eeb0631313f5e97d5087d3&token=8cfaf01d9c80f901ce0fac3146eeb0631313f5e97d5087d3
~
