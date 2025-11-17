---
lang: ru-RU
title: Настройка DHCP-сервера Kea
subtitle: Лабораторная работа №3
author:
  - Гафоров Нурмухаммад
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 15.11.2025

toc: false
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Введение

## Цель работы
- Настроить DHCP-сервер Kea.
- Конфигурировать DNS Bind9.
- Реализовать автоматические DDNS-обновления.

# Конфигурирование DHCP

## Основные изменения
- Обновлены `domain-name` и DNS-параметры.  
- Настроена подсеть, шлюз и диапазон IP.
- Удалены примеры конфигураций.

![Редактирование domain-name и DNS](Screenshot_1.png){ width=70% }

## Проверка и запуск
- Привязка DHCP к интерфейсу `eth1`.
- Успешная проверка конфигурации.
- Автоматический запуск сервиса.

![Запуск DHCP-сервера](Screenshot_6.png){ width=70% }

# Настройка DNS-зон

## Внесённые изменения
- Добавлены A- и PTR-записи.
- Обновлены серийные номера зон.
- Перезапуск Bind9.

![Прямая зона](Screenshot_3.png){ width=70% }

# Анализ работы DHCP

## Проверка клиента
- Клиент получил IP: **192.168.1.30**.
- Lease записан в `kea-leases4.csv`.
- Соответствие MAC-адреса подтверждено.

![Сетевые интерфейсы клиента](Screenshot_8.png){ width=70% }

# Настройка DDNS

## TSIG-ключ
- Создан ключ обновления зон.
- Подключён в Bind9.
- Задана политика `update-policy`.

![TSIG-ключ](Screenshot_10.png){ width=70% }

## Kea DHCP-DDNS
- Создан `tsig-keys.json`.
- Указаны параметры DDNS.
- Запущен сервис DDNS.

![Настройки Kea DDNS](Screenshot_13.png){ width=70% }

## Активация DDNS в DHCP
- Включены обновления DNS.
- Указан суффикс `ngaforov.net`.
- Разрешено перезаписывать записи клиента.

![DDNS настройки DHCP](Screenshot_15.png){ width=70% }

# Проверка DDNS

## Результат проверки
- В DNS появилась запись:
  - `client.ngaforov.net`
  - IP → `192.168.1.30`
- Обновление прошло автоматически.

![Проверка DNS](Screenshot_17.png){ width=70% }

# Выводы

## Итог
- Настроены Kea DHCP и Bind9.
- Реализован DDNS на основе TSIG.
- Стенд полностью автоматизирован.
