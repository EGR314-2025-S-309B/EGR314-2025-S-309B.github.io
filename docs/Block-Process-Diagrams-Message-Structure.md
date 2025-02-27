---
title: Block/Process Diagrams & Message Structure
---

## Block Diagram

### General Diagram

![Image](https://github.com/user-attachments/assets/0c77f48d-81e9-4630-be1a-b01ad48d87c3)

### Connector Diagram

![Image](https://github.com/user-attachments/assets/5181d0f3-c607-4b25-8f0b-ecfba9d1c3aa)

## Process Diagram

``` mermaid
sequenceDiagram
autonumber
actor In-Person User
In-Person User-->>Bruce: Change Motor Direction
Bruce->>Baron: Change Motor Direction
Baron->>Shaurya: Change Motor Direction
Shaurya->>Aadish: Change Motor Direction
Aadish->>Aadish: Motor Direction Changed<br>(Trash)
loop Every Millisecond
  Shaurya->>Aadish: Update Motor Speed
  Aadish->>Aadish: Motor Speed Updated<br>(Trash)
end
Shaurya->>Aadish: Rotational Velocity
Aadish->>Baron: Rotational Velocity
Baron->>Bruce: Rotational Velocity
actor Web User
Baron-->>Web User: Display Rotational Velocity
Bruce-->>In-Person User: Display Rotational Velocity
actor Web User
Web User-->>Baron: Change Motor Direction
Baron->>Shaurya: Change Motor Direction
Shaurya->>Aadish: Change Motor Direction
Aadish->>Aadish: Motor Direction Changed<br>(Trash)
```

## Message Structure

### ID's

| ID | Definition |
|---|---|
| 0xFF | Bruce |
| 0xFE | Baron |
| 0xFD | Aadish |
| 0xFC | Shaurya |

### Message Types

| Message Length | Description |
|---|---|
| 1 (uint8_t) | Button 1 Pressed |
| 1 (uint8_t) | Button 2 Pressed |
| 1 (uint8_t) | Button 3 Pressed |
| 1 (uint8_t) | Motor Forward |
| 1 (uint8_t) | Motor Reverse |
| 1 (uint8_t) | Motor Speed Increase |
| 1 (uint8_t) | Motor Speed Decrease |
| 2 (uint16_t) | Rotational Velocity |

### Messages Structure

| Message Type | Byte 1-2<br>(uint16_t) | Byte 3<br>(uint8_t) | Byte 4<br>(uint8_t) | Byte 5-6<br>(uint16_t) | Byte 7-8<br>(uint16_t) |
|---|---|---|---|---|---|
| 1 | 0x01 | 0xFF | 0xFF | Button 1 Press | 0x20 |
| 2 | 0x02 | 0xFF | 0xFF | Button 2 Press | 0x21 |
| 3 | 0x03 | 0xFF | 0xFF | Button 3 Press | 0x22 |
| 4 | 0x04 | 0xFF | 0xFD | 0x50 | 0x23 |
| 5 | 0x05 | 0xFF | 0xFD | 0x51 | 0x24 |
| 6 | 0x06 | 0xFC | 0xFD | 0x52 | 0x25 |
| 7 | 0x07 | 0xFC | 0xFD | 0x53 | 0x26 |
| 8 | 0x08 | 0xFC | 0xFF | Gyroscope Data | 0x27 |
