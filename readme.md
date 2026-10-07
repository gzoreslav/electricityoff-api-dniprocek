# ElectricityOff API — Дніпро (DNIPROCEK)

Публічне API графіків відключень для **ЦЕК** (провайдер `DNIPROCEK`).

Джерело даних — Yasno blackout-service, регіон `3`, оператор `303`:

```
https://app.yasno.ua/api/blackout-service/public/shutdowns/regions/3/dsos/303/planned-outages
```

Черги лишаються як у джерелі: `1.1`, `1.2` … `6.2`.

## Endpoints

- `GET /api/v1` — статус
- `GET /api/v1/off` або `GET /api/v1/off/DNIPROCEK` — події відключень

### Формат відповіді

```json
{
  "events": [
    {
      "date": "2026-10-07",
      "startTime": "06:00",
      "endTime": "09:30",
      "provider": "DNIPROCEK",
      "electricity": "off",
      "queue": "1.1"
    }
  ],
  "hasTodayData": true,
  "hasTomorrowData": true,
  "serverTime": "07-10-2026 11:00"
}
```

Час у джерелі — хвилини від півночі. У відповідь потрапляють лише слоти з `type: "Definite"` (відключення), коли `status === "ScheduleApplies"`.

## Deploy

```bash
npm install
npx vercel --prod
```
