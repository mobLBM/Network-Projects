# CSIT127 Packet Tracer Project — interconnected LANs (departments)

**Файл проекта:** `CSIT127 project.pkt`  
**Автор:** Timurmalik Djuraev (8562763)

## Описание (что сделано)
Этот проект в Cisco Packet Tracer показывает **несколько локальных сетей (LAN) отделов**, соединённых друг с другом через **маршрутизаторы**.

По скриншоту топологии:
- Есть **несколько LAN отделов**: *Procurement*, *IT*, *HR*, *Staff*
- В каждом отделе: **коммутатор (2960)** + проводные ПК/ноутбуки/принтеры
- Также есть **Wi‑Fi точки** (Access Point) для смартфонов/планшетов
- **Router0** подключает LAN: Procurement, IT, HR
- **Router1** подключает LAN: Staff
- **Router0 ↔ Router1** соединены линком для связи всех отделов между собой

> Никаких “сверх‑сложных” VPN/Firewall/SIEM тут не заявляется — это именно **соединённые LAN’ы** (inter‑LAN routing) + базовая инфраструктура офиса.

## Состав (в общих словах)
- Routers: 2 (Router0, Router1)
- Switches: по одному на отдел (несколько 2960)
- Wireless: точки доступа для Wi‑Fi устройств
- End devices: ПК/ноутбуки/принтеры/смартфоны/планшеты

## Как открыть и проверить
### Требуется
- Cisco Packet Tracer (желательно 8.x)

### Открытие
1. Запусти Packet Tracer
2. **File → Open**
3. Выбери **`CSIT127 project.pkt`**

### Быстрые тесты (минимум)
1. **Ping внутри отдела** (ПК ↔ ПК в одном LAN)
2. **Ping между отделами** (например IT ↔ HR, IT ↔ Staff, Procurement ↔ HR)
3. Если есть принтеры — проверить доступность (ping до принтера)

## Команды для скриншотов (для отчёта)
### На роутерах
```
show ip interface brief
show ip route
show running-config
```

### На свитчах
Если VLAN’ы не настраивались — будет почти всё по умолчанию (VLAN 1).
```
show vlan brief
show interfaces status
show running-config
```

## Рекомендуемая структура репозитория
> GitHub не хранит пустые папки — клади внутрь хотя бы `README.md` или `.gitkeep`.

```
.
├─ CSIT127 project.pkt
├─ README.md
├─ screenshots/
│  ├─ topology.png
│  └─ tests/
├─ docs/
│  └─ report.docx (или report.pdf)
```

## Что вставить в README/отчёт (если попросит преподаватель)
- Кратко: “LAN’ы отделов соединены маршрутизаторами”
- Схема/скрин топологии
- Таблица IP‑подсетей (если использовал разные сети на отдел)
- Подтверждение тестами (ping + show ip route)

---
Если ты хочешь, я сделаю **README на 100% “по факту твоего .pkt”** (с точными подсетями и именами интерфейсов),
просто пришли:
- 1 скрин **IP настройки** любого ПК из каждого отдела (Desktop → IP Configuration), **или**
- вывод на Router0/Router1: `show ip interface brief` и `show ip route`.
