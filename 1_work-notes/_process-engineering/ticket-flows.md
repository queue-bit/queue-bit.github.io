---
title:  "Model Ticket Flows"
excerpt: "Modelling ticket flows tips & tricks"
tags: "process engineering, ticket flows"
---

## Modeling Ticket Flows With Diagrams

Not all processes use tickets, but for those that do it is helpful to model them out in diagrams to gain additional insight and consensus on where improvements can/need to be made. I've additionally found it helpful for readers to include ticket flow diagrams within procedure documentation.

I'm using a fairly simple example here to show the diagrams and how they might be used, I'm intentionally not diving into how the example process can be improved.

### State Diagrams

I've discussed [State Diagrams for ticket flows before](state-diagrams.md), where I landed on this diagram to illustrate a simple ticket flow a Service Desk might use:

```mermaid
stateDiagram-v2
    [*] --> ToDo : New Ticket
    ToDo --> InProgress : Ticket Assigned
    InProgress --> Done : Ticket Completed

    InProgress --> Paused : Waiting for\n Response
    Paused --> InProgress : Got Response

    Paused --> ToDo : Needs\nRe-assignment
    Done --> [*] : Issue Closed
```

### Class Diagrams

We can build on our State Diagram by **misusing** a Class Diagrams, the structure of the diagram lends itself to illustrating additional information like Inputs, Outputs, and sub-processes.

```mermaid
classDiagram
    class CreateTicket{
        User creates a new ticket
        +String summary
        +String description
        ticket(summary,description)
    }
    class ToDo{
        Service Desk prioritizes ticket
        +int priority
        ticket(priority,status) SLA
    }
    class InProgress{
        SD Member assigns ticket
        to themself then works 
        the ticket
        +String comments
        ticket(comments,status)
        comms(questions) Pause Ticket
    }

    class Paused{
        - SD Member waiting for
        information.

        - Ticket is reassigned 
        if SD Member no longer
        available when info
        is provided.

        ticket(status)
    }
    class Done{
        Work is completed,
        ticket is closed

        ticket(status) closed
    }

    CreateTicket --> ToDo : Ticket
    ToDo --> InProgress : Self-Assigned
    InProgress --> Done : Ticket Completed
    InProgress --> Paused : Waiting for Response
    Paused --> InProgress: Got Response
    Paused --> ToDo: Needs Re-assignment
```

### Sequence Diagram

Mapping as a Sequence Diagram can also be helpful. 

What stands out in the diagram below is that the communication between the Service Desk and the User bypasses the ticketing system, this could lead to situations where the ticket does not contain all the information because it relies on the service desk member to add any back and forth to the ticket description.

```mermaid
sequenceDiagram
actor User
participant Ticket
actor SDLead
actor SDMember
    User->>Ticket: Create Ticket
    Ticket->>SDLead: New Ticket
    SDLead->>Ticket: Prioritize
    SDMember->>Ticket: Get Top Ticket
    Ticket->>SDMember: Ticket
    SDMember->>SDMember: Work Ticket
    loop
        SDMember-->>User: Request more info
        SDMember->>Ticket: Update Ticket: Paused
        User-->>SDMember: More info
        SDMember->>Ticket: Update Ticket: In Progress, more info
    end
    SDMember->>SDMember: Work Ticket
    SDMember->>Ticket: Comments / Solution
    SDMember->>Ticket: Mark Ticket Complete
    Ticket->>SDLead: Completed Ticket
    SDLead->>SDLead: Review
    alt Verified Resolved
        SDLead->>Ticket: Close Ticket
    else Not Resolved
        SDLead->>Ticket: Comment
        SDLead->>Ticket: Update Ticket: ToDo
        Note over Ticket,SDLead: Back to 'Prioritize'
    end
    Ticket-->>User: Issue Resolved Message

```

### User Journey

Taking a page out of Product Management, it can be helpful to map the User Journey for ticket flows. 

Try to think of ways to increase the happiness during the low steps. As an example, when the service desk member needs to ask for more information they're not happy, and the user isn't happy having to follow-up to the request, a possible solution is to adjust the ticket template to include examples or questions that reduce the likelihood of having to follow-up.

```mermaid
journey
    title Ticket Flow Example
    section New Issue
      Create Ticket: 2: User
      Prioritize Ticket: 3: SD Lead
    section Assign Ticket
      Review ToDo Tickets: 3: SD Member
      Assign next top item to self: 3: SD Member
    section Work Ticket
      Research Solution: 5: SD Member
      Implement Solution: 5: SD Member
      Test Solution: 4: SD Member
      Ask for more info: 2: SD Member
      Respond to info request: 2: User
      Wait for response: 1: SD Member
    section Complete Ticket
      Comment on solution: 3: SD Member
      Mark ticket Complete: 5: SD Member
      Close Ticket: 5: SD Lead
```