flowchart LR
  Client["Client (mobile/web)"]
  GQL["GraphQL Gateway"]
  subgraph Backend [Microservices / Resources]
    Auth["Auth Service"]
    Users["User Service"]
    Posts["Posts Service"]
    Comments["Comments Service"]
    DB["Databases / Storage"]
    Cache["Cache / DataLoader"]
  end

  Client -->|GraphQL Query| GQL
  GQL -->|auth check| Auth
  GQL -->|batch user ids| Users
  GQL -->|fetch posts| Posts
  GQL -->|fetch comments| Comments
  Posts -.->|reads/writes| DB
  Users -.->|reads/writes| DB
  Comments -.->|reads/writes| DB
  GQL -->|use dataloader| Cache
  Cache --> Users
  Cache --> Posts
