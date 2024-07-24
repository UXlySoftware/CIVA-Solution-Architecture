## Community ERD

This ERD captures all the relationships between communities and other entities

### Questions

1. Can a community have more than 1 president?
2. Can a community have more than 1 treasurer?

**Used generic string types for many field. If any of this has branded type in the backend code, please update them**

```mermaid
---
title: Community and Community Membership
---
erDiagram

    Community {
        ObjectID id
        boolean verfied
        string name
        string communityType
        string address
        ShapeId gisShape
        GoalId[] goals
        date createdAt
        data updatedAt
        Member[] members
        string chatRoomId
        float lat
        float lng
        string city
        string jurisType
        string state
        string[] politicalShapeIds
    }

    Member {
        string _id
        string userId
        string role
        date joinedAt
        timestamp lastActive
        string status
        string[] notification
    }


    Community 1--0+ Member: member

```

There are some cardinality issue depicted below with membership

```mermaid
---
title: Community Roles Issues
---
erDiagram
    Community 1--0+ User: president
    Community 1--0+ User: treasurer
    Community 1--0+ User: volunteer
```

```mermaid
---
title: Community Roles Suggestion
---
erDiagram
    Community 1--zero or one User: "one president"
    Community 1--zero or one User: "one treasurer"
    Community 1--0+ User: "many volunteer"
```

```mermaid
---
title: Community and Community Goals
---
erDiagram
    Goal {
        ObjectId _id
        string name
        string goalId
        URL img
        UserId updatedBy
        date createdAt
        data updatedAt
        int ___v
    }

    Community 0+--0+ Goal: has

```

```mermaid
---
title: Community and Community Shapes
---
erDiagram
    Shape {
        ObjectId _id
        bool Locked_Community
        string ShapeId
        Location location
        bool published
    }

    Location {
        unknown properties
        string type
        LatLng[] coordinates
    }

    Community 0+--0+ Shape: has

```
