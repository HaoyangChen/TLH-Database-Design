# Databse Design - The Living Hood App

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
- Resident_Statement
- Credit_Card_Info
- Work_Order
- Category
- Feedback
- Announcement
- Event
- Calendar
- Cleaning_Service


- Administrator (Do we need this?)//
- User //
- Role//
- User_to_Role//
- Role_to_Permission //
- Permission//

## 4: Deciding Relationships between tables
1) 1 account information is associated with only 1 tenant
2) 1 tenant 


Reference:
[Sample Role-Based Access Control System](https://mysql.tutorials24x7.com/blog/guide-to-design-database-for-rbac-in-mysql)