# ⚠️ Legacy Version

Этот репозиторий больше не развивается.
Новая версия платформы: https://github.com/kolpakovden/mifa-vpn-platform

---
---
---



# 🛡️ VLESS + Telegram Monitoring + Grafana
![Version](https://img.shields.io/badge/version-3.0-blue)
![Xray](https://img.shields.io/badge/Xray-25.8.3-green)
![Telegram](https://img.shields.io/badge/Telegram-bot-26A5E4)
![Grafana](https://img.shields.io/badge/Grafana-dashboard-F46800)
![Loki](https://img.shields.io/badge/Loki-logs-4A90E2)

Self-hosted VPN server with full monitoring and Telegram control.

---

## Overview

Проект объединяет:

- **Xray (VLESS + Reality)** — VPN-сервер
- **Telegram-боты** — управление пользователями и уведомления
- **Grafana + Loki** — мониторинг пользовательской активности
- **Prometheus + Node Exporter** — системные метрики сервера

> Зачем это всё? → [**ABOUT.md**](ABOUT.md)

---

## Features

- **VPN** — уникальные UUID, 5 портов, 11 доменов маскировки
- **Telegram** — уведомления о подключениях + бот управления (/add, /list, /del)
- **Геолокация** — город, страна, провайдер по IP
- **Мониторинг** — логи посещений (Grafana + Loki) и ресурсы сервера (Prometheus + Node Exporter)

---

## Архитектура

```
Internet
   │
   ▼
Xray (VLESS + Reality)
   │
   ├── access.log ──► Promtail ──► Loki ──► Grafana
   │
   ├── API stats ──► Prometheus ──► Grafana
   │
   └── Telegram Bot (notifications + management)
```

---

## Quick Start

```bash
git clone https://github.com/kolpakovden/MIFA-VPN.git
cd MIFA-VPN
```

---

## Setup Guide

### Xray

- Пример конфига: [`config/example.config.json`](config/example.config.json)
- Документация: [`docs/xray-config.md`](docs/xray-config.md)

### Telegram Bots

- Бот уведомлений: [`docs/telegram-bot.md#бот-уведомлений`](docs/telegram-bot.md#бот-уведомлений)
- Бот управления: [`docs/telegram-bot.md#бот-управления`](docs/telegram-bot.md#бот-управления)

### Monitoring

- **User Activity** — Loki + Promtail (логи посещений)
- **System Metrics** — Prometheus + Node Exporter (CPU, RAM, Disk, Network)

Полная инструкция: [`docs/monitoring.md`](docs/monitoring.md)

---

## Project Structure

```
MIFA-VPN/
├── README.md                               # Главная документация
├── MANIFEST.md                             # Мотивация и история
├── .env.example                            # Пример переменных
├── .gitignore                              # Игнорируемые файлы
│
├── docs/                                   # Документация
│   ├── monitoring.md                       # Loki + Prometheus
│   ├── telegram-bot.md                     # Инструкции по ботам
│   ├── xray-config.md                      # Настройка Xray
│   └── commands.md                         # Шпаргалка по командам
│
├── config/                                 # Примеры конфигов
│   ├── example.config.json                 # Xray (пример)
│   ├── loki-config.yaml                    # Конфиг Loki
│   ├── promtail-config.yaml                # Конфиг Promtail
│   └── loki.service                        # Systemd сервис
│
├── scripts/                                # Скрипты
│   ├── check_users.sh                      # Бот уведомлений
│   ├── bot.py                              # Бот управления
│   ├── xray-tg-bot.service                 # Systemd для бота
│   └── xray-exporter.service               # (опционально)
│
└── dashboards/                             # JSON дашбордов
    └── user-activity.json                  # Дашборд для Grafana
```

---

## Dashboards

Импортируй дашборд [`dashboards/user-activity.json`](dashboards/user-activity.json) в Grafana.

После импорта ты получишь:

- Топ доменов
- Активность пользователей
- Логи в реальном времени
- CPU / RAM / Disk
- Сетевую нагрузку

---

## Documentation

| Раздел | Ссылка |
|--------|--------|
| Мониторинг | [`docs/monitoring.md`](docs/monitoring.md) |
| Telegram-боты | [`docs/telegram-bot.md`](docs/telegram-bot.md) |
| Настройка Xray | [`docs/xray-config.md`](docs/xray-config.md) |
| Шпаргалка по командам | [`docs/commands.md`](docs/commands.md) |

---

## Credits

- [@maxgalzer](https://github.com/maxgalzer) за [xray-traffic-bot](https://github.com/maxgalzer/xray-traffic-bot)
- [@Davoyan](https://github.com/Davoyan) за [xray-access-view](https://github.com/Davoyan/xray-access-view)
- [@anatolykopyl](https://github.com/anatolykopyl) за [xray-exporter](https://github.com/anatolykopyl/xray-exporter)
- [@Globchansky](https://github.com/Globchansky) за [xray-stats-exporter](https://github.com/Globchansky/xray-stats-exporter)
- [@mintel](https://github.com/mintel) за [promtail-static](https://github.com/mintel/promtail-static)
- [@grafana](https://github.com/grafana) за [Loki](https://github.com/grafana/loki) и [Grafana](https://github.com/grafana/grafana)
- [@XTLS](https://github.com/XTLS) за [Xray-core](https://github.com/XTLS/Xray-core)

---

# License & Disclaimer

Цель проекта — **бесплатная доступность для всех без коммерческой эксплуатации**.

С 24 октября 2026 года новые разрешения на собственные материалы проекта предоставляются по [MIFA Free Noncommercial License 1.0](LICENSE).

- Разрешены бесплатное некоммерческое использование, изучение, изменение и бесплатное распространение.
- Необходимо сохранять уведомления об авторстве, текст лицензии и ссылку на этот репозиторий; изменения нужно обозначать.
- Запрещены продажа проекта и производных, платный VPN и другие монетизируемые сервисы на их основе.
- Запрещены платные установка, настройка, размещение, сопровождение, поддержка, консультации и обучение по проекту.
- Оплата собственного сервера или подключения независимому провайдеру для разрешённого некоммерческого использования допускается.

**Ранее выданные права MIT сохраняются.** Код и другие материалы, ранее опубликованные под MIT, можно продолжать использовать по MIT, включая коммерческое использование. Замена лицензии не делает прежний код исключительно некоммерческим. Это особенно существенно для архивных версий, где новых разработок может не быть.

Сторонние компоненты и материалы сохраняют собственные лицензии и авторство. Условия этого репозитория не заменяют лицензии Xray, Grafana, Loki и других зависимостей.

Это собственная некоммерческая лицензия с доступными исходниками, а не MIT и не стандартная open source лицензия. Материалы предоставляются «как есть», без гарантий.

---

**Make Internet Free Again** ✊🌐
