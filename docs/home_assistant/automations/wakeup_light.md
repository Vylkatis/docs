---
pagination_prev: null
---

# Wake up Lights

Here is my configuration:

```yaml
alias: Réveil Laura
description: ""
trigger:
  - platform: template
    value_template: >-
      {{ now() >= today_at(states('input_datetime.laura_alarm')) -
      timedelta(minutes =10)  }}
condition:
  - condition: time
    after: "00:00:00"
    before: "23:59:00"
    weekday:
      - mon
      - tue
      - wed
      - thu
      - fri
action:
  - sequence:
      - service: light.turn_on
        metadata: {}
        data:
          brightness_pct: 1
          color_temp: 369
        target:
          entity_id: light.bedroom_light
      - delay:
          hours: 0
          minutes: 0
          seconds: 2
          milliseconds: 0
      - service: light.turn_on
        metadata: {}
        data:
          transition: 600
          brightness_pct: 100
        target:
          entity_id: light.bedroom_light
mode: single
```