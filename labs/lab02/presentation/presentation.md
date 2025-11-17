---
## Front matter
lang: ru-RU
title: Настройка DNS-сервера BIND
subtitle: Лабораторная работа №2
author:
  - Гафоров Нурмухаммад
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 11.11.2025

## Formatting for PDF/Slides
toc: false
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Цели и задачи работы

## Цель
Получить навыки установки и конфигурирования **DNS-сервера BIND**, освоить работу с прямыми и обратными зонами.

# Ход выполнения

## Установка BIND и проверка DNS

- Установлены пакеты bind и bind-utils.
- Выполнен первый DNS-запрос с помощью `dig`.
- Получены записи домена и IP-адреса внешнего DNS.

![Внешний DNS-запрос](Screenshot_7.png){ width=70% }

## Анализ конфигурационных файлов

- `/etc/resolv.conf` — DNS сервера по умолчанию.
- `/etc/named.conf` — основной конфигурационный файл BIND.
- `/var/named/*` — шаблоны зон и системные зоны.

![Конфигурация named.conf](Screenshot_8.png){ width=70% }

## Запуск и проверка DNS-сервера

- DNS-служба запущена и добавлена в автозагрузку.
- Проверен локальный DNS-резолвинг (`dig @127.0.0.1`).

![Запрос через локальный DNS](Screenshot_11.png){ width=70% }

## Назначение DNS-сервера по умолчанию

- Настроено сетевое соединение `eth0` через `nmcli`.
- Установлен DNS: `127.0.0.1`.
- Перезапущен NetworkManager.

![Изменение DNS в nmcli](Screenshot_12.png){ width=70% }

## Открытие DNS для локальной сети

- В `named.conf` разрешены запросы из сети `192.168.0.0/16`.
- В firewall разрешён сервис DNS.

![Изменения в named.conf](Screenshot_13.png){ width=70% }

## Создание файла зон

- Создан новый файл зоны.
- Подключён в `/etc/named.conf`.

![Подключение зоны](Screenshot_15.png){ width=70% }

## Прямая зона

- Создана зона `ngaforov.net`.
- Добавлены записи: SOA, NS, A.

![Файл прямой зоны](Screenshot_17.png){ width=70% }

## Обратная зона

- Создана зона `1.168.192.in-addr.arpa`.
- Добавлены PTR-записи.

![Файл обратной зоны](Screenshot_18.png){ width=70% }

## SELinux и права доступа

- Исправлены контексты файлов через `restorecon`.
- Разрешена запись в зоны с помощью `setsebool`.

![SELinux и права](Screenshot_19.png){ width=70% }

## Проверка dig и host

- `dig ns.ngaforov.net` — возвращает IP.
- `host -l ngaforov.net` — выводит записи зоны.

![Проверка DNS](Screenshot_21.png){ width=70% }

## Автоматизация provisioning

- Конфигурационные файлы сохранены в `/vagrant/provision/server/dns`.
- Создан скрипт `dns.sh`, выполняющий автоматическую настройку.

![Скрипт provisioning](Screenshot_22.png){ width=70% }

# Выводы

## Итог работы

- Установлен DNS-сервер BIND.
- Настроены прямые и обратные зоны.
- Проверена работа DNS через `dig` и `host`.
- Выполнена подготовка автоматического provisioning.

DNS-сервер функционирует как **master-сервер зоны** и корректно обрабатывает запросы.
