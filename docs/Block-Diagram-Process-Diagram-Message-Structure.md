---
title: Block Diagram, Process Diagram, and Message Structure
---

## Block Diagram



## Process Diagram

``` mermaid
sequenceDiagram
autonumber
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
Web User-->>Baron: Change Motor Direction
Baron->>Aadish: Change Motor Direction
Aadish->>Aadish: Motor Direction Changed<br>(Trash)
```

## Message Structure

