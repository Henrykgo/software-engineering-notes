A python framework for building APIs. It uses Python type hints to provide input validation and automatic API documentation, and it supports async endpoints.

#### What it gives
- Validation: define the expected request with a Pydantic model; FastAPI validates the input automatically
- Docs: automatically generate interactive API docs
- Async: `async def` lets the server handle other requests while waiting for slow I/O, such as an LLM or external API call

## FastAPI vs Flask

| | Flask | FastAPI |
|---|---|---|
| Validation | manual or extension | automatic from Pydantic models |
| API docs | extension | automatic at `/docs` |
| Async | add-on | built in |
| Best for | small tools, full control | APIs, I/O-heavy backends, LLM apps |

### Connecting a database
1. **Engine** --> creates and manages a pool of database connections. It is created once when the application starts.
2. **Session** --> a request gets a session to talk to the database. It runs queries and commits or rolls back changes.
3. get_db() Depends() --> makes sure each requests gets a session and that it is closed when the request finishes (returns it)

```
Application starts
       ↓
    Engine
       ↓
Connection pool
 ┌─────┬─────┬─────┐
 │ DB  │ DB  │ DB  │
 │ conn│ conn│ conn│
 └─────┴─────┴─────┘
       ↓
Request arrives
       ↓
Session gets a connection
       ↓
Run queries
       ↓
Request finishes
       ↓
Connection goes back to pool
```

### Sync vs Async
most of the request's time is spend waiting for the database, for an LLM, for another API. What does the server do while waiting?

- **Sync** (`def`): the handler waits for the operation to finish. The thread handling the request is blocked while waiting.
- **Async** (`async def`): when the handler hits `await` it pauses and the server can handle other requests. When the response arrives, the handler resumes.

Key idea: Async is useful for I/O-heavy work because one process can keep many requests waiting on external services without needing a separate thread for each one.
