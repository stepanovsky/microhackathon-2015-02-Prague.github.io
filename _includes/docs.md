Microservice Hackathon
======================

Welcome to the Microservice Hackathon!

Here you find all information required for you to work during the Hackathon.

# Link to the presentation

[Presentation about microservices](https://docs.google.com/presentation/d/1jwgrLaHw3B9nXyVEW0QxFtyTZy2FHjotooqWtXwaI5k/)

# Ok what should I do now? 

Well, let your team pick a service and start coding. Once you commit and push,
Jenkins will build that for you and upload your JAR to nexus. Next Rundeck will
deploy your application to the apps server. 

Each of the microservices will have a predefined port at which it will listen
to requests so you don't have to worry about that.

# I have a UI based microservice - where is my readme?!

Check this out [boot-microservice-gui-readme](https://github.com/4finance/boot-microservice-gui)

# I have a backend based microservice - where is my readme?!

Check this out [boot-microservice-readme](https://github.com/4finance/boot-microservice)

# I have to implement a microservice with a DB - what should I do?

For a relational DB use H2 in memory.

For a NoSQL one use [Fongo](https://github.com/fakemongo/fongo) in compile scope.

# How to run my microservice locally

We give you Spring profiles! Just add a system property:

```bash
-Dspring.profiles.active=dev
```

# Architecture

## Architecture draft

[Click to see the draft](

## Architecture plan

[Click to see the plan](https://docs.google.com/document/d/1dXub2V0U5cNk9-lLUgfeRRQ5yzGMJ8TQpS8iRRWWy5A/)

## Formats of incoming messages (only suggestion! decide yourself)

### fraud-detection-service

PUT /api/loanApplication/{loanApplicationId}

```json
{
    "firstName" : "text",
    "lastName" : "text",
    "job" : "text",
    "amount" : number,
    "age" : number
}
```

### loan-application-decision-maker

PUT /api/loanApplication/{loanApplicationId}

```json
{
    "firstName" : "text",
    "lastName" : "text",
    "job" : "text",
    "amount" : number,
    "fraudStatus" : "text"
}
```

GET /api/loanApplication/{loanApplicationId}
```json
{
    "applicationId" : "text",
    "result" : boolean
}
```

### client-service

POST /api/client

```json
{
    "firstName" : "text",
    "lastName" : "text",
    "age": number,
    "loanId" : "text" (This is actually the loan application identifier.)
}
```
### loan-application-aervice

POST /api/loanApplication

```json
{
    "amount": number,
    "loanId" : "text" (This is actually the loan application identifier.)
}
```

### reporting-service

POST /api/client

```json
{
    "firstName" : "text",
    "lastName" : "text",
    "age": number,
    "loanId" : "text" (This is actually the loan application identifier.)
}
```

POST /api/reporting

```json
{
    "loanId" : "text",
    "job" : "text",
    "amount" : number,
    "fraudStatus" : "text",
    "decision" : "text"
}
```

### marketing-offer-generator

PUT /api/marketing/{loanApplicationId}

```json
{
    "person" : {
        "firstName" : "text",
        "lastName" : "text"
    },
    "decision" : "text"
}
```

GET /api/marketing/{firstName}_{lastName}

```json
{
    "marketingOffer" : "text"
}
```

### ui

```
```
