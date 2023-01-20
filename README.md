## Notes SaaS

This is a collection of small and simple learning pet projects.

The entire Notes Service (SaaS) as a whole is an analogue of the ToDo training task.

Basic goals / user stories:
1. Notes are folded into books (notebooks).
2. Notes have a custom structure that is common within the same book.
3. (task with an asterisk) Books can be put into bags (notebooks bags).
4. (task with an asterisk2) Use [rqlite](https://github.com/rqlite/rqlite) as storage.

Inspiration can be drawn from projects such as [Notion](https://www.notion.so).

Subproject learning patterns:
- Html + javascript
    - Html layouting + javascript + react,
    - Javascipt + nodejs development pipelines
    - Javascript REST API
    - JWT/Bearing tokens workout in js
- Kotlin/android modern practices
    - modern layouting
    - REST API
    - background services / worker manager
- Golang
    - Set of services
    - Separate auth pattern
    - JWT/Bearing tokens workout in golang
    - Scaling-ready architecture

## Thoughts

```mermaid
graph TD
    %% mermaid docs ref https://mermaid-js.github.io/mermaid/#/
    Frontend --> BFF
    Kotlin --> |REST| BFF
    BFF --> |REST,gRPC?| Account
    BFF --> |REST,gRPC?| Notes
    Account --> |gRPC/lib| Storage1
    Notes --> |gRPC/lib| Storage2
    Notes --> |gRPC| Account
    
    Frontend["Frontend<br/>(html+js+react?)"]
    Kotlin["Mobile app<br/>(kotlin)"]
    subgraph Cloud
        BFF["BFF<br/>(nodejs?)"]
        subgraph M ["Services"]
            direction RL
            Account["Account<br/>(golang)"]
            Notes["Notes<br/>(golang)"]
        end
        subgraph S ["Services/DB"]
            Storage1[("Account Storage<br/>(golang/3rd side)")]
            Storage2[("Notes Storage<br/>(golang/3rd side)")]
        end
    end
    
    classDef userspace fill:#f99
    class Frontend,Kotlin userspace
    style Cloud fill:#ffe
    classDef svc fill:#ffc
    class M,S svc
```

<details><summary>Hard mode</summary>

### Advanced tasks/things
_(think about it later)_
    
<p align="center"><b>Set of Notes services</b></p>

```mermaid
graph TD
    API --> |gRPC| Document
    API --> |gRPC| Fold
    
    Document --> DocumentDB
    Fold --> FoldDB
    
    subgraph Notes
        API["API gateway"]
        Document["Document<br/>(golang)"]
        Fold["Books and Bags folding<br/>(golang)"]
        
        subgraph Storage
            DocumentDB[("Documents<br/>DB")]
            FoldDB[("Folds<br/>DB")]
            MQ(("MQ/Saga<br/>(kafka)"))
        end
    end
   
    style Notes fill:#ffe
    style Storage fill:#ffc
```

<p align="center"><b>Set of Account services</b></p>

```mermaid
graph TD

    API --> |gRPC| Account
    API -.-> PermissionAPI
    Account --> |gRPC| Authentication
    Account --> |gRPC| Permission
    PermissionAPI --> |gRPC| Permission
    
    Account --> UserDB
    Authentication --> AuthenticationDB
    Permission --> PermissionDB
    
    subgraph Acc["Account"]
        API["API gateway"]
        Account["Account/User<br/>(golang)"]
        Authentication["Authentication<br/>(golang)"]
        PermissionAPI(["Permissions API"])
        Permission["Permissions/Authorization<br/>(golang)"]
        
        subgraph Storage
            AuthenticationDB[("Authentication<br/>DB")]
            UserDB[("Users/Personal Info<br/>DB")]
            PermissionDB[("Permissions<br/>DB")]        
            MQ(("MQ/Saga<br/>(kafka)"))
        end    
    end
    
    style Acc fill:#ffe
    style Storage fill:#ffc
```

(draft) Permission structure: (by who) -  (to whom) -  (of what) - (and how)

<details><summary>Account subsequences</summary>

```mermaid
sequenceDiagram
    participant acc as Account<br/>service
    participant auth as Authentication<br/>service
    participant perm as Permissions<br/>service
    participant accdb as Account<br/>DB
    participant authdb as Authentication<br/>DB
    participant permdb as Permissions<br/>DB
    
    Note over acc,permdb: Create new user
    Note over acc,permdb: Delete the user
    Note over acc,permdb: Update password
    Note over acc,permdb: Update personal information
    Note over acc,permdb: Read personal information
    
    Note over acc,permdb: Find users

    Note over acc,permdb: Verify credentials (log in)
    
    Note over acc,permdb: Add permission
    Note over acc,permdb: Remove permission
    Note over acc,permdb: Check permission
    Note over acc,permdb: List permissions
```

</details>

</details>

## Prerequisites

Tools / Env.

## License

MIT
(TODO: add license file)

## Colab

Ask me.
