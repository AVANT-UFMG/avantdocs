---
layout: default
title: Guia de Aprendizado
nav_order: 2
---

# Guia de Aprendizado

Este guia apresenta referências externas para consulta sobre os mais variados temas relacionados às atividades que desenvolvemos. Os temas estão dividos de acordo com o uso em cada área da equipe.

# Introdução
Este documento tem o objetivo de reunir referências sobre os conteúdos necessários para o desenvolvimento das atividades na AVANT. As referências neste guia devem cobrir tanto o aspecto teórico quanto prático de cada área de conhecimento da Equipe de Eletrônica da AVANT. Nesse sentido, o material incluído aqui deve ser tal que seu estudo seja _suficiente_ para a formação básica dos membros da equipe. Além disso, _qualquer_ membro deve ser capaz de sugerir alterações, as quais devem ser revisadas pelo respectivo Líder Técnico.

# Progrmação para Iniciantes
Inevitavelmente, membros da Equipe de Eletrônica vão passar a maior parte de seu tempo programando. Seja para testar ideias em simulações ou implementá-las em robôs reais. Na robótica, as linguagens de programação mais utilizadas são Python e C++, cada uma mais adequada para cada situação. Enquanto o Python tem uma comunidade muito forte (você acha biblioteca de Python para quase qualquer coisa) e sua sintaxe simples e versatilidade permitem-nos implementar protótipos com muita rapidez, o C++ é mais eficiente em termos de tempo de execução, especialmente em hardware embarcado, o qual não costuma ser muito poderoso.

Se você nunca programou, recomendamos que comece pelo Python, pois é muito mais simples e vai te permitir focar no que interessa no começo: entender o que significa desenvolver software. Uma vez que se sinta confortável com o Python, comece a estudar o C++. Mas isso é apenas recomendação, sinta-se livre para fazer como considerar melhor para você.

## Python

- [Site com tutoriais de Python, do básico ao avançado [en]](https://www.learnpython.org/)
- [Curso de Python com videoaulas [pt]](https://www.youtube.com/watch?v=S9uPNppGsGo&list=PLvE-ZAFRgX8hnECDn1v9HNTI71veL3oW0)

## C++

- [Site com tutoriais de C++ [en]](https://www.learncpp.com/)

# Integração de Sistemas
A área de integração de sistemas atua com a comunicação entre uma controladora e um computador de bordo. Os modelos utilizados pela equipe são a Pixhawk e a Raspberry Pi. Além disso, também é responsável pela criação de uma interface que simplifique a comunicação da Pixhawk e dos sensores embarcados com o drone.

## Pixhawk
A Pixhawk é uma controladora de voo que possui os projetos de hardware e códigos abertos, possui função de voo autônomo, processador de 32 bits e sensores de navegação embutidos.

- [Site Oficial](https://pixhawk.org/)
- [PX4 User Guide (seções Introduction e Getting Started)](https://docs.px4.io/main/en/)
- [Vídeo curto sobre setup do ambiente da PX4 no Ubuntu](https://youtu.be/OtValQdAdrU)


## Raspberry Pi
A Raspberry Pi é um micro-computador completo e possui todos os seus componentes em uma única placa lógica: processador, memória RAM e placa de vídeo impressos. Também possui entradas USB, HDMI, entre outros. É um computador de bordo, visto que é um equipamento capaz de computar dados importantes para o funcionamento do VANT.

- [Site Oficial](https://www.raspberrypi.org/)

## MAVROS
A comunicação entre a controladora e o computador de bordo se dá a partir do Protocolo MAVLink. Porém, é uma implementação de baixo nível. Para simplificar um pouco essa tarefa, utilizamos um pacote do ROS chamado Mavros, que tem como objetivo fazer uma ponte entre o MAVLink e o ROS.

- [Pacote Mavros](http://wiki.ros.org/mavros)
- [Protocolo MAVLink](https://mavlink.io/en/)

# Navegação
A missão da equipe de navegação é tornar o drone capaz de navegar sozinho pelo ambiente. Isso inclui localização, planejamento e execução da trajetória planejada. Cada problema desse é uma área de pesquisa na robótica, por isso, dedicamos à cada um deles sua própria subseção.

## Localização
O problema de localização é um dos mais importantes na robótica, dada a dependência que qualquer algoritmo de planejamento tem de um bom sistema de localização. Apesar de ser possível utilizar GPS em alguns contextos, ele não serve para ambientes fechados, por exemplo, onde ocorrem muitas missões executadas por robôs. Dessa forma, o robô deve ser capaz de se localizar sem contar com informações externas. Para isso, várias metodologias foram propostas, das quais veremos as três das mais interessantes para o caso de drones.

### Odometria Visual
Odometria é um técnica de localização que estima a posição do robô com base no deslocamento. No caso de drones, podemos estimar o deslocamento a partir das imagens capturadas pela câmera.

- [Texto do Wikipedia [en]](https://en.wikipedia.org/wiki/Visual_odometry)
- [Apresentação aprofundada [en]](https://youtu.be/VOlYuK6AtAE)

Odometria visual é um tema bem complicado. Mas não precisamos nos preocupar tanto com a formalização matemática (se não quisermos), pois há bibliotecas que implementam isso para a gente. Uma muito famosa é o ORB-SLAM2.

- [Código fonte no GitHub](https://github.com/raulmur/ORB_SLAM2)
- [Artigo original](https://arxiv.org/abs/1610.06475)

### Fusão Sensorial
As técnicas de localização existentes atualmente ainda são muito sujeitas a erros. Por isso, é prática comum fazer estimativas independentes baseadas em dados de diferentes sensores e depois combiná-las para chegar numa estimativa melhor do que cada uma sozinha. O modelo matemático comumente utilizado para isso chama-se Filtro de Kalman. Há um pacote do ROS chamado _robot\_localization_ que tem uma ótima implementação deste modelo.

- [Intuição sobre Filtro de Kalman [en]](https://www.youtube.com/watch?v=IFeCIbljreY&pp=ugMICgJwdBABGAE%3D)
- [Videoaula sobre Filtro de Kalman](https://www.youtube.com/watch?v=mXLwe9OEoeI)
- [_robot\_localization_ no GitHub](https://github.com/cra-ros-pkg/robot_localization)

### SLAM
O problema de localizar o robô ao mesmo tempo que se constrói um mapa do ambiente é chamado de SLAM (_Simultaneous Localization and Mapping_). SLAM é um problema bem antigo na robótica, por isso, há técnicas bem estabelecidas para resolvê-lo. No caso 2D, o _Occupancy Grid_ é, provavelmente, a proposta mais utilizada. O algoritmo _GMapping_ é uma implementação altamente eficiente de um _Occupancy Grid_. No caso 3D, temos, por exemplo, o OctoMap, que segue uma ideia parecida.


[Aula sobre Occupancy Grid](https://www.youtube.com/watch?v=aROLZ8zB-2Y&t=4459s)
[GMapping](https://openslam-org.github.io/gmapping.html)
[Pacote ROS do GMapping](http://wiki.ros.org/gmapping)
[OctoMap](https://octomap.github.io)
[Pacote ROS do OctoMap](http://wiki.ros.org/octomap)

## Planejamento
Nesta seção, primeiro são apresentados os pré-requisitos, depois alguns dos algoritmos de planejamento mais importantes e utilizados. Por fim, são mostradas duas bibliotecas que podemos usar no desenvolvimento das tarefas de planejamento.

### Paradigmas Robóticos
Uma preliminar simples, mas importante, no estudo de algoritmos de planejamento é o conceito de paradigmas robóticos.

- [Videoaula em português](https://www.youtube.com/watch?v=B15kbEPK0iM)
- [Resumo no Wikipedia [en]](https://en.wikipedia.org/wiki/Robotic_paradigm)

### Grafos
Grafos formam a base de quase todos os algoritmos apresentados neste texto. Por isso, é importante que se saiba o que é um grafo.

- [Expĺicação sobre grafos](https://www.ime.usp.br/~pf/algoritmos_em_grafos/aulas/grafos.html) 
- [Explicação sobre grafos [en]](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)

Além disso, todos os algoritmos que usam grafos contam com um algoritmo de _busca em grafos_ associado. A lista abaixo contém referências para ambos conceitos. Os mais famosos deles são o algoritmo de Dijkstra e o A*, o qual é uma adaptação do Dijkstra.

- [Videoaula sobre algoritmo de Dijkstra](https://www.youtube.com/watch?v=ovkITlgyJ2s)
- [Vídeo sobre algoritmo de Dijkstra [en]](https://www.youtube.com/watch?v=GazC3A4OQTE)
- [Vídeo sobre o A*](https://youtu.be/mbMbGjX45_E)
- [Vídeo sobre o A* [en]](https://youtu.be/ySN5Wnu88nE)

### Campos Potenciais
Tratados os pré-requisitos, podemos focar no tema principal: algoritmos de planejamento. O primeiro deles é chamado Campos Potenciais.

- [Videoaula sobre Campos Potenciais](https://www.youtube.com/watch?v=GBr8b40LBNg)
- [Texto introdutório bastante legal [en]](https://medium.com/@rymshasiddiqui/path-planning-using-potential-field-algorithm-a30ad12bdb08)
- [Artigo original [en]](https://scholar.google.com/citations?view_op=view_citation&hl=pt-BR&user=4arkOLcAAAAJ&citation_for_view=4arkOLcAAAAJ:60iIaj97TE0C)

### Roadmaps
Alguns algoritmos deliberativos básicos são baseados no conceito de \textbf{roadmaps}. Esses algoritmos são úteis em cenários simples que não mudam com o tempo.


- [Videoaula sobre Roadmaps](https://www.youtube.com/watch?v=1ct_BgMqkdc)


### PRM/RRT
A seguir, apresentaremos dois algoritmos que seguem uma premissa diferente. O objetivo não mais é retornar sempre a melhor solução, mas ser eficiente, fácil de implementar, e o mais generalista possível. Para isso, esses algoritmos têm uma natureza probabilística e são baseados em amostragem (leia-se, "tentativa e erro"). As duas propostas mais famosas são Probabilistic Roadmaps (PRM) e Rapidly-Exploring Random Trees (RRT).


- [Videoaula sobre PRM e RRT](https://www.youtube.com/watch?v=aZgiuvmHNS4)
- [Videoaula sobre PRM e RRT [en]](https://youtu.be/ZDuoQRutcfk)
- [Video sobre RRT com demonstração [en]](https://youtu.be/Ob3BIJkQJEw)

Em termos de implementação, uma biblioteca _open source_ muito utilizada é a [OMPL](http://ompl.kavrakilab.org/). No entanto, como o OMPL não faz verificação de colisões, podemos utilizar o _framework_ [MoveIt!](https://moveit.ros.org/) para planejamento.

# Visão Computacional