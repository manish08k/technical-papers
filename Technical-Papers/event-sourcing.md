# Event Sourcing Architecture

## Referred Links

- https://www.geeksforgeeks.org/system-design/event-sourcing-pattern/
- https://newsletter.scalablethread.com/p/what-is-event-sourcing
- https://www.youtube.com/watch?v=HKspPiCGE2E

## Introduction

Event Sourcing is used to store data not only current one but also history of the process.

## Summary

Event sourcing is storing every update of event instead of updating previous one.

It is simple to understand the architecture where there are different components in the process:

- Event Source
- Publisher
- Queue/Event broker
- Consumer

So the architecture is simple and the process too.

First Event Source like if something happens then it generates events.

And after publisher publishes the event.

As we know queue/Event broker is used for distributing events and all in a manner and make it in an order. Then after consumers receive that, we can say different consumers do different things like business logic, Database update, Notification Workflow.

It is mainly used in banks and E commerce where the data is important thing.

It stores previous data too so when the data is needed then it generates all information from where it is needed.

There is use of snapshots too that makes work simpler. For example, a user needs data of his previous transactions so this snapshots will work as like it is saved state of specified entity where it sends from there instead of replaying from starting of the data.

## Architecture Flow

USER → COMMAND → COMMAND HANDLER → AGGREGATE → EVENT → EVENT STORE → EVENT PUBLISHER → EVENT HANDLER → PROJECTION → READ MODEL
