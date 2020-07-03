# Databse Design - The Living Hood App
### Author: Haoyang (Eric) Chen

## 1: Defining the purpose of the databse:
Residential Services Tracking and Management

## 2: Listing down major functional requirements: 
- The application can be used by current tenants, administrators, and service providers
- Users should be able to sign up with email address and selected property
- Users should be able to reset password with their email account
- Administrators/IT can update and delete information
- Tenants should be able to view the account balance and detailed statement of each month
- Tenants should be able to report maintainence to the system with the information of Category, Description, Photos, Time Duration Preference, and Property Access Information. 
- Tenants are able to view announcement for the community and events
- Different service providers in charge of different category or categories
- Service providers are able to change the work order status and fill out the feedback form; the form should include completion time, maintainance work detail, and the cost of additional tools.
- Cleaning service staff should be able to mark complete for the specific cleaning area: elevator, common area, study room, rooftop lounge, club lounge, public bathroom, and units that the tenant just moved out. 

## 3: Listing down entities to identify tables: 
- Property
- Room
- Tenant
- Service_Provider
- Lease
- Account_Information
- Bill
- Work_Order
- Category
- Feedback
- Announcement
- Event
- Cleaning_Service
- Community


Entities need to be considered:
- Administrator (Do we need this?)
- User (Do we need this?)
- RolE (Do we need this?)
- User_to_Role (Do we need this?)
- Role_to_Permission  (Do we need this?)
- Permission (Do we need this?)
- Calendar (Do we need this?)
- Credit_Card_Information (Do we need this?)

## 4: Deciding Relationships between tables
-  1 account information is associated with only 1 tenant
-  1 tenant has only one account information
-  1 tenant pays 1 or more bills
-  1 bill is paid by 1 or more tenant
-  1 tenant has 1 or more lease
-  1 lease is completed by 1 or more tenants
-  1 tenant lives in only 1 property
-  1 property has 1 or many tenants
-  1 property has many rooms
-  1 room is associated with only 1 property
-  1 tenant can order 1 or many work orders
-  1 work order is placed by only 1 tenant
-  1 work order has only 1 category
-  1 category has many work orders
-  1 service provider is in charge of 1 or more categories
-  1 category has 1 or more service providers
-  1 service provider can give 1 or more feedbacks
-  1 feedback is given by only 1 service provider
-  1 apartment is associated with only 1 community
-  1 community has 1 or many apartments
-  1 community can give one or many annoucements
-  1 announcement is associated with 1 community
-  1 community can host 1 or many events
-  1 event is associated with 1 or many communities

## 5: Deciding the columns, keys, and constraints

### Property: 
| Column | Type | Constraint | key|
|---|---|---|---|
| Property_id | INT | UNIQUE | PK|
| Property_name | VARCHAR | NOT NULL ||
| Property_address | VARCHAR | NOT NULL ||
| Property_description | VARCHAR | NOT NULL ||
| Community_id | INT | NOT NULL | FK |

--------------------
### Room: 
| Column | Type | Constraint | key|
|---|---|---|---|
| Room_id | INT | UNIQUE | PK|
| Room_number | INT | NOT NULL ||
| Vacancy | BOOLEAN | NOT NULL ||
| Resident_Number | INT | NOT NULL ||

------------------------

### Community: 
| Column | Type | Constraint | key|
|---|---|---|---|
| Community_id | INT | UNIQUE | PK|
| Community_name | VARCHAR | NOT NULL||
| Community_description | VARCHAR | NOT NULL||
| Announcement_id | INT | NOT NULL | FK |
| Event_id | INT | NOT NULL | FK |

------------------------------

### Announcement: 
| Column | Type | Constraint | key|
|---|---|---|---|
| Announcement_id | INT | UNIQUE | PK|
| Announcement_name | VARCHAR | NOT NULL ||
| Announcement_description | VARCHAR | NOT NULL ||
| Announcement_time | TIME | NOT NULL||

------------------------------

### Event: 
| Column | Type | Constraint | key|
|---|---|---|---|
| Event_id | INT | UNIQUE | PK|
| Event_name | VARCHAR | NOT NULL ||
| Event_description | VARCHAR | NOT NULL ||
| Event_time | TIME | NOT NULL||

-----------------------
### Tenant: 
| Column | Type | Constraint | key|
|---|---|---|---|
| Tenant_id| INT | UNIQUE | PK|
| First_name | VARCHAR |NOT NULL||
| Last_name | VARCHAR | NOT NULL||
| Identification | INT | NOT NULL ||
| Date_of_Birth | DATE  | NOT NULL ||
| Email | VARCHAR | NOT NULL ||
| Phone_Number | INT | NOT NULL ||
| Room_Id | INT | NOT NULL | FK |
| Property_Id | INT | NOT NULL |FK|
| Lease_id | INT | NOT NULL | FK |
| Account_id | INT | NOT NULL | FK |
| Bill_id | INT | NOT NULL | FK |

----------------------

### Lease: 
| Column | Type | Constraint | key|
|---|---|---|---|
| Lease_id| INT | UNIQUE | PK|
| Start_date | DATE | NOT NULL ||
| End_date | DATE | NOT NULL ||
| Move_in_Date | Date | NOT NULL||

------------------------

### Account_Information:
| Column | Type | Constraint | key|
|---|---|---|---|
|Accound_id | INT | UNIQUE | PK |
|Password | BINARY(16) | NOT NULL ||
|Date_created | DATE | NOT NULL||
|Photo| BLOB | NOT NULL||
|Email|VARCHAR|NOT NULL||

---------------------

### Bill:
| Column | Type | Constraint | key|
|---|---|---|---|
| Bill_id | INT | UNIQUE | PK |
| Bill_name| VARCHAR | VARCHAR ||
| Bill_date | DATE | NOT NULL||
| Bill_amount| FLOAT | NOT NULL ||
| Bill_description | VARCHAR | NOT NULL ||
| Account_Balance | FLOAT | NOT NULL ||
| Auto_payment | BOOLEAN | NOT NULL ||

----------------------

### Work_Order:
| Column | Type | Constraint | key|
|---|---|---|---| 
| WorkOrder_id | INT | UNIQUE | PK |
| Category_id | INT | NOT NULL | FK |
| WorkOrder_name | VARCHAR | NOT NULL ||
| WorkOrder_description | VARCHAR | NOT NULL ||
| Problem_photo | BLOB | NOT NULL ||
| START_TIME_PREFERENCE | DatetIME | NOT NULL||
| END_TIME_PREFERENCE | Datetime | NOT NULL||
| Access_Permission | BOOLEAN | NOT NULL||
| Work_Status | BOOLEAN | NOT NULL ||
| Feedback_id | INT | NOT NULL | FK |
| Service_Provider_id | INT | NOT NULL | FK |

-----------------------

### Category:
| Column | Type | Constraint | key|
|---|---|---|---| 
| Category_id | INT | UNIQUE | PK |
| Category_name | VARCHAR | NOT NULL | |
| Category_description | VARCHAR | NOT NULL | |

----------------------

### Feedback:
| Column | Type | Constraint | key|
|---|---|---|---| 
| Feedback_id | INT | UNIQUE | PK |
| Completion_time | Time | NOT NULL ||
| Maintainence_work_detail | VARCHAR | NOT NULL ||
| Cost_of_additional_tools | FLOAT | NOT NULL ||

-----------------------

### Service_Provider:
| Column | Type | Constraint | key|
|---|---|---|---| 
| Service_Provider_id | INT | UNIQUE | PK |
| Service_Provider_Last_name | VARCHAR | NOT NULL | PK |
| Service_Provider_First_name | VARCHAR | NOT NULL | PK |
| Category_id | INT | NOT NULL | FK |
| Date_of_Birth | DATE  | NOT NULL ||
| Email | VARCHAR | NOT NULL ||
| Phone_Number | INT | NOT NULL ||

----------------------
### Reference:
[Sample Role-Based Access Control System](https://mysql.tutorials24x7.com/blog/guide-to-design-database-for-rbac-in-mysql)