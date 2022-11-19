## Notes SaaS

This is a collection of small and simple learning pet projects.

Learning patterns:
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
    F --> B
    K --> |REST| B
    B --> |REST,gRPC?| A
    B --> |REST,gRPC?| N
    A --> |gRPC/lib| S1
    N --> |gRPC/lib| S2
    
    F["Frontend<br/>(html+js+react?)"]
    K["Mobile app<br/>(kotlin)"]
    subgraph Cloud
        B["BFF<br/>(nodejs?)"]
        subgraph M ["Services"]
            A["Auth<br/>(golang)"]
            N["Notes<br/>(golang)"]
        end
        subgraph S ["Services / DB"]
            S1[("Auth Storage<br/>(golang/3rd side)")]
            S2[("Notes Storage<br/>(golang/3rd side)")]
        end
    end
    
    classDef userspace fill:#f99
    class F,K userspace
    style Cloud fill:#ffe
    classDef svc fill:#ffc
    class M,S svc
```

## Refs
- mermaid docs https://mermaid-js.github.io/mermaid/#/
