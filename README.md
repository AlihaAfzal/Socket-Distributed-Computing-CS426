# Socket-Based Distributed Computing (TCP)

**Course:** Parallel and Distributed Computing
**Course Code:** CS426
**Assignment 2**
**Submitted by:** Aliha Afzal


## Task 1 – Collaborative Messaging Environment (Chat System)

### Description

This task implements a **real-time text chat system** using TCP sockets in C#.
Multiple users connect to a shared server (Coordinator), and all messages are broadcast to every connected client.
The environment supports multiple clients communicating simultaneously.

### Files

* **ChatServer.cs** – Central server handling connections and message broadcasting.
* **ChatClient_Aliha.cs** – Client program (User 1).
* **ChatClient_Liha.cs** – Client program (User 2).

### Example Users

* Aliha
* Liha

### Message Flow

1. The **server** listens for connections on port 9000.
2. Each **client** connects, enters a username, and starts sending messages.
3. The server receives each message and broadcasts it to all connected clients.
4. All client messages are shown in real time on every participant’s console.

### Concurrency Handling

* Each connected client runs in its **own thread** on the server.
* A **shared list** stores all client connections; it is protected with `lock` to avoid race conditions.
* Thread-safe broadcasting ensures message order and avoids data corruption.

### Example Output

**Server Window:**

```
[Server] Listening on port 9000...
[Server] Aliha connected.
[Server] Liha connected.
[Broadcast] Aliha: Hello everyone!
[Broadcast] Liha: Hi Aliha!
```

**Client (Aliha):**

```
Connected to chat server.
Type your messages below.
> Hello everyone!
Liha: Hi Aliha!
```

**Client (Liha):**

```
Connected to chat server.
Type your messages below.
> Hi Aliha!
Aliha: Hello everyone!
```


## Task 2 – Networked Quiz Coordinator (Distributed Quiz System)

### Description

This task builds a **TCP-based distributed quiz system** where a quiz server sends questions to all participants.
Each participant answers within a time limit and receives a score summary at the end.



### Example Participants

* Aliha
* Ansa

### Timing

* Each question has **60 seconds** time .

### Concurrency Handling

* Each participant is handled in a **separate thread** by the quiz server.
* Shared score data is protected with `lock` for thread safety.
* The server manages synchronization to ensure all participants get questions simultaneously.

### Example Output

**Server Window:**

```
[Server] Quiz started.
[Server] Sending Question 1 to all participants.
Aliha answered: A
Ansa answered: B
[Server] Scoring complete.
Final Scores:
Aliha: 3
Ansa: 2
```

**Client (Aliha):**

```
Connected to Quiz Server.
Question 1: What is the capital of France?
A) Paris  B) London  C) Berlin
> A
Correct!
```

**Client (Ansa):**

```
Connected to Quiz Server.
Question 1: What is the capital of France?
A) Paris  B) London  C) Berlin
> B
Incorrect. Correct answer: A
```


## Summary of Concurrency Handling

| Feature         | Task 1 (Chat)                | Task 2 (Quiz)                |
| --------------- | ---------------------------- | ---------------------------- |
| Model           | Multi-threaded TCP           | Multi-threaded TCP           |
| Synchronization | `lock` on client list        | `lock` on score list         |
| Thread Role     | Broadcast messages           | Manage participants & scores |
| Safety          | Thread-safe message handling | Thread-safe scoring system   |
