---
## Front matter
title: "Отчёт по лабораторной работе 1"
subtitle: "Подготовка лабораторного стенда"
author: "Гафоров Нурмухаммад"

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
papersize: a
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
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

# Введение

## Цель работы  

Целью данной работы является приобретение практических навыков установки Rocky Linux на виртуальную машину с помощью инструмента Vagrant.

# Ход выполнения

В рабочем каталоге проекта был размещён файл `packer.exe`, а также конфигурация `vagrant-rocky.pkr.hcl`. Через командную строку была выполнена инициализация проекта и сборка образа операционной системы Rocky Linux. После завершения работы Packer сформировался box-файл виртуального образа.

Затем box-файл был добавлен в локальное хранилище Vagrant. Процесс прошёл успешно, и образ стал доступен для развёртывания виртуальных машин.

![Регистрация box-файла в Vagrant](Screenshot_1.png){ #fig:002 width=85% }

Далее был выполнен запуск виртуальной машины **Server**. Vagrant автоматически создал виртуальную машину в VirtualBox, назначил сетевые параметры и импортировал ранее зарегистрированный образ.

![Запуск виртуальной машины Server](Screenshot_2.png){ #fig:003 width=85% }

В проект были добавлены два provisioning-скрипта. Первый создаёт нового пользователя, устанавливает пароль и добавляет его в группу с правами администратора.

![Скрипт создания пользователя](Screenshot_3.png){ #fig:004 width=70% }

Второй изменяет hostname виртуальной машины, формируя доменное имя по шаблону `<hostname>.<username>.net`.

![Скрипт изменения hostname](Screenshot_4.png){ #fig:005 width=60% }

После завершения развёртывания выполнено подключение к серверу через SSH с помощью Vagrant. Затем осуществлён переход на созданного пользователя и выход из сессии.

![SSH-подключение и вход под пользователем](Screenshot_5.png){ #fig:006 width=85% }

Также была выполнена проверка входа в графическое окружение виртуальной машины, что подтверждает успешную настройку пользователя и hostname.

![Графическое окружение Rocky Linux](Screenshot_6.png){ #fig:007 width=85% }

# Вывод

В результате выполнения работы был развёрнут лабораторный стенд на базе Vagrant и VirtualBox в операционной системе Windows. Образ Rocky Linux был успешно собран с использованием Packer и зарегистрирован в Vagrant, после чего произведён запуск виртуальной машины. В процессе автоматической конфигурации были созданы пользовательская учётная запись и изменено сетевое имя хоста. Проверка подключения по SSH и вход в графическое окружение подтвердили корректность выполненных настроек и готовность стенда к дальнейшему использованию.

## Контрольные вопросы

### 1. Для чего предназначен Vagrant?

Vagrant — это инструмент для автоматизированного развертывания и управления виртуальными машинами.  
Он позволяет быстро создавать воспроизводимые среды разработки, используя единый конфигурационный файл.  
Основные цели:
- автоматизация создания виртуальных машин;
- единообразие окружений у разработчиков;
- возможность запуска как на Windows, Linux, macOS;
- интеграция с популярными гипервизорами (VirtualBox, VMware и др.).

### 2. Что такое box-файл? В чём назначение Vagrantfile?

**Box-файл** — это шаблон (образ) виртуальной машины, подготовленный для использования Vagrant.  
Box включает минимальную операционную систему и используется как базовый элемент для создания новых виртуальных машин.

**Vagrantfile** — основной конфигурационный файл проекта Vagrant.  
Назначение:
- описывает параметры виртуальной машины (ресурсы, сеть, hostname, синхронизация папок);
- задаёт provisioning (скрипты автоматической настройки системы);
- определяет используемый box-файл.

### 3. Приведите описание и примеры вызова основных команд Vagrant

| Команда | Назначение |
|---------|-----------|
| `vagrant init` | Создаёт новый Vagrantfile в каталоге проекта. |
| `vagrant box add <name> <file>` | Добавляет box-файл в локальное хранилище Vagrant. |
| `vagrant up` | Запускает виртуальную машину и выполняет её настройку. |
| `vagrant halt` | Корректно выключает виртуальную машину. |
| `vagrant ssh` | Подключение к VM через SSH. |
| `vagrant destroy` | Удаляет виртуальную машину. |
| `vagrant status` | Показывает текущее состояние VM. |
| `vagrant reload` | Перезапуск VM с применением изменений Vagrantfile. |


### 4. Дайте построчные пояснения содержания файлов vagrant-rocky.pkr.hcl, ks.cfg, Vagrantfile, Makefile

**vagrant-rocky.pkr.hcl** (файл Packer):
- определяет источник образа (ISO Rocky Linux);
- настраивает параметры сборки (CPU, RAM);
- содержит настройки автоматической установки ОС;
- указывает provisioning — действия, выполняемые во время сборки образа (установка пакетов и т. д.).

**ks.cfg** (Kickstart-файл):
- используется для автоматической установки Linux без участия пользователя;
- содержит:
  - разметку дисков;
  - параметры пользователя root;
  - настройки сети;
  - список пакетов для установки.

**Vagrantfile**:
- определяет:
  - используемый box-файл;
  - сетевые параметры машины (NAT/статический IP);
  - имя виртуальной машины (hostname);
  - provisioning-скрипты (создание пользователя, автоматическая настройка).


**Makefile**:
- содержит набор автоматизированных действий для сборки проекта;
- упрощает запуск Packer и управление Vagrant;
- позволяет выполнить сборку одной командой (`make build`).


