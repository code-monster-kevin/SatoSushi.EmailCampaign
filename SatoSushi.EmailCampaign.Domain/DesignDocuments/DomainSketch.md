# Email Campaign Service Domain

The Problem Domain:
1. Who to send
2. What to send
3. When to send

Campaign -> stores the details of who, what and when to send. \
CampaignContact -> stores the contacts linked to the campaign. \
Contact -> the master list of all contacts for the entire application. \
ContactModel -> Additional information that will be used by the email template to personalize the email communication

```mermaid
classDiagram

Campaign --* CampaignContact : has a
CampaignContact --* Contact : associate
CampaignContact --* ContactModel : has a

class Campaign{
    +String Title
    +DateTime StartDate
    +DateTime EndDate
    +CampaignWorkflow CampaignWorkflow
}

class CampaignContact{
    +Contact Contact
    +Campaign Campaign
}

class Contact{
  +String Email
  +String Name
  +Bool IsUnsubscribed
  +Unscubscibe()
}

class ContactModel{
    +String Field1
    +String Field2
    +String Field3
}


```
### Campaign Detail

```mermaid
classDiagram

Campaign "1" --* "1" CampaignWorkflow : has a
CampaignWorkflow --> QueAction
CampaignWorkflow --> EmailTemplate
CampaignWorkflow --> CampaignWorkflow : action

class Campaign{
    +String Title
    +DateTime StartDate
    +DateTime EndDate
    +CampaignWorkflow CampaignWorkflow
}

class CampaignWorkflow{
    +EmailTemplate EmailTemplate
    +int DayToWait
    +QueAction QueAction
    +CampaignWorkflow CampaignWorkflow
}

class QueAction{
    <<enumeration>>
    NEW
    SENT
    OPENED
}

class EmailTemplate{
    +String Title
    +String Subject
    +String Content
}
```

## Email Communication Workflow
Once the campaign is setup, the email scheduler will trigger the communication tasks

### Email Scheduler
```mermaid
graph TB
A1 --> A2
A2 --> A3
A2 --> A4
A4 --> A6
A3 --> A5
A1["Email Scheduler"]
A2{"Any Active Campaigns?"}
A3["Yes"]
A4["No"] 
A5["Campaign WorkFlow"]
A6["End"]

```

### Campaign Workflow
Campaign Workflow determines the what and when to send, creates the task queue for actual sending of the emails

```mermaid
graph TB
A1 --> A2
A2 --> A3
A3 --> A4
A3 --> A5
A4 --> A6
A5 --> A7

A1["Start"]
A2["Get Campaign Contacts (Unsubscribed == false)"]
A3{"Is Contact Added To MailQue?"}
A4["Yes"]
A5["No"]
A6["End"]
A7["Add Contact to MailQue"]
```





### Reference:
Mermaid JS
Class Diagrams: [https://mermaid-js.github.io/mermaid/#/classDiagram]