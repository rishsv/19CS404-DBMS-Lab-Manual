# ER Diagram Workshop – Submission Template

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="987" height="755" alt="image" src="https://github.com/user-attachments/assets/3e42c3a7-992e-4fab-891a-2eb52751bcab" />


### Entities and Attributes
| Entity  | Attributes (PK, FK)                                                        | Notes                                |
| ------- | -------------------------------------------------------------------------- | ------------------------------------ |
| MEMBER  | **MemberID (PK)**, Name, Email, Phone                                      | Stores member details                |
| BOOK    | **BookID (PK)**, Title, Author, Category, Availability                     | Stores book information              |
| LOAN    | **LoanID (PK)**, LoanDate, DueDate, ReturnDate, MemberID (FK), BookID (FK) | Records borrowed books               |
| FINE    | **FineID (PK)**, Amount, PaidStatus, LoanID (FK)                           | Stores fine details for late returns |
| EVENT   | **EventID (PK)**, EventName, EventDate, Capacity                           | Stores library event details         |
| ROOM    | **RoomID (PK)**, RoomName, Capacity                                        | Stores room information for events   |
| SPEAKER | **SpeakerID (PK)**, Name, Expertise                                        | Stores speaker details               |


### Relationships and Constraints
| Relationship                       | Cardinality                                    | Participation   | Notes                                                                   |
| ---------------------------------- | ---------------------------------------------- | --------------- | ----------------------------------------------------------------------- |
| Borrows (MEMBER–BOOK through LOAN) | One Member → Many Loans, One Book → Many Loans | Partial         | A member can borrow many books; each loan links one member and one book |
| Incurs (LOAN–FINE)                 | One Loan → Zero or One Fine                    | Partial         | Fine is incurred only for overdue loans                                 |
| Registers (MEMBER–EVENT)           | Many Members ↔ Many Events                     | Partial         | Members can register for multiple events                                |
| Hosts (EVENT–ROOM)                 | Many Events → One Room                         | Total for Event | Each event is hosted in a room                                          |
| Speaks at (SPEAKER–EVENT)          | Many Speakers ↔ Many Events                    | Partial         | A speaker may speak at many events                                      |
| Features (EVENT–SPEAKER)           | Many-to-Many                                   | Partial         | Events may feature multiple speakers                                    |


### Assumptions
1.A member can borrow multiple books, but each loan record refers to one member and one book.

2.A fine is generated only if a loan exceeds the due date.

3.Members may register for multiple events, and events can have many members.

4.Each event is hosted in one room, but a room may host multiple events at different times.

5.A speaker can participate in multiple events, and an event may include multiple speakers.
