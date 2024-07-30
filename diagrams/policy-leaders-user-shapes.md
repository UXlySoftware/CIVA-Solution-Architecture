## Policy/Legislation User Leaders ERD
## Policy ~ Grant 
``` mermaid

--- 
title: User and Shape
---
erDiagram

    Leader {
            ObjectID id
            string CandidateStatus
            int UniqueEntryID
            string Country
            string Email
            string Facebook
            string State
            string JurisCat
            string JurisLabel
            string JurisType
            string JurisTypeId
            string JurisTypeName
            string[] LegisId
            string LinkedIn
            string fullName
            string Phone
            string PhotoURL
            string Position
            string[] ShapeId
            string Twitter
            string Website
            string Youtube
            ObjectId updatedBy
            boolean isDeleted 
            date createdAt
            date updateAt

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

Policy {
       string[] ShapeId
       string jurisCat
       string[] communityGoals
       string title
       string url
       string summary
       string legisId
       string jurisType
       string jurisTypeName
       string policyType
       ObjectId createdBy
       ObjectId updatedBy
       ObjectId resourceType
       string grantCode
       string grantTitle
       string grantAgencyCode
       string grantAgency
       string grantStatus
       date grantPostedDate
       date grantCloseDate
       string grantCategory
       string grantEligibilty
       string grantContactName
       string grantContactEmail
       string grantPhoneNo
       string grantAgencyWebsite
       string grantUrl
       ObjectId[] associatedleaders
       boolean isDeleted
       string lawNum
       string policyArea
       string type
       string fiscalYear
       string passageDate
       string state
       date createdAt
       date updateAt
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

Leader ||--|| Shape : "belongs to"
User }o--o{ Shape : "belongs to"
Policy ||--|| Shape :"belongs to"

```

