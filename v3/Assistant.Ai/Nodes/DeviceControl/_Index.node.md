---
AWN-TYPE: NODE/SPACE
AWN-TITLE: Index — DeviceControl
AWN-DESC: "Оркестратор папки DeviceControl: заглушки для управления компьютером, телефоном, сервером и умным домом; к заполнению по мере интеграций."
AWN-LOAD: on_demand
AWN-PRIORITY: 45
AWN-TRIGGERS:
  - управление устройствами
  - device control
  - компьютер телефон сервер
  - удалённое управление
  - devicecontrol
AWN-STATUS: draft
AWN-MEMORY: none
AWN-AUTOMATIZATION: false
AWN-CRON: 0 9 * * *
AWN-CATEGORY: system
AWN-VERSION: 0.1.0
AWN-CREATED: 2026-05-07
AWN-UPDATED: 2026-05-07
---

# Index — DeviceControl

> [!info] О файле
> Вход в `Assistant.Ai/Nodes/DeviceControl/`. Что здесь лежит и с какой дочерней нодой работать при запросе про ПК, телефон, сервер или умный дом.

## Назначение папки

Сгруппировать инструкции и правила для **локального или удалённого управления** четырьмя категориями: компьютер, телефон, сервер и умный дом. Сейчас всё — **заглушки** без конкретных инструментов и API.

## Состав

- [[Assistant.Ai/Nodes/DeviceControl/ComputerControl.node|ComputerControl.node]] — сценарии управления **компьютером**.
- [[Assistant.Ai/Nodes/DeviceControl/PhoneControl.node|PhoneControl.node]] — сценарии управления **телефоном**.
- [[Assistant.Ai/Nodes/DeviceControl/ServerControl.node|ServerControl.node]] — сценарии управления **сервером**.
- [[Assistant.Ai/Nodes/DeviceControl/SmartHomeControl.node|SmartHomeControl.node]] — сценарии управления **умным домом**.

## Локальные правила

- Не смешивать с идентичностью ассистента и глобальными правилами vault — только сценарии «агент + устройство».
- После появления реальных интеграций (SSH, ADB, MDM и т.д.) обновлять соответствующую дочернюю ноду, а этот Index — при изменении состава папки или общего порядка работы.
