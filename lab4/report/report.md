---
## Front matter
title: "Отчёт по лабораторной работе 4-D (НФИ-2)"
subtitle: "Программный комплекс обучения методам обнаружения, анализа и устранения последствий компьютерных атак «Ampire»"
author: "Козлов В.П., Гэинэ А., Шуваев С., Джахангиров И.З, Хватов М.Г. | НФИбд-02-22"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: Arial
romanfont: Arial
sansfont: Arial
monofont: Arial
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
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Отработать сценарий: Захват DNS-Сервера.

# Задание

1. Установить meterpreter-сессию с узлом в сегменте DMZ.

2. Осуществить поиск DNS-сервера.

3. Отсканировать 100 самых часто используемых портов.

4. Обнаружить ответ от порта 22, а также 53, что стандартно для DNS сервера.

5. Осуществить брут форс атаку.

6. С помощью пароль, подключиться по ssh открыв новую shell сессию.

7. Альтернативно, подключаемся за счёт модуля auxiliary(scanner/ssh/ssh_login).

# Выполнение лабораторной работы

Запускаем msfconsole. Загружаем модуль exchange_proxyshell_rce (рис. [-@fig:001])

![Модуль exchange_proxyshell_rce. Настройки](image/1.png){ #fig:001 width=70% }

Настраиваем модуль и запускаем (рис. [-@fig:002])

![Настройка и запуск](image/2.png){ #fig:002 width=70% }

Получаем сессию meterpreter. Выполняем проброс портов в сеть  (рис. [-@fig:003])

![Пробрасываем порты"](image/3.png){ #fig:003 width=70% }

Сворачиваем сессию. Переключаемся на модуль ping_sweep (рис. [-@fig:004])

![модуль ping_sweep"](image/4.png){ #fig:004 width=70% }

Запускаем скан. Получаем открытый для нас рут во внутрь. (рис. [-@fig:005])

![Запуск ping_sweep и рут](image/5.png){ #fig:005 width=70% }

Отображаем хостов во внутренней сети (рис. [-@fig:006])

![Хосты внутренней сети](image/6.png){ #fig:006 width=70% }

Переключаемся на socks proxy. Настраиваем (рис. [-@fig:007])

![Настройка socks proxy](image/7.png){ #fig:007 width=70% }

Сканируем 100 самых используемых портов (рис. [-@fig:008])

![Сканирование](image/8.png){ #fig:008 width=70% }

Видим уязвимости (рис. [-@fig:009])

![Открытые порты](image/9.png){ #fig:009 width=70% }

Через hydra делаем подбор паролей (рис. [-@fig:010])

![Работа гидры](image/10.png){ #fig:010 width=70% }

Нашли совпадение (рис. [-@fig:011])

![Гидра успешна нашла нам пароль](image/11.png){ #fig:011 width=70% }

Через ssh заходим на компьютер, пользуясь полученным паролем (рис. [-@fig:012])

![ssh сессия](image/12.png){ #fig:012 width=70% }

Находим флажок. Захватываем его (рис. [-@fig:013])

![Флаг захвачен!](image/13.png){ #fig:013 width=70% }

Как альтернатива: пользуемся модулём ssh_login (рис. [-@fig:014])

![ssh_login](image/14.png){ #fig:014 width=70% }

Флажок найден (повторно) (рис. [-@fig:015])

![Флаг захвачен! х2](image/15.png){ #fig:015 width=70% }

# Выводы

Отработали сценарий: Захват DNS-Сервера. 


# Список литературы
1.  **CVE-2019-0630** — Common Vulnerabilities and Exposures.  
    URL: `https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-0630`

2.  **CVE-2019-17427** — Уязвимость XSS в Redmine.  
    URL: `https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-17427`

3.  **CVE-2019-18890** — Уязвимость Blind SQL-инъекции в Redmine.  
    URL: `https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-18890`