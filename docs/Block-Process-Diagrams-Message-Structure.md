---
title: Block/Process Diagrams & Message Structure
---

## Block Diagram

![image](https://github.com/user-attachments/assets/4ef2de21-2632-4618-a25a-40dea04b6c11)

## Process Diagram

``` mermaid
sequenceDiagram
autonumber
actor In-Person User
participant Bruce
participant Baron
actor MQTT
In-Person User->>Bruce: Toggle Motor
Bruce-->>MQTT: Toggle Motor
MQTT-->>Baron: Toggle Motor
Baron->>Baron: Motor Toggled<br>(Trash)
MQTT-->>Baron: Toggle Motor
Baron->>Baron: Motor Toggled<br>(Trash)
```
>Edit: UART communication was supposed to happen between Baron and the old team 309 members. However, with team 309B, only the mqtt server will be used for communication. Due to the nature of the project, it makes more sense to communicate over wifi rather than uart.

## Message Structure

### IDs

Each user has been assigned a user ID to make communication easier between users. Any messages sent will contain the sender and reciever ID to identify where its coming from and where its going to. Below is a list of IDs for each user in our project

| ID | User |
|---|---|
| M | Bruce |
| B | Baron |

### Message Types

The message types are defined by the Process Diagram. Our Process Diagram only has 3 types of messages that are send between users, so below are those messages and their functions.

| Message Type | Description |
|---|---|
| 1 | Toggle Motor |

### Message Variations

While message types are meant to define each message in the Process Diagram, there can be multiple variations within a message type. A motor direction message can mean to move the motor forward or reverse, so below is a breakdown of each message variation in each type and its ID.

| Message Type | Variations | ID |
|---|---|---|
| 1 | Motor Start | 0x0040 |
| 1 | Motor Stop | 0x0041 |

### Messages Structure

This is a breakdown of how serial messages will be sent. It shows each byte in a message and what its use is.

- Any messages sent to Bruce will be sent to Baron through UART and then sent to Bruce through MQTT server.
- Any messages sent from Bruce will be sent to Baron through MQTT server and then sent to there respective user through UART.

| Message Type | Byte 1-2 (Prefix)<br>(uint16_t) | Byte 3 (Sender ID)<br>(uint8_t) | Byte 4 (Reciever ID)<br>(uint8_t) | Byte 5-6 (Data)<br>(uint16_t) | Byte 7-8 (Suffix)<br>(uint16_t) |
|---|---|---|---|---|---|
| 1 | AZ | Bruce | Baron | Motor Start | YB |
| 1 | AZ | Bruce | Baron | Motor Stop | YB |

>Edit: The bulk of out messages got removed when transfering to team 309B. We no longer have an offical sensor or actuator system so this is the best we could do in the time we had
