# Database Normalization to 3NF

## Objective
The goal of this task is to review the provided database schema, identify redundancies or violations of normalization principles, and adjust the design to achieve *Third Normal Form (3NF)*.

## Initial Schema
The initial schema includes the following entities:

1. *User*
   - UserID (Primary Key)
   - Name
   - Email
   - Phone
   - Address

2. *Property*
   - PropertyID (Primary Key)
   - Name
   - Location
   - Type
   - Price

3. *Booking*
   - BookingID (Primary Key)
   - BookingDate
   - StartDate
   - EndDate
   - TotalCost
   - UserID (Foreign Key)
   - PropertyID (Foreign Key)

4. *Message*
   - MessageID (Primary Key)
   - SentDate
   - Content
   - UserID (Foreign Key)
   - PropertyID (Foreign Key)

5. *Review*
   - ReviewID (Primary Key)
   - Rating
   - Comment
   - UserID (Foreign Key)
   - PropertyID (Foreign Key)

6. *Payment*
   - PaymentID (Primary Key)
   - PaymentDate
   - Amount
   - BookingID (Foreign Key)

---

## Normalization Steps

### First Normal Form (1NF)
1. Ensure that all attributes contain atomic values:
   - No multivalued or composite attributes exist in the schema.

### Second Normal Form (2NF)
2. Ensure all non-key attributes are fully functionally dependent on the primary key:
   - No partial dependency exists (since all composite keys have been replaced by single primary keys).
   - Example: Attributes in the Payment table depend solely on BookingID.

### Third Normal Form (3NF)
3. Eliminate transitive dependencies:
   - Ensure that non-key attributes depend only on the primary key and not on other non-key attributes.

### Schema Adjustments
#### Identified Redundancy in Message and Review:
- *Problem*: Both Message and Review store references to UserID and PropertyID. However, these fields do not directly depend on the primary keys of their respective tables.
- *Solution*: Link Message and Review to the Booking table instead of duplicating the relationships with User and Property.

#### Revised Schema:
1. *User*
   - UserID (Primary Key)
   - Name
   - Email
   - Phone
   - Address

2. *Property*
   - PropertyID (Primary Key)
   - Name
   - Location
   - Type
   - Price

3. *Booking*
   - BookingID (Primary Key)
   - BookingDate
   - StartDate
   - EndDate
   - TotalCost
   - UserID (Foreign Key)
   - PropertyID (Foreign Key)

4. *Message*
   - MessageID (Primary Key)
   - SentDate
   - Content
   - BookingID (Foreign Key)

5. *Review*
   - ReviewID (Primary Key)
   - Rating
   - Comment
   - BookingID (Foreign Key)

6. *Payment*
   - PaymentID (Primary Key)
   - PaymentDate
   - Amount
   - BookingID (Foreign Key)

---

## Explanation of Changes
### Removed Redundancy:
1. The Message and Review tables previously had duplicate relationships with both User and Property. By linking them to the Booking table:
   - UserID and PropertyID references are resolved through the Booking table.
   - This eliminates redundant foreign keys while maintaining all necessary relationships.

### Ensured 3NF:
2. All attributes in every table now depend *only* on their respective primary keys.
   - Example: In the Message table, Content and SentDate depend only on MessageID.

---

## Benefits of 3NF
1. Reduces redundancy and saves storage space.
2. Simplifies data integrity and minimizes the risk of anomalies during data operations.
3. Improves query performance by streamlining relationships and reducing the need for joins.