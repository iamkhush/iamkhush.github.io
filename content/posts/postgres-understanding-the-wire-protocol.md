---
title: "Understanding Postgre's Wire Protocol"
date: 2020-09-26T00:04:06+02:00
type: 'post'
tags: [Postgres, Database]
summary: "Let's break down the offical Postgres's message based communication protocol."
---

## Introduction to Postgres Wire Protocol

Postgres uses *Message based protocol* to comunicate between clients( for eg. `psql`) and DB server.
I will try to summarize some aspects of the protocol.
- Current version is 3.0
- Supports TCP/IP and Unix domain sockets (IPC Sockets).
- Each connection goes through 3 phases - 
  - [Startup Phase]({{< ref "#startup-phase" "Startup Phase">}})
  - [Normal Phase]({{< ref "#operations-in-normal-phase" >}})
  - [Termination Phase]({{< ref "#termination-phase">}})

![Connection Phases between Client and PG server](/postgres/conn-phases.png) 

### Startup Phase
- Client opens connection by sending startup message ( See 1 in the figure above )
    - The structure of a startup message is as follows - 

|4 byte|4 bytes| |
|---|---|---|
| Length of message | Protocol Version | Message Data like username, database name etc 
- Server checks the message data from above and also its own config files, to determine the response, which can be one of the following - 
  - A success response (`AuthenticationOk`) ( 3a in the figure )
  - An error response (`ErrorResponse`) ( 3b in the figure )
  - Authentication related messages( like `AuthenticationMD5Password`)
  - Protocol negotiation response (`NegotiateProtocolVersion`)
- If the response was `AuthenticationOk` then server sends some more messages( 4 in the figure ), but the most important of them is `ReadyForQuery` message( 5 in the figure ). Once sent, the next phase (Normal phase) is initiated.
- Server launches a new process for each client connection.
- Also interestingly, other than the startup message, the message format is 

|1 byte|4 bytes| |
|---|---|---|
| [Message Type][1]  | Length of message  | Message Data depending on Message Type 


### Operations in Normal Phase
- Client sends query message and Server responds accordingly.
- When server parses the query, it does the following steps - 
  1) *Parse* step which creates a prepared statement from a textual query. It may have a name, in which case it can be reused multiple times, hence optimizing response times. This step can be done manually using `PREPARE`  SQL.
  2) *Bind* step which creates a portal given a prepared statement (from step 1) and values for any parameters. Again, it may have a name as well. Query planning happens after this step completes. Can be done by SQL `CREATE CURSOR` and `FETCH`.
  3) *Execute* step which runs the portal's query. Also can be called manually by SQL `EXECUTE`.
  4) *Sync* step which completes the query transaction.
- Query can use either of 2 sub-protocols -
  - A **simple query protocol** in which only a textual SQL query is sent.
    - Backend creates an unnamed prepared statement, portal and executes it.
    - It then responds with one or more response messages, finally ending the response with `ReadyForQuery` Message.
    - Interestingly, if the query contains multiple SQL statements ( seperated with a `;`), a `CommandComplete` is sent after each statement is executed. However `ReadyForQuery` is only issued after all queries are completed. If there is any error raised in any one of them, all the statements are rolled back, first `ErrorResponse` is responded followed by a `ReadyForQuery`
    - Also,  there is no need for client to wait for `ReadyForQuery` and can send further queries if it wants.
  - An **Extended Query Protocol** does the 3 steps as seperate statements.
    - For response of *Parse* step, `ParseComplete` response is sent.
    - For response of *Bind* step, `BindComplete` response is sent.
    - For response of *Execute* step, `CommandComplete` response is sent.
    - For response of *Sync* step, `ReadyForQuery` response is sent.
    - Important to note that it cannot parse multiple SQL statements, unlike Simple Query protocol.
    - A *Sync* needs to be sent everytime to end a transaction. 
    - However, one can send multiple *Bind* and *Execute* messages, for same portal without waiting for `ReadyForQuery`.
      - A web application can use this feature to get async responses of its queries.
- One important caveat is that a prepared statement cannot be shared between different processes / connections. It only lives for 1 session. 
- Checkout my pg-client implementation script [here](https://gist.github.com/iamkhush/8612c62be915e554d9430b65fcd7d2d9)

### Termination Phase
- Normally initiated by client
- Server responds and roll backs any incomplete transactions.

Sources - 
- https://www.postgresql.org/docs/12/

[1]: https://www.postgresql.org/docs/current/protocol-message-formats.html

