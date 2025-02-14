---
title: Block Diagram, Process Diagram, and Message Structure
---

## Block Diagram

### General Diagram
![Image](https://github.com/user-attachments/assets/940949f6-fcf2-4f78-bd3a-8c2ba29b47a6)

### Connector Diagram
![Image](https://github.com/user-attachments/assets/afec4950-839c-433e-a2cd-8bad1bd7e58a)

## Process Diagram

``` mermaid
sequenceDiagram
autonumber
actor In-Person User
In-Person User-->>Bruce: Change Motor Direction
Bruce->>Baron: Change Motor Direction
Baron->>Shaurya: Change Motor Direction<br>(Passes through pcb)
Shaurya->>Aadish: Change Motor Direction
Aadish->>Aadish: Motor Direction Changed<br>(Trash)
loop Every Millisecond
  Shaurya->>Aadish: Update Motor Speed
  Aadish->>Aadish: Motor Speed Updated<br>(Trash)
end
Shaurya->>Baron: Rotational Velocity
Baron->>Bruce: Rotational Velocity
Bruce-->>In-Person User: Display Rotational Velocity
actor Web User
Web User-->>Baron: Change Motor Direction
Baron->>Aadish: Change Motor Direction
Aadish->>Aadish: Motor Direction Changed<br>(Trash)
```

## Message Structure

| Message Type<br>byte 1-2<br>(uint16_t) | Description |
|---|---|
| 1 | Button 1 Pressed |
| 2 | Button 2 Pressed |
| 3 | Button 3 Pressed |
| 4 | Screen Select |
| 5 | Screen Back |
| 6 | Screen Cycle |
| 7 | Display on Screen |
| 8 | Motor Forward |
| 9 | Motor Reverse |
| 10 | Motor Speed Increase |
| 11 | Motor Speed Decrease |
| 12 | Rotational Velocity |
| 13 | Gyroscope Data |

### Single Byte Messages

| Message Type | Byte 1 |
|---|---|
| 1 | Button 1 (uint8_t) |
| 2 | Button 2 (uint8_t) |
| 3 | Button 3 (uint8_t) |
| 4 | 0x01 (uint8_t) |
| 5 | 0x02 (uint8_t) |
| 6 | 0x03 (uint8_t) |
| 7 | 0x04 (uint8_t) |
| 8 | 0x05 (uint8_t) |
| 9 | 0x06 (uint8_t) |
| 10 | 0x7 (uint8_t) |
| 11 | 0x8 (uint8_t) |
| 12 | 0x9 (uint8_t) |

### Multi Byte Messages

| Message Type | Byte 1 | Byte 2 |
|---|---|---|
| 13 | 0x10 (uint8_t) | 0x11 (uint8_t) |
