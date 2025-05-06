---
title: Block/Process Diagrams & Message Structure
---

## Block Diagram

![image](https://github.com/user-attachments/assets/4ef2de21-2632-4618-a25a-40dea04b6c11)

### Block Diagram Decision Making Process

This block diagram allows for both devices to be powered, programmed, and communicate to one another. It meets all the class requirements for things like uart and power but also fits our projects unique MQTT requirements. It also has some basic debug components for testing.

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

### Process Diagram Decision Making Process

This semester emphasises uart communication so boards can interact with one another. Our project uses MQTT for communication, but uart is still a backup. This diagram allows us to send any data we could recieve to where it needs to go and it allows in person and web users to interact with it.

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

### Message Structure Decision Making Process

This was the most customizable part of our project. We needed a way to send data to one another, know where its comming from, and who its going to. To do this we defined the start and end of a message with 2 bytes. This will tell the board when a message is being recieved. Within this message is bytes of data that define the sender, reciever, and data. This is always in the same location in the message to its easy to identify what is where. This message structure allows us to identify bad messages and messages that arent meant for a specific board so they can be passed on.

## Top 5 Changes

- Prefix and suffix

The prefix and suffix used to be different per message type. We later realized that its easier to make any message prefix and suffix the same and identify the message type by the sender becuase each message type only comes from one specific sender.

- Amount of messages

Because our team split last minute, we had to remove a handful of message types that werent going to be used. This cut down on the message types by quite a bit

- Data Storing

We used to store the 2 byte data types in 2 seperate variables, but later we realized this is a bad idea because it makes things harder to manage. Plus it was completely unnecessary because 1 variable can store more than 1 byte. So we changed it to exactly that. We now store multiple bytes of data in one variable and then run a data.to.bytes command to convert it for sending.

- Data length

We currently use 2 bytes to store data. This was because the rotational velocity was going to be 2 bytes long, but now we dont have that sensor so we would ideally make the new data only 1 byte long because thats all we need.

- Sender and Reciever Length

We were originally going to send full names as the sender and reciever bytes. We realized this is impractical becuase it would either require converting it to hex or binary, or it would take more than 1 byte. So we make it one letter as the identifier so now its easier to send that data.
