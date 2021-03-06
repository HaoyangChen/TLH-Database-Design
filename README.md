# Databse Design - The Living Hood App
### Author: Haoyang (Eric) Chen, Yutong Wei,Lizi Xian
### [Live Site](https://haoyangchen.github.io/TLH-Database-Design/)

## 1: Defining the purpose of the databse:
Residential Services Tracking and Management

## 2: Listing down major functional requirements: 
- The application can be used by current tenants, maintenances and cleaning staffs
- Users should be able to sign up with email address using a pin code send by adminstrators.
- Users should be able to reset password with their email account
- Administrators/IT can update and delete information
- The database will retain all the billing details within 12 months.
- Tenants should be able to report maintainence to the system with the information of Category, Description, Photos, Time Duration Preference, and Property Access Information. 
- Tenants are able to view announcement for the community and events
- Different service providers in charge of different category or categories
- Service providers are able to change the work order status and fill out the feedback form; the form should include completion time, maintainance work detail, and the cost of additional tools.
- Cleaning service staff should be able to mark complete for the specific cleaning area: elevator, common area, study room, rooftop lounge, club lounge, public bathroom, and units that the tenant just moved out. 

## 3: Listing down entities to identify tables: 
- Property
- Room
- Location
- Room_type
- Laundry_type
- Tenant
- Service_Provider
- Service_Provider_Category
- Lease
- Account_Information
- Bill
- Work_Order
- Category
- Feedback
- Announcement
- Event
- Community
- Department


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
-  1 bill is paid by 1 tenant
-  1 tenant has 1 or more lease
-  1 lease is completed by 1 or more tenants
-  1 tenant lives in only 1 property
-  1 property has 1 or many tenants
-  1 property has many rooms
-  1 room is associated with only 1 property
-  1 room has 1 room type
-  1 room has 1 laundry type
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

### Pin_code: 
| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| pin_code | INT | NOT NULL | PK| a 6 digits long code given by admin to allow tenants to register applcation accounts|
| last_name | VARCHAR(255) | NOT NULL | | tenants' last name |
| first_name | VARCHAR(255) | NOT NULL | | tenants' first name |
| property_id| VARCHAR(50) | NOT NULL | | tenants' current property id |
| identity | VARCHAR(50) | NULL | | tenants' identification number (e.g. ssn) |
| email | VARCHAR(254) |NULL| | tenants sign up and sign in by emails |
| phone_number | INT | NULL || tenants' phone number |
| lease_start_date | DATE | NULL || a start date of tenant's lease agreement |
| lease_end_date | DATE | NULL || an end date of tenant's lease agreement |
| lease_contract | VARCHAR(255) | NULL || tenants' lease agrrement sigend contract |
| unit| VARCHAR(50) | NULL | | tenants' current unit number |
| monthly_rent | DECIMAL(7,2) | NULL | | montly rent tenants need to pay for their current units |
| property_name| VARCHAR(100) | NULL | | tenants' current property name |

--------------------------------


### Tenant: 

| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| email | VARCHAR(254) |NOT NULL| PK | tenants sign up and sign in by emails |
| last_name | VARCHAR(255) | NOT NULL | | tenants' last name |
| first_name | VARCHAR(255) | NOT NULL | | tenants' first name |
| nick_name | VARCHAR(255) | NOT NULL | | tenants' nick name |
| account_password | VARCHAR(255) | NOT NULL || tenants' password for the application logging |
| identity | VARCHAR(50) | NULL | | tenants' identification number (e.g. ssn) |
| phone_number | VARCHAR(11) | NULL || tenants' phone number |
| date_created | DATE | NOT NULL| |registeration date of a application account|
| monthly_rent | DECIMAL(7,2) | NOT NULL | | a montly rent tenants need to pay for their current units |
| current_balance | DECIMAL(7,2) | NOT NULL | | the amounts of money that in user's application account |
| auto_payment| TINYINT(1)| NOT NULL | | a value of zero(false) means the account has no auto payment. a value of one(true) means the account has auto payment |
| card_number| INT(11)| NULL | | tenants' card number |
| cardholder_name| VARCHAR(255)| NULL | | tenants' carholder name |
| exp_date| DATE| NULL | | tenants' card expiration date |
| zipcode| INT(11)| NULL | | tenants' card zip code |
| lease_id| VARCHAR(255) | NULL | | tenants' lease id (all) |
| property_id| VARCHAR(50) | NOT NULL | | tenants' current property id |
| unit| VARCHAR(50) | NULL | | tenants' current unit number |
| notification_id| VARCHAR(255) | NULL | | id of notification messages |

--------------------------------


### Billing_detail: 
| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| id | VARCHAR(50) |NOT NULL| PK | billing id |
| description | VARCHAR(50) | NOT NULL | | billing's description |
| created_date | DATE | NOT NULL | |created date of the bill |
| amount | DECIMAL(7,2) | NOT NULL | | billing amount |
| email | VARCHAR(254)) | NOT NULL | | tenants' email |

--------------------------------


### Lease: 
| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| lease_id| VARCHAR(25) | NOT NULL | PK | lease id |
| lease_contract | VARCHAR(255) | NOT NULL ||tenants' lease agrrement sigend contract|
| lease_status | TINYINT(1) | NULL || a value of zero(false) means the lease is active. a value of one(true) means the lease is not active|
| lease_created_date| DATETIME | NULL|| the date admin register a new tenant into admin system|
| lease_start_date | DATE | NULL || the start date of the lease|
| lease_end_date | DATE | NULL || the end date of the lease|

------------------------------

### Notification: 
| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| notification_id | VARCHAR(25) | NOT NULL| PK| notification id |
| notification_title | VARCHAR(50) | NOT NULL || the title of a notification |
| notification_description | VARCHAR(255) | NOT NULL | | the description of a notification|
| notification_time | DATETIME | NOT NULL| | a specific time that a notification would be sent to tenants|
| expiration_time| DATETIME | NULL| | a specifica time that a notification would be expired |
| flag | TINYINT(1) | NULL| | a value of zero means the notification is unread. a value of one means the notification is read |

------------------------------

### Property: 

| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| property_id | VARCHAR(50) | NOT NULL | PK| propert id |
| property_name | VARCHAR(100) | NOT NULL || property name |
| state | VARCHAR(20)| NOT NULL || the state of the property |
| zipcode | INT(11) | NOT NULL || the zipcode of the property |
| street_name | VARCHAR(255) | NOT NULL || the street name of the property |
| city | VARCHAR(45) | NOT NULL || the city of the property |
| total_units | INT(11) | NULL || total number of units in the property |

------------------------
### Unit: 
| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| unit_number | VARCHAR(50) | NOT NULL |PK| unit number |
| unit_type | VARCHAR(50)| NOT NULL | | the function of units |
| predefined_rent| DECIMAL(7,2)| NOT NULL ||predefined rent for a sepecific unit |
| unit_description|VARCHAR(255)| NULL ||the description of a specific unit |
| lease_id|VARCHAR(25)| NULL ||lease id |
| property_id | VARCHAR(50) | NOT NULL || propert id |
| property_name | VARCHAR(100) | NULL || property name |

--------------------------------


### Event: 
| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| event_id | VARCHAR(50) |  NOT NULL | PK| event id |
| event_name | VARCHAR(50) | NOT NULL || event name |
| event_photo | VARCHAR(255) | NULL || event photo |
| event_start_time | DATETIME | NOT NULL || the start time of the event |
| event_end_time | DATETIME | NOT NULL || the end time of the event |
| event_description | VARCHAR(500) | NOT NULL || the description of an event |
| event_location | VARCHAR(255) | NOT NULL|| a place where an event will be happening |
| property_id | VARCHAR(50) | NOT NULL |PK| propert id |
| event_status | TINYINT(1) | NOT NULL||  a value of zero(false) means the event is ongoing. a value of one(true) means the event is expired |
| participants_counts | INT(11) | NOT NULL | | the number of tenants attending to the event |

-----------------------

### Maintenance:
| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| maintenance_email | VARCHAR(254) | NOT NULL| PK | maintenances sign up and sign in by emails| 
| identity | VARCHAR(50) | NULL | | maintenances' identification number (e.g. ssn) |
| last_name | VARCHAR(255) | NOT NULL | | maintenances' last name |
| first_name | VARCHAR(255) | NOT NULL | | maintenances' first name |
| preferred_name| VARCHAR(255) | NOT NULL | | maintenances' preferred name |
| password | VARCHAR(255) | NOT NULL || maintenances' password for the application logging |
| phone_number | VARCHAR(11) | NULL ||  maintenances' phone number |
| availability_setup | MEDIUMTEXT | NULL | | maintenances' weekly availability setup |
| total_available_time | VARCHAR(25)| NULL | | maintenances' total available time |
| minimum_hour| VARCHAR(25) | NULL| | maintenances'minimum weekly working hours |
| property_id | VARCHAR(50) | NULL || propert id |
| category_name| VARCHAR(255) | NULL || service types (there are 9 types maintenance services in total) |


-----------------------
### Work_Order:
| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| WorkOrder_id | VARCHAR(50) | NOT NULL  | PK | work order id |
| work_order_description | VARCHAR(255) | NOT NULL | | the description provided by tenants about the maintenance issues |
| problem_photo | VARCHAR(255) | NULL || photos of the maintenance issues (up to 3) |
| time_preference | VARCHAR(500) |  NULL || three different availiable time slot provided by tenants |
| permission_to_enter| TINYINT(1) | NOT NULL || a value of zero(false) means the permissions was not given. a value of one(true) means the permissions was given|
| work_status | VARCHAR(25)| NOT NULL || 5 types of work status:unassigned, scheduled, in_progress, paused, completed |
| date_created | DATETIME | NOT NULL || created date of a work order on application |
| scheduled_date | DATE| NULL|| a date scheduled by admin to let maintenances to process a work order |
| scheduled_time | VARCHAR(50) | NULL|| a timeslot scheduled by admin to let maintenances to process a work order 
| category_name| VARCHAR(255) | NOT NULL || service types (there are 9 types maintenance services in total) |
| email | VARCHAR(254) |NOT NULL| PK | tenants sign up and sign in by emails |
| maintenance_email | VARCHAR(254) | NULL| | maintenances sign up and sign in by emails| 
| property_name | VARCHAR(100) | NOT NULL || property name |
| unit| VARCHAR(50) | NOT NULL | | tenants' current unit number |
| tenant_last_name | VARCHAR(255) | NULL | | tenants' last name |
| tenant_first_name | VARCHAR(255) | NULL | | tenants' first name |
| tenant_phone_number | VARCHAR(11) | NULL | | tenants' phone number |

-----------------------

### Feedback:
| Column | Type | Constraint | key| Description|
|---|---|---|---|---|
| work_order_id| VARCHAR(50) | NOT NULL | PK | work order id |
| report_cost| DECIMAL(7,2) | NOT NULL || the cost of the items for tenants'work order |
| attach_photos | VARCHAR(255)| NULL || receipts photos |
| notes | VARCHAR(500) | NULL || information provided by tenants which wants admin to know |
| item_description | VARCHAR(500) | NULL || the descriptions of the items for tenants'work order|

-----------------------


### Location: 
| Column | Type | Constraint | key|
|---|---|---|---|
| location_id | INT | UNIQUE | PK|
| location_name | VARCHAR | NOT NULL ||
| location_description | VARCHAR | NOT NULL ||
| house_number | INT | NOT NULL | |
| street_name | VARCHAR | NOT NULL | |
| city | VARCHAR | NOT NULL ||
| state | VARCHAR | NOT NULL ||
| zip_code | INT | NOT NULL ||

--------------------
### Room: 
| Column | Type | Constraint | key|
|---|---|---|---|
| room_id | INT | UNIQUE | PK|
| room_number | INT | NOT NULL ||
| vacancy | BOOLEAN | NOT NULL ||
| resident_number | INT | NOT NULL ||
| parking_spot | INT | NOT NULL ||
| pet_friendly | BOOLEAN | NOT NULL ||
| fitness | BOOLEAN | NOT NULL ||
| rooftop_access | BOOLEAN | NOT NULL ||
| share_space_tidy_up | BOOLEAN | NOT NULL ||
| additional_feature | VARCHAR |  ||
| kitchen | BOOLEAN | NOT NULL ||
| furnished | BOOLEAN | NOT NULL ||
| floor | INT | NOT NULL ||
| bathroom | BOOLEAN | NOT NULL ||
| sqft | INT | NOT NULL ||
| property_id | INT | UNIQUE | FK|
| room_type_id | INT | NOT NULL | FK|
| laundry_type_id | INT | NOT NULL | FK|

------------------------
### Room_type: 
| Column | Type | Constraint | key|
|---|---|---|---|
| room_type_id | INT | NOT NULL |PK|
| room_type_name | VARCHAR | NOT NULL ||
| room_type_description | VARCHAR | NOT NULL ||

------------------------
### Laundry_type: 
| Column | Type | Constraint | key|
|---|---|---|---|
| laundry_type_id | INT | NOT NULL |PK|
| laundry_type_name | VARCHAR | NOT NULL ||
| laundry_type_description | VARCHAR | NOT NULL ||

------------------------

### Community: 
| Column | Type | Constraint | key|
|---|---|---|---|
| community_id | INT | UNIQUE | PK|
| community_name | VARCHAR | NOT NULL||
| community_description | VARCHAR | NOT NULL||

------------------------------

### Announcement: 
| Column | Type | Constraint | key|
|---|---|---|---|
| Announcement_id | INT | UNIQUE | PK|
| Announcement_name | VARCHAR | NOT NULL ||
| Announcement_description | VARCHAR | NOT NULL ||
| Announcement_time | TIME | NOT NULL||
| Community_id | INT | UNIQUE | FK|

------------------------------

### Event: 
| Column | Type | Constraint | key|
|---|---|---|---|
| Event_id | INT | UNIQUE | PK|
| Event_name | VARCHAR | NOT NULL ||
| Event_description | VARCHAR | NOT NULL ||
| Event_time | TIME | NOT NULL||
| Community_id | INT | UNIQUE | FK|

-----------------------

### Service_Provider:
| Column | Type | Constraint | key|
|---|---|---|---| 
| Service_provider_email | VARCHAR | UNIQUE | PK |
| Service_Provider_Full_name | VARCHAR | NOT NULL | |
| Category_id | INT | NOT NULL | FK |
| Password | BINARY(16) | NOT NULL ||
| Date_created | DATE | NOT NULL||
| Photo| BLOB | NOT NULL||
| Phone_Number | INT | NOT NULL ||
| Department_Id| INT | NOT NULL|FK|

------------------------




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
| email| INT | NOT NULL| FK |
| Time_placed|DATETIME| NOT NULL ||
| Status_Changed_Time|DATETIME| NOT NULL ||

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
| Service_provider_email | VARCHAR | UNIQUE | PK |
| Service_Provider_Full_name | VARCHAR | NOT NULL | |
| Category_id | INT | NOT NULL | FK |
| Password | BINARY(16) | NOT NULL ||
| Date_created | DATE | NOT NULL||
| Photo| BLOB | NOT NULL||
| Phone_Number | INT | NOT NULL ||
| Department_Id| INT | NOT NULL|FK|

--------------------------------------


### Service_Provider_Category:
| Column | Type | Constraint | key|
|---|---|---|---| 
| Service_Provider_Category_id | INT | UNIQUE | PK |
| Service_Provider_id | INT | UNIQUE | FK |
| Category_id | INT | UNIQUE | FK |

------------------------------------

### Department:
| Column | Type | Constraint | key|
|---|---|---|---| 
|Department_id| INT | NOT NULL | PK |
|Department_name| VARCHAR | NOT NULL ||
|Department_description| VARCHAR | NOT NULL ||


----------------------
### Reference:
[Sample Role-Based Access Control System](https://mysql.tutorials24x7.com/blog/guide-to-design-database-for-rbac-in-mysql)
