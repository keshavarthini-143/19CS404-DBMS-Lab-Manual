# EX-01: ER Diagram Workshop – Submission Template

```
NAME: KESHAVARTHINI B
REG.NO: 212224040158
```

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
<img width="859" height="694" alt="image" src="https://github.com/user-attachments/assets/b2263c82-f147-4b07-abd7-1fd7dafe054d" />



### Entities and Attributes

## 1. MEMBER 
o MEMBER_ID (PK) 
o NAME 
o MEMBERSHIP_TYPE 
o START_DATE 

## 2. TRAINER 
o TRAINER_ID (PK) 
o NAME 
o SPECIALIZATION 
o PHONE 

## 3. PROGRAM 
o PROGRAM_ID (PK) 
o PROGRAM_NAME 
o DURATION 

## 4. SESSION 
o SESSION_ID (PK) 
o DATE 
o TIME 
o ATTENDANCE_STATUS (implied, not explicitly shown as attribute in this 
simplified view, but part of context) 

## 5. PAYMENT 
o PAYMENT_ID (PK) 
o AMOUNT 
o PAYMENT_DATE 
o PAYMENT_TYPE (Membership / Session)

### Relationships and Constraints

registers_for (M:N): Requires MEMBER_ID (FK to MEMBER) and PROGRAM_ID (FK to PROGRAM).

assigned_to (M:N): Requires TRAINER_ID (FK to TRAINER) and PROGRAM_ID (FK to PROGRAM).

PAYMENT (1:N): Requires MEMBER_ID (FK to MEMBER).

SESSION (1:N): This table is central and requires three Foreign Keys:

MEMBER_ID (FK to MEMBER)

TRAINER_ID (FK to TRAINER)

PROGRAM_ID (FK to PROGRAM)

### Assumptions

- 1-to-1 Sessions: Sessions are private (one member per session).

- No Co-Teaching: A session has only one trainer.

- Exclusive Links: A session belongs to exactly one program. A payment comes from exactly one member.

- Mandatory Links: A SESSION record cannot exist without a valid MEMBER, TRAINER, and PROGRAM (these FKs are likely NOT NULL).

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
<img width="865" height="928" alt="image" src="https://github.com/user-attachments/assets/41e249eb-a280-4f06-ac62-c743f80aff73" />



### Entities and Attributes

## 1. MEMBER 
o MEMBER_ID (PK) 
o NAME 
o ADDRESS 
o PHONE_NUMBER 

## 2. BOOK 
o BOOK_ID (PK) 
o TITLE 
o AUTHOR 
o CATEGORY 
o ISBN 
o PUBLICATION_YEAR 

## 3. AUTHOR (can be separate if more details are needed, or combined with Speaker) 
o AUTHOR_ID (PK) 
o NAME 
o BIO 

## 4. EVENT 
o EVENT_ID (PK) 
o EVENT_NAME 
o DATE 
o TIME 
o DESCRIPTION 

## 5. SPEAKER (can be SPEAKER/AUTHOR if they are the same entity) 
o SPEAKER_ID (PK) 
o NAME 
o BIO 

## 6. ROOM 
o ROOM_ID (PK) 
o ROOM_NUMBER 
o CAPACITY 

## 7. BORROWING (associative entity for book loans) 
o BORROWING_ID (PK) 
o LOAN_DATE 
o RETURN_DATE 
o DUE_DATE 
o FINE_AMOUNT (derived attribute

### Relationships and Constraints

BORROWS (M:N): Requires MEMBER_ID (FK to MEMBER) and BOOK_ID (FK to BOOK).

REGISTERS FOR (M:N): Requires MEMBER_ID (FK to MEMBER) and EVENT_ID (FK to EVENT).

SPEAKS_AT (M:N): Requires EVENT_ID (FK to EVENT) and SPEAKER_ID (FK to SPEAKER).

EVENT (1:N): Requires ROOM_ID (FK to ROOM).

BOOK (1:N): Requires AUTHOR_ID (FK to AUTHOR).

### Assumptions

- Single Author: A book has only one author.

- Book Titles: BOOK entity represents a title, not a physical copy.

- Mandatory Location: An EVENT must be assigned to one ROOM.

- M:N Speakers: Events can have multiple speakers, and speakers can attend multiple events.
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
<img width="865" height="500" alt="image" src="https://github.com/user-attachments/assets/09892d12-d688-45f9-bda8-069139a01fa6" />



### Entities and Attributes

## 1. CUSTOMER 
o CUSTOMER_ID (PK) 
o NAME 
o PHONE_NO 
o EMAIL 

## 2. TABLE 
o TABLE_NO (PK) 
o CAPACITY 
o LOCATION (e.g., window, corner) 
o STATUS (e.g., available, occupied) 

## 3. RESERVATION 
o RESERVATION_ID (PK) 
o RESERVATION_DATE 
o RESERVATION_TIME 
o NUM_GUESTS 
o STATUS (e.g., confirmed, seated, cancelled) 

## 4. ORDER 
o ORDER_ID (PK) 
o ORDER_DATE 
o ORDER_TIME 
o TOTAL_AMOUNT 
o STATUS (e.g., pending, cooking, served, paid) 

## 5. DISH 
o DISH_ID (PK) 
o DISH_NAME 
o DESCRIPTION 
o PRICE 
o CATEGORY (Starter, Main, Dessert, Drink) 

## 6. WAITER 
o WAITER_ID (PK) 
o NAME 
o SHIFT 

## 7. BILL 
o BILL_ID (PK) 
o BILL_DATE 
o TOTAL_AMOUNT 
o SERVICE_CHARGE 
o TAX_AMOUNT 
o PAYMENT_STATUS

### Relationships and Constraints

RESERVATION (1:N): This table is central and requires three Foreign Keys:

CUSTOMER_ID (FK to CUSTOMER)

TABLE_ID (FK to TABLE)

WAITER_ID (FK to WAITER)

ORDER (1:N): Requires RESERVATION_ID (FK to RESERVATION).

BILL (1:1): Requires RESERVATION_ID (FK to RESERVATION, which must also be a UNIQUE key).

ORDER_ITEM (M:N): Requires ORDER_ID (FK to ORDER) and DISH_ID (FK to DISH).

### Assumptions

- One Table per Reservation: A single reservation cannot reserve multiple tables.

- One Waiter per Reservation: A reservation is the responsibility of a single waiter.

- No Split Bills: A reservation generates exactly one bill.

- Mandatory Links: A RESERVATION record cannot exist without a CUSTOMER, TABLE, and WAITER.

- Time Conflicts: The schema itself does not prevent booking the same TABLE at the same time. This logic must be enforced by the application.
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
