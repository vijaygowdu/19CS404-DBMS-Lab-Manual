# ER Diagram Workshop – Submission Template
## Name : K Vijay
## Reg No : 212223040236

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.


# Scenario A: City Fitness Club Management

## Business Context: 

FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

## Requirements:
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:


<img width="1634" height="1253" alt="image" src="https://github.com/user-attachments/assets/b6774c52-8844-42fa-89c7-40bca0101534" />


### Entities and Attributes


| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Admin     |           User_Name (PK), Password	         |    Admin manages the website.|
|  Gym Member	      |           Member_ID (PK), First_Name, Last_Name, User_Name, Password, Email_ID, Phone_Number, Age, Address (Street, City)	         |  A person who uses the system for gym-related activities.|
|   Instructor	     |              Instructor_ID (PK), First_Name, Last_Name, User_Name, Password, Email_ID, Phone_Number, Age, Address (Street, City)	      |    Manages exercises, diet plans, and classes. |
| Exercise	       |        Exercise_ID (PK), Exercise_Types	            |    Different types of workouts/exercises.   |
|     Diet Plan	   |              DietPlan_ID (PK), Diet_Types	      |    Diet plans categorized by types.   |
|   Classes	     |                Class_ID (PK), Cost, Date, Timing	    |     Gym classes that members can take.  |
|     Gym Buddy Website	   |             (No explicit attributes shown)	       |    Acts as a platform entity between users (admin, member, instructor).   |


### Relationships and Constraints


| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Admin – Manage – Gym Buddy Website	      |     1 : 1	       |         Total (Admin must manage)	      |    Admin controls the website.   |
|  Gym Member – Used – Gym Buddy Website	            |        M : 1	    |     Partial (members use site)	          |    Members interact with website.   |
|       Instructor – Manage – Gym Buddy Website	       |      M : 1	      |          Partial	     |  Instructors also interact via website.     |
|         Gym Member – View – Exercise	     |     M : M	       |          Partial	     |     Members can view many exercises, and exercises can be viewed by many members.  |
|          Instructor – Manage – Exercise	    |    1 : M	        |     Total on Exercise	          |   Instructors create/manage exercises.    |
|     Gym Member – View – Diet Plan	         |  M : M	          |      Partial         |   Members can view many diet plans.    |
|      Instructor – Manage – Diet Plan	        |       1 : M	     |     Total on Diet Plan	          |    Instructors manage diet plans.   |
|        Gym Member – Take Classes – Classes	      |       M : 1	     |           Partial	    |    A member can take many classes, each class can have many members.   |
|         Instructor – Assign – Classes	     |       M : 1	     |        Total on Instructor	       |    Instructors are assigned to classes.   |


### Assumptions


- Each Gym Member and Instructor has unique login credentials (User Name, Password).

- A Diet Plan is always created/managed by an Instructor (not directly by a member).

- Classes are scheduled by instructors and attended by members; each class must have at least one instructor assigned.

- Exercises can exist independently, but usually managed by instructors.

## The Gym Buddy Website is more of a conceptual entity representing the system, not a data table.


# Scenario B: City Library Event & Book Lending System

## Business Context:  
The Central Library wants to manage book lending and cultural events.

## Requirements:  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:

<img width="1182" height="915" alt="image" src="https://github.com/user-attachments/assets/408d3556-1971-4dff-ba06-5628921a9904" />

### Entities and Attributes


| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|  Books	      |           Book_ID (PK), Title, Author, Price, Available	         |   Represents library books.|
|   Publisher	     |             Pub_ID (PK), Name, Address	       |     Publishers of books.  |
|    Member	    |         Member_ID (PK), Name, Address, Member_Type, Member_Date, Expiry_Date	           |  Library members who borrow books.     |
|    Borrowed_By (Associative Entity)	    |        Book_ID (FK), Member_ID (FK), Issue, Due_Date, Return_Date	            | Relationship entity to track which member borrowed which boo      |


### Relationships and Constraints


| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Published_By (Books–Publisher)	             |    M : 1	        |      Total on Books, Partial on Publisher	         | Each book must be published by exactly one publisher, a publisher can publish many books.      |
|    Borrowed_By (Books–Member)	          |       M : M	     |      Partial on both sides	         |A member can borrow many books, and a book can be borrowed by many members over time (history tracked).       |


### Assumptions

- Each book has exactly one publisher.

- A member can borrow multiple books at a time.

- The Borrowed_By entity is used to store transaction details (issue date, due date, return date).

- A book’s Available attribute indicates whether it can be borrowed.


# Scenario C: Restaurant Table Reservation & Ordering

## Business Context: 
A popular restaurant wants to manage reservations, orders, and billing.

## Requirements:  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:

<img width="2581" height="1575" alt="image" src="https://github.com/user-attachments/assets/bc021b2e-6b67-484a-9b1b-2368b179d283" />


### Entities and Attributes


| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Admin	       |    admin_id (PK), admin_Fname, admin_Mname, admin_Lname, admin_pass	                |    Manages and checks rooms.   |
| Receptionist	       |rec_id (PK), rec_Fname, rec_Mname, (other attributes)	                    |Confirms customer reservations and checks rooms.       |
|Customer	        |cust_id (PK), cust_Fname, cust_Mname, cust_Lname, cust_address, cust_number	                    | Makes reservations and creates transactions.      |
|   Room	     |   room_id (PK), (attributes like availability, capacity)	                 |Represents physical hotel rooms, linked to room types.       |
| Room_type	       |room_code (PK), room_name	                    |Defines category/type of room (e.g., Deluxe, Standard).       |
|Transaction	        |trans_id (PK), cust_id (FK), rec_id (FK), start_date, end_date, total_payment, payment_type (FK)	                    |Records booking/payment details for customers.   |
|Payment_type	        |payment_type_id (PK), payment_name	                    |Stores different payment methods (cash, card, online).       |


### Relationships and Constraints



| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Admin – Checks – Room	             | 1 : N	           |Total on Admin, Partial on Room	               |Admin checks multiple rooms. |
|  Receptionist – Checks – Room	            |  1 : N	          |Total on Receptionist, Partial on Room	               | Receptionist verifies/checks room availability.      |
|      Receptionist – Confirms – Customer	        |1 : N	            |Total on Receptionist, Partial on Customer	               | Receptionist confirms bookings for customers.      |
| Customer – Creates – Transaction	             | 1 : N	           | Total on Customer, Partial on Transaction	              | A customer can create multiple transactions.      |
|Room – has – Room_type	              |  N : 1	          | Total on Room, Partial on Room_type	              |Each room must belong to a room type.       |
| Transaction – has – Payment_type	             |  N : 1	          | Total on Transaction, Partial on Payment_type	              |  Every transaction requires a payment type.     |

### Assumptions
- Each Admin and Receptionist can check multiple rooms, but each room is checked by only one staff member at a time.

- A Customer must exist before making a Transaction.

- Transaction includes booking dates (start_date, end_date) and payment info.

- Room_type determines room classification; attributes like price and capacity can be included here.

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
