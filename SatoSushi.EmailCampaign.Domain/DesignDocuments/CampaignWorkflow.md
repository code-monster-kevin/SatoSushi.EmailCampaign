# Campaign Workflow
A service for automating communicating with anyone
Problem Domain:
Automate what, who and when to send email communications.


## Creating a new campaign
The steps to creating a new communication campaign

```mermaid
graph TB
S2 --> T2
C1 --> S1

subgraph Template
T1["Create Template Footer"] --> T2["Create Email Template"]
end

subgraph Communication Settings
S1["Create Communication Settings"] --> S2["Select Email Template"]
end

subgraph Campaign
C1["Create Campaign"] --> C2["Add Contacts To Campaign"]
end
```

## Communication Settings
The communication settings workflow

```mermaid
graph TB

subgraph Scheduler
A1["Get Active Campaign (End Date > Today > Start Date)"] 
--> A2["Get Contact List (Unsubscribe = false & Date Added + DayToWait >= Today)"]
--> A3["Add Contact to Email Task Queue"]
end

```

## Email Activity Tracking
The workflow for controlling email activity
```mermaid
graph TB

subgraph Send Email
S1["Send Email & Update Sent=true"] --> S2["Track Email"] --> S3{"Is email opened?"} --> S4["Yes"] & S5["No"]
end