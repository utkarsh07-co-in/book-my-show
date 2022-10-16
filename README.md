# book-my-showBook My Show
Implementation
Application is developed in Spring Boot 2.0.0 with Java 8 on Spring Tool Suite IDE. Database used is MySQL 5.7.17.

You can book movie tickets using the application.

Mandatory entities to book a ticket are - user, movie, theater with seats, shows of configured movies in configured theater with seats.

Logging is done on console as well as file. Log file can be accessed at /var/log/bookmyshow.log.

Exception Handling is done using ExceptionInterceptor.

Unit test cases are present for User Operations - User Registration and User Get. Cases for exceptions are also handled.

Assumptions
For the simplicity of system, I have made following assumptions while implementing the solution -

Single User Model - One user will use at once. No locking implemented for seat selection.
Single Screen Theaters - No multiple screen handling for a theater has been done. However an option is given for future scope.
10 seats for each show are configured - 5 for CLASSIC and 5 for PREMIUM. Seat numbers are kept fixed in all theaters.
No Payment flow used.
Setup the Application
Create a database bookmyshow using the sql file bookmyshow.sql provided in src/main/resources.

Open src/main/resources/application.properties and change spring.datasource.username and spring.datasource.password properties as per your MySQL installation.

Type mvn spring-boot:run from the root directory of the project to run the application.

Setting up the data
Access the application using swagger on http://localhost:8080/bms/swagger-ui.html

Execute the API http://localhost:8080/bms/initialize/generate from swagger inside the heading data-populator. This will create a sample user, movie, theater, theater seats, shows, shows seats that will be used in booking ticket.

Booking a ticket
Use the show-controller heading in swagger and call the search API inside it using pageNo=1 and limit=10 to see the available list of shows.

Select any show from the above search result and copy its id.

Now go to ticket-controller in the swagger and execute the book ticket API using the following request body -

{"seatType":"CLASSIC","seatsNumbers":["1A"],"showId":1,"userId":1}

{ "seatType": "CLASSIC", "seatsNumbers": [ "1A" ], "showId": 1, "userId": 1 }

This will book a ticket for you and you will get ticket id along with show details in response.

Verifying the results from DB
Login to your MySQL and go to bookmyshow DB

SELECT * FROM bookmyshow.users; to see all registered users.

SELECT * FROM bookmyshow.movies; to see all movies.

SELECT * FROM bookmyshow.theaters; to see all theaters.

SELECT * FROM bookmyshow.theater_seats; to see all theater's seats.

SELECT * FROM bookmyshow.shows; to see all shows for movies in theaters.

SELECT * FROM bookmyshow.show_seats; to see all show's seats by type.

SELECT * FROM bookmyshow.tickets; to see all booked tickets.

Other API Details
UserController - API to add and get user

MovieController - API to add and get movie

TheaterController - API to add and get theater

ShowController - API to add and search show

Future Scope
Multiple user handling
Seat locking during payment
Multiple Screen handling in theater
Seat management on the fly
Payment Flow
Login and User Account Management
