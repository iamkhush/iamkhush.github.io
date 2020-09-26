---
title: "Understanding the Postgre's Wire Protocol"
date: 2020-09-26T00:04:06+02:00
type: 'post'
tags: [Postgres, Database]
---

## Introduction to Postgres Wire Protocol

Postgres uses *Message based protocol* to comunicate between clients( for eg. `psql`) and DB server.
- Current version is 3.0
- Supports TCP/IP and Unix domain sockets (IPC Sockets).
- Each connection goes through 3 phases - 
  - [Startup Phase]({{< ref "#startup-phase" "Startup Phase">}})
  - [Normal Phase]({{< ref "#operations-in-normal-phase" >}})
  - [Termination Phase]({{< ref "#termination-phase">}})


### Startup Phase
- Client opens connection by sending startup message.
- The structure of a startup message is as follows - 

|<--1 byte-->|<-----4 bytes------->| |
|---|---|---|
| Message Type  | Length of message  | Message Data |
|   |   |   |

- Client also sends authentication information in message data.
- Server responds with success or failure message and accordingly Normal phase is entered
- Interesting to note, server launches a new process for each client connection.

### Operations in Normal Phase
- Client sends query and Server responds.
- Query can use either of 2 sub-protocols -
  - A simple query protocol in which only a textual SQL query is sent.
  - An Extended Query Protocol which includes 3 steps
    1) *Parse* step which creates a prepared statement from a textual query. It may have a name, in which case it is optimized for multiple uses.
    2) *Bind* step which creates a portal given a prepared statement ( from step 1) and values for any parameters.
    3) *Execute* step which runs the portal's query.

### Termination Phase
- Normally initiated by client
- Server responds and roll backs any incomplete transactions

Check out my [next post]({{< ref "deep-dive-into-postgres-wire-protocol.md" >}} "Deep Dive into PostGres Wire Protocol") we will go deep dive into each phase. 

Source - 
- https://www.postgresql.org/docs/12/protocol-overview.html
- https://www.postgresql.org/docs/12/protocol.html

