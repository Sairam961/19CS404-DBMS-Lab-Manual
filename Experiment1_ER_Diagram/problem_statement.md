# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="1148" height="954" alt="image" src="https://github.com/user-attachments/assets/8f93afaf-488e-4762-a8a1-8c57d63fe498" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
| :--- | :--- | :--- |
| **Program** | Program_ID (PK), Program_name, Description | Fitness courses offered by the club |
| **Trainer** | Trainer_ID (PK), Specialization, Name | Instructors assigned to fitness programs |
| **Member** | Member_ID (PK), Name, Start_date, Membership_type | Registered gym members |
| **Session** | Session_ID (PK), Trainer_ID (FK), Member_ID (FK), Date, Time | Personal training sessions |
| **Attendance** | Attendance_ID (PK), Session_ID (FK), Date | Attendance records for personal sessions |
| **Payment** | Payment_ID (PK), Member_ID (FK), Date, Amount | Payments made for memberships and sessions |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
| :--- | :--- | :--- | :--- |
| **Assigned** | N:M | Program: Partial, Trainer: Partial | Trainers are assigned to handle specific fitness programs |
| **Joins** | M:N | Member: Partial, Program: Partial | Members can register for and join multiple fitness programs |
| **Conducts** | 1:N | Trainer: Partial, Session: Total | A trainer conducts multiple personal training sessions |
| **Books** | 1:N | Member: Partial, Session: Total | A member can book multiple personal training sessions |
| **records** | 1:N | Session: Partial, Attendance: Total | Each session records attendance instances |
| **makes** | 1:N | Member: Partial, Payment: Total | A member makes payments for memberships or booked sessions |

### Assumptions

* Personal training sessions are booked individually between one member and one trainer.
* Attendance is tracked per booked session to verify attendance history.
* A member can make multiple payments covering different membership terms or session packages over time.

---

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
*Paste or attach your diagram here*  
<img width="1578" height="1058" alt="image" src="https://github.com/user-attachments/assets/ea711b3d-c86c-4d0d-b390-4de26ee3ec53" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
| :--- | :--- | :--- |
| **Room** | Room_ID (PK), Capacity, Room_no | Represents room spaces available for study or events |
| **Booking** | Booking_ID (PK), Room_ID (FK), Member_ID (FK), Date, Purpose | Tracks room reservations made by members |
| **Member** | Member_ID (PK), Name, Email, Phone | Registered library members |
| **Book** | Book_ID (PK), Title, Author, Category | Cataloged books in the library |
| **Loan** | Loan_ID (PK), Member_ID (FK), Book_ID (FK), due_date, return_data | Tracks borrowing history and due dates |
| **Fine** | Fine_ID (PK), Loan_ID (FK), Amount | Overdue charges associated with a specific loan |
| **Event** | Event_ID (PK), Room_ID (FK), Venue, Date | Cultural events organized by the library |
| **Speaker** | Speaker_ID (PK), Name, Bio | Guest speakers or authors featured at events |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
| :--- | :--- | :--- | :--- |
| **Reserved** | 1:N | Room: Partial, Booking: Total | A room can have multiple bookings; each booking belongs to one room |
| **Places** | 1:N | Member: Partial, Booking: Total | A member can place multiple room bookings |
| **Borrows** | 1:N | Member: Partial, Loan: Total | A member can have multiple loan transactions |
| **Book-Loan** | 1:N | Book: Partial, Loan: Total | A book can be borrowed multiple times across separate loans |
| **Incurs** | 1:1 | Loan: Partial, Fine: Total | A loan incurs at most one fine when overdue |
| **Registers** | M:N | Member: Partial, Event: Partial | Members can register for multiple events; events have multiple members |
| **Hosts** | N:1 | Event: Total, Room: Partial | Many events can be hosted in a room over time |
| **Features** | M:N | Event: Partial, Speaker: Partial | Events can feature multiple speakers; speakers can present at multiple events |

### Assumptions
* A Fine is only generated when a borrowed book is returned past its due_date.
* Each physical copy of a book has a unique Book_ID to track individual loans.
* Rooms can be reserved directly by members for private study or assigned by library administration to host events.
* An Event can feature multiple speakers, and each speaker can be associated with multiple events.
---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="1130" height="1134" alt="image" src="https://github.com/user-attachments/assets/b7b68c7a-c479-4d95-aa66-8e45069a60b5" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
| :--- | :--- | :--- |
| **Customer** | Customer_ID (PK), Name, Phone | Stores restaurant customer details |
| **Reservation** | Reservation_ID (PK), Customer_ID (FK), Table_ID (FK), Waiter_ID (FK), Date, Time, num_guests | Details of table reservations |
| **Table** | Table_ID (PK), Capacity | Physical dining tables in the restaurant |
| **Waiter** | Waiter_ID (PK), Name, Phone | Restaurant service staff |
| **Bill** | Bill_ID (PK), Reservation_ID (FK), Total, Service_charge | Invoice generated for a reservation |
| **Order** | Order_ID (PK), Reservation_ID (FK), order_time | Food orders placed under a reservation |
| **Dish** | Dish_ID (PK), Category_ID (FK), Name, Price | Menu items available for ordering |
| **Category** | Category_ID (PK), Category_name | Classifies dishes (e.g., Starter, Main, Dessert) |
| **Order_item** | Order_ID (PK, FK), Dish_ID (PK, FK), Subtotal, Quantity | Line item details linking ordered dishes to orders |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
| :--- | :--- | :--- | :--- |
| **places** | 1:N | Customer: Partial, Reservation: Total | A customer places one or more table reservations |
| **assigns** | 1:N | Table: Partial, Reservation: Total | Each reservation is assigned a specific table |
| **served_by** | 1:N | Waiter: Partial, Reservation: Total | Each reservation is attended to by a waiter |
| **generates** | 1:1 | Reservation: Total, Bill: Total | A reservation generates exactly one final bill |
| **contains** | 1:N | Reservation: Partial, Order: Total | A reservation can contain multiple food orders |
| **Includes** | M:N | Order: Total, Dish: Total | Orders include multiple dishes (resolved via Order_item) |
| **classifies** | 1:N | Category: Total, Dish: Total | Each dish belongs to a specific menu category |

### Assumptions

* Walk-in customers are registered as regular customers and assigned an immediate reservation record.
* Bills are calculated based on the total sum of all order items linked to the reservation plus the service charge.
* A single reservation can place multiple food orders during their dining session.
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
