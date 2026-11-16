# Граница server API на этапе 1

Источник серверного контракта — [Панель-Service](https://github.com/pasha-tsaran/Panel-Service).

## Уже реализовано сервером

`POST /api/v1/activate`

```json
{"activation_key":"<12 decimal digits>"}
```

Серверная Pydantic-модель принимает ровно 12 цифр. Успешный ответ содержит
`account` (`id`, `email`, `telegram_username`, `phone_number`) и `protocols`
(`wireguard`, `amneziawg`, `vless`). Ответ имеет `Cache-Control: no-store` и
`Pragma: no-cache`.

Неизвестный, отключённый, неполный или истёкший аккаунт получает одинаковый
`401 Invalid activation key`; лимит повторных неудач возвращает `429`.

Клиент передаёт 12 цифр без префикса.

## Пока не реализовано сервером

- список серверов, их состояние, нагрузку и задержку;
- отдельная проверка состояния/даты подписки;
- обновление или выдача профилей по выбранному server/protocol/device;
- платёжный API;
- remote diagnostics upload.

На этапе 1 эти возможности представлены только доменными контрактами и явно
названными mock-реализациями. Клиент не предполагает несуществующие endpoint'ы.
