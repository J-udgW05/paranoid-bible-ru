# 🛡️ Библия Параноика (Paranoid Bible RU)

> **Полное практическое руководство по кибербезопасности, анонимности, защите данных и цифровому суверенитету (2026).**

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC_BY--NC--SA_4.0-lightgrey.svg)](site/license.html)
[![Zero Logs](https://img.shields.io/badge/Privacy-Zero_Logs-brightgreen.svg)](site/privacy.html)
[![CSP Strict](https://img.shields.io/badge/CSP-Strict_default--src_'none'-blue.svg)](site/_headers)
[![PWA Ready](https://img.shields.io/badge/PWA-Offline_Cache_v14-orange.svg)](site/sw.js)

---

## 📖 О проекте

«Библия Параноика» — фундаментальный структурированный справочник (153 тематических раздела), охватывающий все уровни модели цифровой безопасности:
- **Операционные системы:** Hardening Windows 10/11 (включая unattend-установку, групповые политики Enterprise/Education vs Pro/Home, изоляцию телеметрии), Linux (Qubes OS, Tails, Whonix, Arch/Debian Hardening), macOS, Android (GrapheneOS), iOS.
- **Сетевая безопасность:** Tor, I2P, WireGuard, Shadowsocks, VLESS, Reality, DNS over HTTPS/TLS, изоляция локальных сетей и роутеров (OpenWrt/pfSense).
- **Криптография и данные:** VeraCrypt, LUKS, GnuPG (PGP), Age, BitLocker, менеджеры паролей (KeePassXC), уничтожение данных (shredding, secure erase).
- **Анонимные коммуникации:** Signal, SimpleX Chat, Briar, Session, Matrix, временная почта и PGP-шифрование.
- **Правовой контекст и регуляторика:** Сравнительный анализ законодательства и стандартов СНГ (152-ФЗ, Яровая, СОРМ), Евросоюза (GDPR, NIS2, eIDAS), США (FISA 702, CLOUD Act, HIPAA), стран Азии и Латинской Америки.

---

## 🔒 Архитектура безопасности сайта

Сайт спроектирован по принципу максимальной защиты и нулевого доверия:
1. **Zero Tracking & No Cookies:** Отсутствуют любые внешние аналитические метрики (Google Analytics, Яндекс.Метрика), пиксели и рекламные трекеры.
2. **Строгая Content Security Policy (CSP):**
   ```http
   default-src 'none'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self' data:; connect-src 'none'; frame-src 'none'; object-src 'none'; base-uri 'self'; form-action 'none';
   ```
3. **Безопасные внешние ссылки:** Все 4100+ ссылок снабжены защитными атрибутами `rel="noopener noreferrer nofollow"` и открываются в изолированных контекстах (`target="_blank"`).
4. **Защитные HTTP-заголовки (`site/_headers`):**
   - `X-Frame-Options: DENY` (защита от Clickjacking)
   - `X-Content-Type-Options: nosniff` (защита от MIME-sniffing)
   - `Referrer-Policy: no-referrer` (утечка адреса при переходах исключена)
   - `Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=(), usb=(), browsing-topics=()`
5. **Автономность (PWA Offline Service Worker):** Работает полностью оффлайн без подключения к интернету.

---

## 📂 Структура репозитория

```
paranoid-bible-ru/
├── site/
│   ├── index.html         # Основное руководство (153 раздела, 2.3 МБ чистого HTML)
│   ├── privacy.html       # Политика конфиденциальности и Zero-Log декларация
│   ├── disclaimer.html    # Отказ от ответственности и этический регламент
│   ├── canary.html        # Warrant Canary (гарантия независимости и отсутствия бэкдоров)
│   ├── contacts.html      # Защищенные каналы связи и публичный PGP-ключ
│   ├── license.html       # Лицензия CC BY-NC-SA 4.0 и условия использования
│   ├── sw.js              # Service Worker (Cache-First, v14)
│   ├── manifest.json      # PWA Web App Manifest
│   └── _headers           # Заголовки безопасности для хостинга (Cloudflare Pages / Netlify)
├── .gitignore             # Исключение системного мусора и зависимостей
├── package.json           # Локальные скрипты безопасности и Safe Chain
└── README.md              # Документация репозитория
```

---

## 🚀 Локальный запуск

Сайт полностью статичен. Для открытия достаточно дважды кликнуть на `site/index.html` в любом браузере, либо поднять локальный веб-сервер:

```bash
# Python
python -m http.server 8080 --directory site

# Node.js
npx serve site
```

---

## 📜 Лицензия

Материалы руководства распространяются под международной лицензией **[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)**.
Любое использование допускается в некоммерческих целях с сохранением авторства и аналогичной лицензией.
