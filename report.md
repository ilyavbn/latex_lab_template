---
# Front matter
title: "Курсовая работа "
subtitle: "dsfsdfМоделирование передачи данных в MININET"
author: "Ассан Акосси Жан-Самуэль НФИбд-03-18"

# Generic otions
lang: ru-RU
toc-title: "Содержание"

# Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

# Pdf output format
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
### Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Misc options
indent: true
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

##


# Введение{.unnumbered}


## Актуальность работы{.unnumbered}

Актуальность темы работы обусловлена интересом исследователей к изучению задач моделирования процессов передачи даннах в компьютерных сетях. Реальное сетевое оборудование дорого использовать для развёртывания экспериментальных стендов. В качестве альтернативного решения есть несколько программ, например GNS3, CISCO PACKET TRACER, PUTTY SECURE CRT, моделирующих оборудование сетей передачи данных. Но все средства имитационного моделирования сетей передачи данных позволяют собирать данный с построенных в них моделях сетей. Возможное решение --- Mininet[@mininet] и Wireshark[@wireshark].



## Цель работы {.unnumbered}

Целью моей курсовой работы является …...

## Задачи работы{.unnumbered}

Основными задачами мой работы являются:

1. ...

2. ...

## Методы исследования{.unnumbered}

Методом исследования является ...

## Структура работы{.unnumbered}

Курсовая работа состоит из введения, трех разделов, заключения и списка используемой литературы. Во введении ….

В первом  разделе ....

Во втором разделе ...

Во третьем разделе ...

В заключении подведены общие итоги курсовой работы, изложены основные выводы.




# Эмулятор компьютерной сети Mininet

## О Mininet
Mininet[@mininet] --- это свободно распространяемое  программное обеспечение виртуализации разработки и тестирования сетевых инструментов и протоколов. С помощью одной команды Mininet может создать реалистичную виртуальную сеть на любом типе машины (виртуальной, облачной или собственной).  В результате она обеспечивает недорогое решение и оптимизированную разработку в соответствии с производственными сетями. Mininet полезен для разработки, обучения и исследований, поскольку его легко настраивать и
взаимодействовать с ним через CLI или GUI. Mininet был первоначально разработан для экспериментов
с OpenFlow2 и программно-определяемыми сетями.


## Установка и настройка Mininet
Mininet позволяет построить виртуальную сеть непосредственно на компьютере. Хосты Mininet работают под управлением стандартного сетевого программного обеспечения Linux, а коммутаторы поддерживают OpenFlow для очень гибкой пользовательской маршрутизации и программно-определяемых сетей. Для развертывания mininet в этой работе использовался дистрибутив  Ubuntu версии 20.10.

### Использование пакета для установки Mininet

Перед установкой проверяются обновления в системе:

 *sudo apt-get update*

Затем производится установка пакета mininet с помощью команды

*sudo apt-get install mininet*

Запуск mininet осуществляется с помощью команды

*sudo mn*

Если нет ошибок, то установка прошла успешно.

Команды, приведенные на рис. [-@fig:003] создают простую топологию, состоящую из одного коммутатора (s1) и двух хостов (h1, h2),
 проверяют, работает ли OVS с помощью команды pingall (рис. [-@fig:004]).


<!--
![Обновление дистрибутива](image/01.png){ #fig:001 width=70% }

![Установка MININET в дистрибутиве Ubuntu](image/02.png){ #fig:002 width=70% }
-->

![Запуск MININET](image/03.png){ #fig:003 width=70% }

![Тестирование содединений между хостами h1 и h2](image/04.png){ #fig:004 width=70% }

OVS --- это виртуальный коммутатор, который будет использоваться для подключения устройств в mininet.
Хост h1 смог достичь h2, а h2 смог достичь h1. Это также показывает, что 0% пакетов были отброшены.


###	Использование mininet в графическом режиме

С Mininet можно работать и с помощью графического интерфейса. Для этого используется Miniedit.

Miniedit --- это не что иное, как программа на языке python, предоставляющая графический интерфейс, который позволяет нам создавать топологии и управлять ими.

Можно использовать следующий набор команд для установки программного обеспечения для работы в  Miniedit:

- установить git, если он не установлен:

 *apt-get install git*

- создать клон репозитория mininet на github:

*git clone https://github.com/mininet/mininet*

- установить пакет python, если он не установлен:

*sudo app install python3-pip python3-tk*

- установить mininet внутри python:

*sudo pip3 install install mininet*

<!-- установка библиотеки tkinter для python если он не установлен, используйте -->
- установить стандартный эмулятор терминала для графической среды, если он не установлен:

*sudo apt-get install xterm*

Если все настроено правильно, у нас не возникнет проблем с запуском программы mininet с графическим
интерфейсом (рис. [-@fig:011]).

<!--
![Установка git](image/05.png){ #fig:005 width=70% }

![Клонирование mininet с github](image/06.png){ #fig:006 width=70% }

![Установка python3-pip](image/07.png){ #fig:007 width=70% }

![Установка mininet с помощью python](image/08.png){ #fig:008 width=70% }

![Установка python3-tk](image/09.png){ #fig:009 width=70% }

![Установка xterm](image/10.png){ #fig:010 width=70% }
-->

![Окно интерфейса miniedit](image/11.png){ #fig:011 width=70% }


## Пример модели простой сети в Mininet

Создадим топологию сети, состоящую из двух хостов и коммутатора. Для этого необходимо выполнить следующие шаги (рис. [-@fig:014]):

- запустить программу;

- создать топологию, в которой у нас есть два хоста и коммутатор для развертывания;

- настроить хосты h1:10.0.0.1/8, h2:10.0.0.2/8 и запустить проект через кнопку *запуск*.



<!-- ![шаг 1](image/12.png){ #fig:012 width=70% } -->

<!-- ![шаг 2](image/13.png){ #fig:013 width=70% } -->

![Настройка адресов для хостов](image/14.png){ #fig:014 width=70% }

На рис. [-@fig:016] показано, что сеть и терминалы h1 и h2 доступны.

<!--
![Доступность хостов](image/15.png){ #fig:015 width=90% }
-->

![Проверка доступности хостов](image/16.png){ #fig:016 width=90% }

<!--


![шаг 6](image/17.png){ #fig:017 width=70% }

-->

Пример изменения адреса для хоста показан на  рис. [-@fig:018].
<!-- Здесь я удалил адрес на хостах h1 и h2, щелкнув правой кнопкой мыши на хосте h1, свойства и также на h2. -->

![Изменение адреса для хоста](image/18.png){ #fig:018 width=90% }


На рис. [-@fig:019] показан ввод команды ifonfig, чтобы показать, какой адрес установлен на хостах.


![Проверка, какой адрес установлен на хосте](image/19.png){ #fig:019 width=90% }

<!-- Здесь я сохранил топологию.

![шаг 9](image/20.png){ #fig:020 width=90% }
-->

# Анализ характеристик сети в Mininet

## Описание модели сети на базе протокола TCP

Текст.


## Построение модели сети на базе протокола TCP в Mininet

Текст.

## Визуализация данных с помощью Wireshark

Текст.

# Заключение{.unnumbered}

Текст.

# Список литературы{.unnumbered}

<!-- Тут ничего не пишем ! -->
