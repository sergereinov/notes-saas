## Notes SaaS

This is a collection of small and simple learning pet projects.

The entire Notes Service (SaaS) as a whole is an analogue of the ToDo training task.

Basic goals / user stories:
1. Notes are folded into books (notebooks).
2. Notes have a custom structure that is common within the same book.
3. (task with an asterisk) Books can be put into bags (notebooks bags)

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
    BFF --> |REST,gRPC?| Auth
    BFF --> |REST,gRPC?| Notes
    Auth --> |gRPC/lib| Storage1
    Notes --> |gRPC/lib| Storage2
    Notes --> |gRPC| Auth
    
    Frontend["Frontend<br/>(html+js+react?)"]
    Kotlin["Mobile app<br/>(kotlin)"]
    subgraph Cloud
        BFF["BFF<br/>(nodejs?)"]
        subgraph M ["Services"]
            direction RL
            Auth["Auth<br/>(golang)"]
            Notes["Notes<br/>(golang)"]
        end
        subgraph S ["Services / DB"]
            Storage1[("Auth Storage<br/>(golang/3rd side)")]
            Storage2[("Notes Storage<br/>(golang/3rd side)")]
        end
    end
    
    classDef userspace fill:#f99
    class Frontend,Kotlin userspace
    style Cloud fill:#ffe
    classDef svc fill:#ffc
    class M,S svc
```

<p align="center"><b>Set of Auth services</b></p>

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
    
    subgraph Auth
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
    
    style Storage fill:#ffc
```

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
   
    style Storage fill:#ffc
```

## Prerequisites

Tools / Env.

## License

MIT
(TODO: add license file)

## Colab

Ask me.
