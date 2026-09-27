# Trooper

## Tech Stack
- [x] Chi router
- [ ] Sqlc
- [ ] goose for migrations
- [x] Postgres RDB
- [x] Redis
- [x] Cassandra
- [ ] Kafka


## Directory structure

```
│
├── /cmd
│   ├── /task-service
│   │   ├── main.go           ← entry point: HTTP server startup
│   │   └── /handler          ← HTTP handlers, specific to this binary
│   │       └── task.go
│   │
│   ├── /relay-node
│   │   ├── main.go           ← entry point: starts relay loop
│   │   └── /relay            ← relay-specific logic (polling, batching)
│   │       └── relay.go
│   │
│   ├── /scheduler-node
│   │   ├── main.go           ← entry point: starts scheduler loop
│   │   └── /scheduler        ← scheduling logic (sweep, cron parsing)
│   │       └── scheduler.go
│   │
│   └── /worker-node
│       ├── main.go           ← entry point: starts worker loop
│       └── /worker           ← worker logic (task execution, HTTP dispatch)
│           └── worker.go
│
└── /internal
    ├── /config               ← shared config loading (env vars, etc.)
    │   └── config.go
    │
    ├── /db                   ← postgres connection pool setup
    │   └── db.go
    │
    ├── /redis                ← redis client setup and wrappers
    │   └── redis.go
    │
    ├── /task                 ← core domain: Task struct, Status enum, etc.
    │   └── task.go
    │
    ├── /repository           ← all DB queries live here (used by multiple nodes)
    │   ├── task_repo.go      ← e.g. GetDueTasks, UpdateStatus, CreateTask
    │   └── lock.go           ← SELECT FOR UPDATE SKIP LOCKED helpers
    │
    └── /queue                ← message queue abstraction (publish/consume)
        └── queue.go  
```
