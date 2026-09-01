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
![ER Diagram](er_diagram_fitness.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

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
![ER Diagram](er_diagram_library.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
| :--- | :--- | :--- |
| **Room** | **`Room_ID` (PK)**, `Capacity`, `Room_no` | Represents room spaces available for study or events |
| **Booking** | **`Booking_ID` (PK)**, **`Room_ID` (FK)**, **`Member_ID` (FK)**, `Date`, `Purpose` | Tracks room reservations made by members |
| **Member** | **`Member_ID` (PK)**, `Name`, `Email`, `Phone` | Registered library members |
| **Book** | **`Book_ID` (PK)**, `Title`, `Author`, `Category` | Cataloged books in the library |
| **Loan** | **`Loan_ID` (PK)**, **`Member_ID` (FK)**, **`Book_ID` (FK)**, `due_date`, `return_data` | Tracks borrowing history and due dates |
| **Fine** | **`Fine_ID` (PK)**, **`Loan_ID` (FK)**, `Amount` | Overdue charges associated with a specific loan |
| **Event** | **`Event_ID` (PK)**, **`Room_ID` (FK)**, `Venue`, `Date` | Cultural events organized by the library |
| **Speaker** | **`Speaker_ID` (PK)**, `Name`, `Bio` | Guest speakers or authors featured at events |

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
- 
- 
- 

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
![ER Diagram](er_diagram_restaurant.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
