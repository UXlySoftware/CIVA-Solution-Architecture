This server architecture shows the layers. There are two kinds of requests:

1. request involving dynamic data for which one needs to access the api and data
2. request involving static data only for which the content can be directly served by a CDN without accessing the API servers

```mermaid
sequenceDiagram

    participant U as User
    participant LB as LoadBalancer
    participant DDOS as DDOS Protection
    participant API as API Servers
    participant Auth as Auth Server
    participant S3 as Cloud Storage
    participant DB as Databases
    participant CDN as Content Delivery Network

    Note over U, LB: request dynamic data
    activate U
        U ->> LB: request dynamic data
        activate LB
            LB -->> DDOS: forward
                alt attack detected
                    Note over DDOS: attacked
                    activate DDOS
                    DDOS -->> U: deny request
                    deactivate DDOS
                else
                    LB -->> API: forward
                        alt not authorized
                            Note over API: unauthorized action
                            activate API
                            API -->> Auth: get authorization
                                activate Auth
                                Auth -->> API: not authorized
                                deactivate Auth
                            API -->> U: deny request
                            deactivate API

                        else authorized
                            Note over API: authorized action
                            activate API
                            API -->> Auth: get authorization
                                activate Auth
                                Auth -->> API: authorized
                                deactivate Auth

                            activate DB
                            activate S3
                                Note over API, DB: process request and data
                                API -> DB: database access
                                API -> S3: file storage access
                            deactivate DB
                            deactivate S3
                            API -->> U: response
                            deactivate API
                        end
                end
        deactivate LB
    deactivate U


    Note over U, LB: request static files (e.g., images, videos, files)
    activate U
        U ->> LB: request static files
        activate LB
            LB -->> DDOS: forward
                alt attack detected
                    Note over DDOS: attacked
                    activate DDOS
                    DDOS -->> U: deny request
                    deactivate DDOS
                else
                    LB -->> CDN: forward
                    activate CDN
                        alt data missing
                            CDN -->> S3: Sync files
                        end
                    deactivate CDN
                    CDN -->> U: serve file
                end
        deactivate LB
    deactivate U

```
