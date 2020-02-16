# Email Campaign Service Domain Models

### Contacts
The persons that we want to communicate with
```mermaid 
classDiagram

Contact "1" --* "many" Address : Composition
class Contact{
  +String Email
  +String Name
  +String IdentityNo
  +String PhoneNo
  +Unsubscribe()
}

class Address{
  +String Street1
  +String Street2
  +String City
  +String State
  +String PostCode
  +String Country
}
```

### Email Template
The communication content to be sent to the contacts
```mermaid 
classDiagram

EmailTemplate "1" --* "1" TemplateFooter : Composition
class EmailTemplate{
  +String Title
  +String Subject
  +String Content
}

class TemplateFooter{
  +String Content
}
```

### Campaign
The main entry point for setting up the communication campaign

```mermaid 
classDiagram

class Campaign{
  +String Title
  +DateTime StartDate
  +DateTime EndDate
  +String Description
}

```

### Campaign Settings
The behaviour and communication plans for the campaign

```mermaid 
classDiagram

CampaignSettings <|-- Action : Implements

class CampaignSettings{
  +EmailTemplate EmailTemplate
  +int DayToWait
  +Action Action
}

class Action{
  <<enumeration>>
  ALL
  OPENED
  UNOPENED
}
```

### Email Task
The queue to track emails to be sent

```mermaid
classDiagram

class MailQue{
  +CampaignWorkflow CampaignWorkflow
  +Contact Contact
  +QueStatus QueStatus
}

class QueAction{
  <<enumeration>>
  NEW
  SENT
  OPENED
}

```

