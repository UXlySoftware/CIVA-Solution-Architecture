## Poll User Shape ERD

``` mermaid

--- 
title:Poll, User and Shape
---
erDiagram

    Poll {
            ObjectID id
            string pollType
            string title
            string headline
            ObjectId createdBy
            ObjectId updatedBy
            string jurisType
            string status
            string[] shapeIds
            int pollQuestionsNumber
            PollQuestions[] pollQuestions
            Answer[] answer
            string[] attachments
            string access
            int targetAudienceAdmin
            int targetAudienceMembers
            int potentialAudienceAdmin
            int potentialAudienceMembers
            date schedule
            ObjectId audienceGroup
            date createdAt
            date updateAt

    }
    Answer {
        string ansId
        string ans
        striing questionId
        ObjectId[] userIds
    }
    
    PollQuestions {
        string ques
        string questionId
    }
    Name {
        string first
        string last
    }
    Shape {
        ObjectId _id
        bool Locked_Community
        string ShapeId
        Location location
        bool published
    }

    Location {
        Properties properties
        string type
        LatLng[] coordinates

    }

     Properties {
        string JurisTypeID
        string JurisCat
        string State
        string JurisType
        string JurisTypeName
        string JurisLabel
        string Country
        string ShapeID

     }



User {
            ObjectID id
            string email
            Name name
            int countryCode
            int phoneNo
            string roles
            string address
            string[] politicalShapeId
            string[] primaryPoliticalShapeId
            string photoUrl
            ObjectId company
            string companyRole
            date createdAt
            date updateAt

    }

Poll ||--o{  Shape : "belongs to"
User ||--o{ Shape : "belongs to"

```

