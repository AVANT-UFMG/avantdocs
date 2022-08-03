---
layout: default
title: Avant Docker
parent: Projetos
nav_order: 1
---

# O projeto avant docker
## _Um ambiente para execução dos projetos da equipe_

Avant Docker é um ambiente personalizado com todas as dependências que a equipe
de eletrônica utiliza para testar e desenvolver software para os drones projetados.

## Por que um ambiente comum?

Na Avant, utilizamos muitos softwares que precisam de um passo a passo rigoroso no 
momento da instalação, qualquer erro pode acabar fazendo com que a instalação seja 
incompleta e o sistema não funciona de maneira correta. Além disso, pessoas diferentes
possuem dispositivos diferetes, e portanto, configurações diferents. Isso é um outro
fator que pode gerar instalações e ou configurações adicionais, ou seja, mais dor 
de cabeça. O avant docker vem para resolver esses problemas, visto que todos da 
equipe podem utilizar o mesmo ambiente com as configurações exatamente iguais.

## Instalação

Avant docker é um container [Docker](https://docs.docker.com/engine/install/), e é tudo que precisa ser instalado. 
Para versionamento de código, pode ser útil instalar o [GIT](https://git-scm.com/downloads).

## Executando o ambiente

Avant docker precisa de algumas configurações para conseguir funcionar, 
mas fique tranquilo, um [script shell](https://drive.google.com/file/d/1nmPV8-XFz_oHwHe2R3quh9qZFqyGAVC3/view?usp=sharing) já foi feito para facilitar sua vida.

Para obter a imagem do Docker basta fazer:
```
sudo docker pull avantufmg/avant_ros-full:latest
```
Para executar o container, apenas digite:
```
sudo ./run.sh --OPÇÃO
```

| Opção | Desrição |
| :---: | :---:    |
|focal  | Utiliza a placa de vídeo do seu computador para renderizar aplicações |
|focal-nogpu | ***Não*** utiliza a placa de vídeo para renderizar aplicações |

***Atenção:*** Não se confunda, o docker avant vai renderizar as interfaces gráficas
independentemente da opção escolhida, aqui você escolhe somente ***COMO*** ele fará isso.
## Permanência de dados

Containers docker são feitos para serem efêmeros, e por isso, não podemos armazenar
nada dentro deles, já que, mais cedo ou mais tarde, eles deixarão de existir.

Não se preocupe, GIT vem para te salvar.

Containers Docker possuem a habilidade de criar um volume na sua máquina, ou seja, permitem sincronizar diretórios entre o host e o container. Se você cria um volume em seu computador, tudo que for alterado nesse volume será alterado dentro e fora do container, e isso vai para ambos os lados: Se você alterar o volume em seu computador, o mesmo volume se altera dentro do container, e se você altera um volume dentro do container, o mesmo volume se altera dentro do seu computador.

Dessa maneira, se o volume também for um repositório GIT, você pode subir o container de forma limpa e, quando ele subir, os dados nesse diretório serão importados para dentro do container. Se modificar esses arquivos durante o desenvolvimento do código e quiser salvar essas modificações, você pode usar o GIT na sua própria máquina para manter o versionamento do volume. 

## Mas como eu crio um volume?

Isso é muito simples, o script de execução já faz isso para você, uma vez que ele aceita parametros adicionais. Para criar um volume basta fazer o seguinte:

```
sudo ./run.sh --OPÇÃO --run-args "-v /CAMINHO/HOST:/CAMINHO/CONTAINER"
```

***Atenção:*** Os caminhos passados precisam sem caminhos completos (absolutos), e não se preocupe se o diretório não existir dentro do container, ele será criado automaticamente!
