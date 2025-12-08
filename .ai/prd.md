# Product Requirements Document (PRD) - Parking Tracker

## 1\. Product Overview

Parking Tracker is an internal web application designed to simplify and automate the process of booking parking spots at the company's offices.

The MVP (Minimum Viable Product) version focuses on delivering core functionalities that will allow employees to independently book, view, and cancel parking spot reservations. The application will also feature a basic Administrator role, enabling the management of individual spot availability. In its initial phase, the product will be available as a web application optimized for use on laptops.

## 2\. User Problem

Currently, employees who commute to the office by car face uncertainty regarding the availability of a parking spot. The lack of a central system causes conflicts, double bookings, and situations where reserved spots remain empty while other employees cannot find parking.

## 3\. Functional Requirements

### 3.1. Authentication and Authorization

* The system will use Supabase Auth for user authentication. All application users must be company employees.
* There are two user roles:

  * User (Employee): Can book, view, and cancel their own reservations.
  * Administrator: Has User permissions plus access to a dedicated admin panel.

### 3.2. User Profile

* Every user has a profile containing the following fields:

  * First Name
  * Last Name
  * Team Name
  * Default Office
  * Vehicle License Plate
  * Vehicle Brand/Model (a single text field)

* The user can edit the information in their profile.

### 3.3. Booking System

* A user can book one parking spot for a given day.
* Bookings can be made up to 7 business days in advance.
* A booking can be canceled no later than 3:00 AM (3 hours before 6:00 AM) on the day of the reservation.
* If there are no available spots for a given day, the application will display an appropriate message. The system will not support a waitlist.
* A booking is assigned to a specific parking spot chosen by the user.

### 3.4. User Interface (UI)

* The application is a web app intended for use on laptops.
* The main booking process view consists of:

  1. A calendar view where the user selects the desired day.
  2. After selecting a day, the user selects the office and parking level (if applicable).
  3. After selecting the location, an interactive parking lot map (created in HTML/CSS/react-konva) is displayed with clearly marked spots (available, taken, out of service).
  4. The user makes a booking by clicking on a selected available spot.

* The user has access to a separate "My Bookings" view, where they can see their upcoming and past bookings and cancel upcoming ones.

### 3.5. Admin Panel

* Users with the Administrator role have access to a dedicated view.
* The Admin Panel allows for enabling and disabling individual parking spots (e.g., for maintenance or a special guest reservation).
* A disabled spot becomes impossible to book by standard users.

## 4\. Product Boundaries

The following features and issues are intentionally excluded from the MVP scope:

* No "no-shows" handling: The MVP version will not include mechanisms to penalize or monitor users who book a spot but do not show up. This is identified as a key risk to be addressed in future versions.
* No waitlist: The application will not offer an option to sign up for a waiting list for a freed-up spot.
* Limited profile functionality: The "default office" and "team name" fields will be collected in the profile but will not be used for automation, filtering, or reporting in the MVP.
* In-app role management: The process of granting and revoking the "Administrator" role will not occur within the application interface. This will be a task performed manually, directly in the Supabase panel.
* No mobile apps: The MVP is a web application, with no dedicated versions for iOS or Android.
* Static parking lot management: Adding new parking lots, changing their visual layout, or modifying the total number of spots will require developer intervention and database modifications, and will not be possible from the Admin Panel.

## 5\. User Stories

### Authentication and User Profile

* ID: US-001
* Title: Logging into the application
* Description: As an employee, I want to be able to securely log into the application to access the booking system.
* Acceptance Criteria:

  * Access to the application is protected and requires authentication.
  * The login system is integrated with Supabase Auth.
  * After a successful login, I am redirected to the main application view (e.g., the booking calendar).
  * In case of a failed login attempt, I see a clear error message.

* ID: US-002
* Title: Managing user profile
* Description: As an employee, I want to be able to view and edit my profile information, such as my vehicle or team, to keep it up to date.
* Acceptance Criteria:

  * There is a "My Profile" section in the application.
  * The profile displays the fields: first name, last name, team name, default office, vehicle license plate, brand/model.
  * I can edit the fields: team name, default office, license plate, brand/model.
  * After saving the changes, they are permanently stored in the system.

### Booking Process

* ID: US-003
* Title: Browsing spot availability in the calendar
* Description: As an employee, I want to see in the calendar which days I can make a booking for, to quickly get an overview of available dates.
* Acceptance Criteria:

  * I can see a calendar interface.
  * Past dates and dates more than 7 business days in the future are inactive (cannot be clicked).
  * Optionally: Days with a fully booked parking lot can be visually distinguished.

* ID: US-004
* Title: Selecting a spot on the interactive map
* Description: As an employee, after selecting a day and office, I want to see an interactive map of the parking lot so I can choose a specific, preferred spot.
* Acceptance Criteria:

  * After selecting a day and location, a parking lot map appears on the screen.
  * The spots on the map have three clearly distinguishable visual statuses: available, taken, out of service.
  * I can hover over a taken spot to (optionally) see who booked it.
  * I cannot click or select a spot that is already taken or out of service.

* ID: US-005
* Title: Making a parking spot reservation
* Description: As an employee, I want to be able to book a selected available parking spot to be sure of parking when I arrive at the office.
* Acceptance Criteria:

  * After clicking on an available spot on the map, I see a request to confirm the booking.
  * After confirmation, the booking is saved to my account in the system.
  * The spot I selected immediately changes its status to "taken" for me and other users viewing the same day.
  * I receive a visual confirmation of a successful booking.

* ID: US-006
* Title: Attempting to book on a day with no available spots
* Description: As an employee, when trying to book a spot on a day when all spots are already taken, I want to receive a clear message about the lack of availability.
* Acceptance Criteria:

  * After selecting a day on which all spots are taken, the application displays a message, e.g., "No available spots on this day."
  * The interactive parking map is not displayed, or all spots on the map are marked as taken.
  * The system does not offer an option to be added to a waitlist.

* ID: US-007
* Title: Attempting to make a second booking for the same day
* Description: As an employee who already has a booking for a given day, I want the system to prevent me from making another booking for the same day.
* Acceptance Criteria:

  * If I already have a booking for the selected day, the system does not allow me to initiate the process of booking another spot.
  * The booking button is inactive, or I see a message like "You already have a booking for this day."

### Booking Management

* ID: US-008
* Title: Viewing my bookings
* Description: As an employee, I want to have access to a list of my upcoming and past bookings to easily manage my plans.
* Acceptance Criteria:

  * There is a "My Bookings" section in the application.
  * The list includes information about the date, office, and the number of the booked spot.
  * Bookings are divided into upcoming and past.
  * A "Cancel" button is visible next to each upcoming booking.

* ID: US-009
* Title: Canceling a booking within the allowed time frame
* Description: As an employee whose plans have changed, I want to be able to cancel my booking to free up the spot for others.
* Acceptance Criteria:

  * In the "My Bookings" view, I click the "Cancel" button next to an upcoming booking.
  * The operation is possible if there are more than 3 hours left until 6:00 AM on the day of the booking.
  * After confirming the cancellation, the booking is removed from my account.
  * The canceled parking spot immediately becomes available for booking by other users.

* ID: US-010
* Title: Attempting to cancel a booking after the deadline
* Description: As an employee trying to cancel a booking too late, I want the system to prevent this and inform me about it.
* Acceptance Criteria:

  * An attempt to cancel a booking for a given day after 3:00 AM on that day fails.
  * The "Cancel" button in the "My Bookings" view is inactive, or clicking it displays a message informing me that the cancellation deadline has passed.

### Admin Functions

* ID: US-011
* Title: Accessing the admin panel
* Description: As an Administrator, I want to have access to a special panel that is not visible to regular users, to manage the parking lots.
* Acceptance Criteria:

  * After logging in as a user with the "Administrator" role, I see a link to the "Admin Panel" in the navigation.
  * A regular user does not see this link and cannot access the panel (e.g., via a direct URL).

* ID: US-012
* Title: Disabling a parking spot
* Description: As an Administrator, I want to be able to temporarily disable a specific parking spot from being booked, e.g., due to maintenance.
* Acceptance Criteria:

  * In the Admin Panel, I can select an office and see the interactive parking map.
  * By clicking on any spot (available or taken), I can change its status to "out of service."
  * A spot with the "out of service" status cannot be booked by any user.
  * If the spot was booked at the time of being disabled, that booking should be automatically canceled, and the user informed (notification functionality may be outside MVP scope, but the spot's status must change).

* ID: US-013
* Title: Enabling a parking spot
* Description: As an Administrator, I want to be able to re-enable a spot that was previously disabled.
* Acceptance Criteria:

  * In the Admin Panel, by clicking on a spot with the "out of service" status, I can change its status to "available."
  * After the status change, the spot immediately becomes visible as available for booking to all users.

## 6\. Success Metrics

### 6.1. Key Performance Indicator (KPI)

* Metric: Percentage of active users who have made at least 4 bookings in the last month.
* Goal: To measure regular use of the application and habit-building among employees, which indicates its utility and fit with user needs. A high rate will mean the application has become an integral part of hybrid work planning.

### 6.2. Supporting Metrics

* Parking Occupancy Rate: The average percentage of occupied parking spots on different days of the week and in different offices. This will help identify trends and actual parking demand.
* Adoption Rate: The ratio of the number of registered users to the total number of employees eligible to use the parking. This will show how effectively the tool has been implemented in the organization.
* Individual Spot Utilization: Monitoring which spots are booked most frequently and which are booked least frequently. This can help identify less attractive spots and take action to improve their utilization.
