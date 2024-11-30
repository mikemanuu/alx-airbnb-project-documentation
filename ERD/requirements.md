# Entity-Relationship Diagram (ERD) Creation

## Objective
This project involves creating an Entity-Relationship Diagram (ERD) to visually represent the database schema and relationships between entities based on the given specifications.

## Description
The ERD includes the following entities:
1. *User*
2. *Property*
3. *Booking*
4. *Message*
5. *Review*
6. *Payment*

### Entities and Attributes
- *User*
  - UserID (Primary Key)
  - Name
  - Email
  - Phone
  - Address

- *Property*
  - PropertyID (Primary Key)
  - Name
  - Location
  - Type
  - Price

- *Booking*
  - BookingID (Primary Key)
  - BookingDate
  - StartDate
  - EndDate
  - TotalCost
  - UserID (Foreign Key)
  - PropertyID (Foreign Key)

- *Message*
  - MessageID (Primary Key)
  - SentDate
  - Content
  - UserID (Foreign Key)
  - PropertyID (Foreign Key)

- *Review*
  - ReviewID (Primary Key)
  - Rating
  - Comment
  - UserID (Foreign Key)
  - PropertyID (Foreign Key)

- *Payment*
  - PaymentID (Primary Key)
  - PaymentDate
  - Amount
  - BookingID (Foreign Key)

### Relationships
1. *User* to *Booking*: A User can make multiple Bookings, but each Booking is associated with one User.
2. *Property* to *Booking*: A Property can have multiple Bookings, but each Booking is associated with one Property.
3. *User* to *Message*: A User can send multiple Messages related to different Properties.
4. *Property* to *Message*: Messages are associated with specific Properties.
5. *User* to *Review*: A User can leave multiple Reviews for different Properties.
6. *Property* to *Review*: A Property can have multiple Reviews left by different Users.
7. *Booking* to *Payment*: Each Booking can have one Payment associated with it.

## How to Create the ERD
### Tools Required
- [Draw.io (diagrams.net)](https://app.diagrams.net/) or similar diagramming tools.
- [PlantUML](https://plantuml.com/) for rendering .uml files into visual diagrams.

### Steps
1. *Using PlantUML*:
   - Write the .uml file with all entities, attributes, and relationships.
   - Render the .uml file using PlantUML or any online PlantUML editor (e.g., [PlantText](https://planttext.com)).
   - Export the generated diagram as an image (PNG/SVG).

2. *Using Draw.io*:
   - Open Draw.io and create a new diagram.
   - Add entities as rectangles with attributes listed inside.
   - Use diamonds for relationships and connect entities with lines.
   - Use *crow’s foot notation* for cardinality.

## File Contents
1. ERD.uml: Contains the PlantUML script for generating the ERD.
2. README.md: This file, documenting the project and instructions.

## Example .uml File
```plaintext
@startuml
entity User {
  + UserID : Integer [PK]
  + Name : String
  + Email : String
  + Phone : String
  + Address : String
}

entity Property {
  + PropertyID : Integer [PK]
  + Name : String
  + Location : String
  + Type : String
  + Price : Float
}

entity Booking {
  + BookingID : Integer [PK]
  + BookingDate : Date
  + StartDate : Date
  + EndDate : Date
  + TotalCost : Float
  + UserID : Integer [FK]
  + PropertyID : Integer [FK]
}

entity Message {
  + MessageID : Integer [PK]
  + SentDate : DateTime
  + Content : String
  + UserID : Integer [FK]
  + PropertyID : Integer [FK]
}

entity Review {
  + ReviewID : Integer [PK]
  + Rating : Integer
  + Comment : String
  + UserID : Integer [FK]
  + PropertyID : Integer [FK]
}

entity Payment {
  + PaymentID : Integer [PK]
  + PaymentDate : Date
  + Amount : Float
  + BookingID : Integer [FK]
}

User "1" -- "0..*" Booking : makes
Property "1" -- "0..*" Booking : associated with
User "1" -- "0..*" Message : sends
Property "1" -- "0..*" Message : related to
User "1" -- "0..*" Review : writes
Property "1" -- "0..*" Review : reviewed by
Booking "1" -- "1" Payment : paid with
@enduml
```
## Credits

This ERD is designed as part of a database design task, showcasing relationships between entities and attributes.

