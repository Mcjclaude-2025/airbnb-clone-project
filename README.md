# airbnb-clone-project
The initial project in my learning journey in the AlX Prodev course


          Team Roles
Business Analyst (BA): Translates business needs into technical requirements; bridges client vision and development execution.

Product Owner (PO): Owns the product vision; prioritizes features and ensures the final product meets customer needs.

Project Manager (PM): Oversees timelines, budgets, and team coordination; ensures smooth delivery and stakeholder alignment.

UI/UX Designer: Designs user interfaces and experiences; focuses on usability, aesthetics, and user journey optimization.

Software Architect: Defines high-level system architecture; selects tools, sets coding standards, and ensures scalability.

Software Developer: Builds the application; includes front-end, back-end, or full-stack engineers depending on scope.

Quality Assurance (QA) Engineer: Tests functionality and performance; ensures the product meets requirements and is bug-free.

Test Automation Engineer: Develops automated test scripts; speeds up testing and ensures consistent quality checks.

DevOps Engineer: Bridges development and operations; builds CI/CD pipelines and ensures efficient, stable deployments.

                Database Design
Designing a database for an Airbnb-like app requires identifying key entities, their attributes, and relationships to support core functionalities like user management, property listings, bookings, reviews, and payments. Below is a detailed database design with key entities, their important fields, and how they are related.

---

### Key Entities and Fields

1. **Users**
   - Description: Represents hosts and guests using the platform.
   - Fields:
     - `user_id` (Primary Key): Unique identifier for each user.
     - `email`: User's email for login and communication.
     - `name`: Full name of the user.
     - `password_hash`: Securely hashed password for authentication.
     - `phone_number`: Contact number for verification and communication.
   - Additional Notes: May include fields like `profile_picture`, `is_host` (boolean to indicate host status), or `created_at` for account creation timestamp.

2. **Properties**
   - Description: Represents listings (e.g., homes, apartments) available for booking.
   - Fields:
     - `property_id` (Primary Key): Unique identifier for each property.
     - `host_id` (Foreign Key): Links to the `user_id` of the host.
     - `title`: Name or title of the listing (e.g., "Cozy Beach Cottage").
     - `location`: Address or coordinates (e.g., city, country, or lat/long).
     - `price_per_night`: Cost per night in the local currency.
   - Additional Notes: Could include fields like `description`, `max_guests`, or `amenities` (e.g., Wi-Fi, parking).

3. **Bookings**
   - Description: Represents reservations made by guests for properties.
   - Fields:
     - `booking_id` (Primary Key): Unique identifier for each booking.
     - `property_id` (Foreign Key): Links to the booked property.
     - `guest_id` (Foreign Key): Links to the `user_id` of the guest.
     - `check_in_date`: Start date of the stay.
     - `check_out_date`: End date of the stay.
   - Additional Notes: May include `total_price` or `status` (e.g., confirmed, canceled).

4. **Reviews**
   - Description: Represents feedback and ratings for properties or hosts left by guests.
   - Fields:
     - `review_id` (Primary Key): Unique identifier for each review.
     - `property_id` (Foreign Key): Links to the reviewed property.
     - `guest_id` (Foreign Key): Links to the `user_id` of the reviewer.
     - `rating`: Numerical score (e.g., 1-5 stars).
     - `comment`: Text description of the guest’s experience.
   - Additional Notes: Could include `created_at` for timestamp or `host_response` for host replies.

5. **Payments**
   - Description: Represents transactions for bookings.
   - Fields:
     - `payment_id` (Primary Key): Unique identifier for each payment.
     - `booking_id` (Foreign Key): Links to the associated booking.
     - `amount`: Total payment amount.
     - `payment_date`: Date the payment was processed.
     - `payment_status`: Status (e.g., completed, pending, refunded).
   - Additional Notes: May include `payment_method` (e.g., credit card, PayPal) or `transaction_id` for external payment systems.

---

### Relationships Between Entities

1. **Users and Properties**:
   - Relationship: One-to-Many
   - Description: A user (host) can own multiple properties, but each property is owned by exactly one host.
   - Implementation: The `host_id` field in the Properties table is a foreign key referencing the `user_id` in the Users table.

2. **Properties and Bookings**:
   - Relationship: One-to-Many
   - Description: A property can have multiple bookings, but each booking is associated with exactly one property.
   - Implementation: The `property_id` field in the Bookings table is a foreign key referencing the `property_id` in the Properties table.

3. **Users and Bookings**:
   - Relationship: One-to-Many
   - Description: A user (guest) can make multiple bookings, but each booking is made by exactly one guest.
   - Implementation: The `guest_id` field in the Bookings table is a foreign key referencing the `user_id` in the Users table.

4. **Properties and Reviews**:
   - Relationship: One-to-Many
   - Description: A property can have multiple reviews, but each review is associated with exactly one property.
   - Implementation: The `property_id` field in the Reviews table is a foreign key referencing the `property_id` in the Properties table.

5. **Users and Reviews**:
   - Relationship: One-to-Many
   - Description: A user (guest) can write multiple reviews, but each review is written by exactly one guest.
   - Implementation: The `guest_id` field in the Reviews table is a foreign key referencing the `user_id` in the Users table.

6. **Bookings and Payments**:
   - Relationship: One-to-One
   - Description: Each booking has exactly one payment, and each payment is associated with exactly one booking.
   - Implementation: The `booking_id` field in the Payments table is a foreign key referencing the `booking_id` in the Bookings table.

---

### Additional Considerations

- **Normalization**: The design follows normalization principles to reduce redundancy. For example, separating Users and Properties ensures that host information isn’t duplicated across listings.
- **Scalability**: For large-scale systems, additional tables like `Amenities` (for property features) or `Messages` (for host-guest communication) could be added.
- **Indexes**: Create indexes on frequently queried fields like `property_id`, `user_id`, or `check_in_date` to optimize performance.
- **Data Types**: Choose appropriate data types (e.g., VARCHAR for `email`, DECIMAL for `price_per_night`, DATE for `check_in_date`) based on the database system (e.g., MySQL, PostgreSQL).
- **Security**: Store sensitive data like `password_hash` securely and consider encrypting fields like `phone_number`


            Feature Breakdown
Based on the Airbnb app database design provided, the main features of the project can be inferred from the entities and their relationships. Below is a list of the main features—User Management, Property Management, Booking System, Review System, and Payment System—along with a 2-3 sentence description of each, explaining their contribution to the project.

---

### Main Features

1. **User Management**
   - **Description**: This feature handles the registration, authentication, and profile management of users, including both hosts and guests. It supports functionalities like account creation, login, and updating personal details such as email, name, and phone number.
   - **Contribution**: User Management ensures secure access to the platform and distinguishes between hosts and guests, enabling personalized experiences and trust through verified profiles.

2. **Property Management**
   - **Description**: Allows hosts to create, update, and manage property listings, including details like title, location, price, and amenities. Guests can search and view these listings to find suitable accommodations.
   - **Contribution**: Property Management is the core of the platform, enabling hosts to offer their spaces and guests to discover and evaluate properties, driving the marketplace functionality.

3. **Booking System**
   - **Description**: Facilitates the reservation process by allowing guests to book properties for specific dates and hosts to manage availability. It tracks check-in/check-out dates and booking status to ensure smooth coordination.
   - **Contribution**: The Booking System enables seamless transactions between guests and hosts, ensuring properties are reserved efficiently and conflicts (e.g., double bookings) are avoided.

4. **Review System**
   - **Description**: Enables guests to leave ratings and comments about their stay, and hosts to respond to feedback. Reviews are linked to specific properties and users to provide transparency.
   - **Contribution**: The Review System builds trust and accountability in the platform by allowing users to share experiences, helping future guests make informed decisions and encouraging hosts to maintain quality.

5. **Payment System**
   - **Description**: Manages financial transactions for bookings, including processing payments, tracking amounts, and handling statuses like completed or refunded. It links payments directly to bookings for accurate record-keeping.
   - **Contribution**: The Payment System ensures secure and reliable transactions, providing confidence to users and enabling the platform to handle revenue flow effectively.
