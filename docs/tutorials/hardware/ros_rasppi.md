---
layout: default
nav_order: 1
parent: Hardware
title: Instalar ROS no Raspberry Pi
---

# Instalar ROS no Raspberry Pi
## Requisitos
Para completar esse tutorial, você vai precisar de:
- Computador/Notebook
- Raspberry Pi (qualquer um dos modelos 2/3/4/400)
- Cartão micro SD
    - Class 10 (recomendável, por ser mais rápido, mas não obrigatório)
    - Mínimo: 4 GB para Ubuntu Server, 8 GB para Ubuntu Mate; recomendável: 16 GB ou 32 GB
- Adaptador de cartão micro SD para conectá-lo ao seu computador

## Instalando o OS adequado
O sistema operacional padrão do Raspberry Pi é o Raspbian, uma distribuição baseada no [Debian](https://www.debian.org/) especialmente pensada para o Raspberry. Mas rodar e gerenciar os pacotes do ROS no Raspbian pode dar dor de cabeça. Por isso, o primeiro passo recomendado é instalar uma versão do Ubuntu (outra distribuição baseada no Debian), suportada nativamente pelo ROS, no seu Raspberry.

Para isso, temos duas opções. 

1) Se você quer um sistema operacional completo, isto é, se pretende desenvolver no Raspberry Pi, sugerimos o [Ubuntu Mate](https://ubuntu-mate.org/), que tem uma versão própria para o Raspberry.

2) Se você quer uma versão mínima, ou seja, se vai só botar o Raspberry Pi no robô, então é melhor usar o [Ubuntu Server](https://ubuntu.com/tutorials/install-ubuntu-server#1-overview).

### Ubuntu Mate
**TODO**

### Ubuntu Server
#### 22.04
A forma mais fácil de instalar o Ubuntu Server é usando o Raspberry Pi Imager. Para instalá-lo no Linux, digite

```
sudo apt install snap   # instala o snap, caso não esteja instalado
sudo snap install rpi-imager
```

Se a instalação for bem sucedida, abra o Raspberry Pi Imager.

![Tela inicial do Raspberry Pi Imager](/avantdocs/assets/images/tutorials/ros_rasppi/imager_home.png)

Então, clique em `CHOOSE OS` e escolha o Ubuntu Server 22.04 para arquiteturas `amd64` (o ROS Humble não suporta `amrhf`).

![Primeiro passo na escolha do sistema operacional](/avantdocs/assets/images/tutorials/ros_rasppi/imager_os_step1.png)

![Segundo passo na escolha do sistema operacional](/avantdocs/assets/images/tutorials/ros_rasppi/imager_os_step2.png)

![Terceiro passo na escolha do sistema operacional](/avantdocs/assets/images/tutorials/ros_rasppi/imager_os_step3.png)

Em seguida, insira seu cartão no micro SD no computador. Então, clique em `CHOOSE STORAGE` e selecione seu cartão micro SD para salvar o Ubuntu nele. Por fim, clique em `WRITE` e espere terminar.

Quando o Imager tiver terminado de escrever a imagem do Ubuntu no cartão micro SD, remova-o do computador e insira no Raspberry Pi. Então, ligue o Raspberry Pi e espere o Ubuntu carregar.

Depois que o sistema tiver iniciado, ele vai te pedir nome de usuário e senha para logar. O nome de usuário e senha que vêm por padrão são ambos `ubuntu`. Se for seu primeiro login, o sistema vai te pedir para mudar a senha. Depois de mudar a senha, terminou! Agora você tem um Raspberry Pi com Ubuntu Server 22.04! O próximo passo é instalar o ROS Humble.

#### 20.04
**TODO**

## Instalando o ROS
### ROS 1
**TODO**

### ROS 2
Para instalar o ROS Humble no Ubuntu Server, basta seguir as instruções no [site oficial](http://docs.ros.org.ros.informatik.uni-freiburg.de/en/humble/Installation/Ubuntu-Install-Debians.html) como se estivesse instalando no Ubuntu Desktop. Contudo, alguns comandos são muito grandes e chatos de digitar, o que pode resultar em erros. Por isso, recomendamos que use um script bash para instalar tudo. Baixe o script que fizemos [neste link](https://drive.google.com/uc?export=download&id=1gVz1G-KqCqOMb2CN7-0L-HLPz_UIy5Hd) (provavelmente, o Google vai te dar um aviso de segurança, mas pode confiar na gente). Ele recebe como primeiro parâmetro o nome da distribuição do ROS que você deseja instalar.

```
# Exemplo: instalar o ROS Humble
bash install_ros2.sh humble
```

Para executar o script no Raspberry Pi, salve-o num pen drive ou cartão SD e insira o dispositivo no qual o script foi salvo no Raspberry. No Ubuntu MATE, é fácil: basta usar a interface gráfica para mover o script do dispositivo de armazenamento para o Rasperry Pi e executá-lo. No Ubuntu Server, é um pouco mais complicado, por não haver interface gráfica. Então, primeiro execute o comando

```
lsblk
```

Ele vai listar um monte de coisa, mas o que te interessa são os que têm o tipo `disk` e tamanho igual ao do seu pen drive ou cartão SD. O nome que você procure `sda` ou `sdb`, e, possivelmente, com um número no final, como `sdb1`. Um exemplo está mostrado abaixo.

![Exemplo do lsblk](/assets/images/tutorials/ros_rasppi/find_drive.png)

Então, monte o dispositivo. **Esse exemplo assume que o nome do dispositivo é `sda`, troque pelo nome que você encontrou com o `lsblk`!**.

```
mkdir /media/usb
sudo mount /dev/sda /media/usb  # troque sda pelo nome que apareceu no seu computador!
```

Agora, tudo que estava salvo no pen drive/cartão SD está na pasta /media/usb. Então, para executar o script de instalação,

```
cd /media/usb                   # ir para a pasta
bash install_ros2.sh humble     # instalar o ros humble
```

Ele deve pedir para você confirmar algumas coisas com o teclado a longo do caminho. Quando terminar de instalar, você já vai ter o ROS 2 instalado e funcionando!

> **Importante**: esse script instala a versão básica do ROS 2, então não tem RViz, Gazebo, e nenhuma ferramenta com interface gráfica. Ele foi pensando para ser usado no Ubuntu Server, então não precisa dessas coisas. Se quiser instalar a versão desktop (a que todas essas ferramentas), use esse [script](https://drive.google.com/uc?export=download&id=1h29pv2KkwFuNNKKnq_X-4k9W9TIir0Vq).
