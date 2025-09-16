# Tuya Smart Knob — Master Brightness for Multiple Groups

This [Home Assistant](https://www.home-assistant.io/) blueprint allows you to use a **Tuya Zigbee rotary knob** (ZG-101Z/D, TS004F, etc.) as a master brightness controller for multiple lights or groups.  
It stores brightness in a single `input_number` helper (0–100) and applies it to all selected targets with smart pre-power logic, availability filtering, and auto-resync when power is restored.

---

## 📥 Import Blueprint

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?url=https://raw.githubusercontent.com/Kurenin/home-assistant-blueprints/main/zigbee/tuya_smart_knob_master_brightness.yaml)

*(Update RAW URL if your repo or folder structure changes.)*

---

## ✨ Features

- **Master brightness** (via `input_number`) applied to all selected lights/groups.  
- **Smart pre-power**:  
  - If *all* pre-power devices were Off, any action turns them On.  
  - Otherwise, relays are left untouched.  
- **Availability filter**: skip `unavailable` entities when adjusting.  
- **Auto-resync**: when any light comes back to On, brightness is restored from the master value.  
- Works with both **JSON** and **/action** MQTT payloads.  
- No `operation_mode` is sent.

---

## ⚙️ Inputs

| Input | Description |
|-------|-------------|
| **Device MQTT topic** | Example: `zigbee2mqtt/Knob/#` (captures both JSON and `/action`) |
| **Target lights/groups** | Entities that will receive the same brightness |
| **Master brightness helper** | An `input_number` (0–100) to store current master brightness |
| **Pre-power devices** | Optional list of switches/lights that must be powered before dimming |
| **Pre-power delay** | Delay (sec) after pre-powering before applying brightness |
| **Single-click action** | `toggle_pre_power` or `toggle_lights` |
| **Step size (command mode)** | Brightness step when knob sends COMMAND (default 8%) |
| **Step size (event mode)** | Brightness step when knob sends EVENT (default 8%) |
| **Min/Max brightness** | Clamp brightness between these values |
| **Transition** | Smooth fade time when adjusting brightness |
| **Power on with rotate** | If lights were Off, rotation turns them On with current brightness |
| **Smart pre-power (all Off)** | Only pre-power devices if *all* were Off |
| **Apply only available** | Skip entities in `unavailable` state |
| **Resync on restore** | Restore master brightness when any target turns On |
| **Automation mode** | `single`, `restart`, `queued`, or `parallel` |

---

## 🛠 Example Use

- Rotary knob controls brightness of multiple light groups (kitchen + living room).  
- If all relays were Off, first action powers them before adjusting.  
- If one group is temporarily unavailable, only the available lights are updated.  
- After power outage, brightness automatically syncs to stored master value.

---

## 📄 License

This project is licensed under the [MIT License](../LICENSE).

