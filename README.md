# BookMyShow Database Design

## Entities and Attributes:

1. **Theatre**
   - TheatreID (Primary Key)
   - Name
   - Location
   - Capacity
   - ContactNumber

2. **Movie**
   - MovieID (Primary Key)
   - Title
   - Genre
   - Language
   - Duration
   - Rating

3. **Show**
   - ShowID (Primary Key)
   - MovieID (Foreign Key)
   - TheatreID (Foreign Key)
   - Date
   - Time
   - Price
   - SeatsAvailable

4. **Booking**
   - BookingID (Primary Key)
   - ShowID (Foreign Key)
   - UserID (Foreign Key)
   - NumTickets
   - TotalPrice
   - BookingDate

5. **User**
   - UserID (Primary Key)
   - Name
   - Email
   - PhoneNumber

## Table Structures:

```sql
CREATE TABLE Theatre (
    TheatreID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Location VARCHAR(255),
    Capacity INT,
    ContactNumber VARCHAR(20)
);

CREATE TABLE Movie (
    MovieID INT AUTO_INCREMENT PRIMARY KEY,
    Title VARCHAR(255) NOT NULL,
    Genre VARCHAR(100),
    Language VARCHAR(50),
    Duration INT,
    Rating DECIMAL(3, 1)
);

CREATE TABLE Show (
    ShowID INT AUTO_INCREMENT PRIMARY KEY,
    MovieID INT,
    TheatreID INT,
    Date DATE,
    Time TIME,
    Price DECIMAL(6, 2),
    SeatsAvailable INT,
    FOREIGN KEY (MovieID) REFERENCES Movie(MovieID),
    FOREIGN KEY (TheatreID) REFERENCES Theatre(TheatreID)
);

CREATE TABLE Booking (
    BookingID INT AUTO_INCREMENT PRIMARY KEY,
    ShowID INT,
    UserID INT,
    NumTickets INT,
    TotalPrice DECIMAL(8, 2),
    BookingDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (ShowID) REFERENCES Show(ShowID),
    FOREIGN KEY (UserID) REFERENCES User(UserID)
);

CREATE TABLE User (
    UserID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Email VARCHAR(255),
    PhoneNumber VARCHAR(20)
);
```


## Sample Entries:

```sql
-- Insert sample data into Theatre table
INSERT INTO Theatre (Name, Location, Capacity, ContactNumber)
VALUES ('PVR Cinemas', '123 ABC Road, Mumbai', 300, '95295XXXXX');

-- Insert sample data into Movie table
INSERT INTO Movie (Title, Genre, Language, Duration, Rating)
VALUES ('Baahubali: The Beginning', 'Action, Drama', 'Hindi', 159, 8.1);

-- Insert sample data into Show table
INSERT INTO Show (MovieID, TheatreID, Date, Time, Price, SeatsAvailable)
VALUES (1, 1, '2024-02-25', '15:00:00', 10.00, 200);

-- Insert sample data into User table
INSERT INTO User (Name, Email, PhoneNumber)
VALUES ('Jayant C', 'jayant.c@example.com', '95295XXXXX');
```

## SQL Queries:

### P1: Create Tables

```sql
-- Create Theatre Table
CREATE TABLE Theatre (
    TheatreID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Location VARCHAR(255),
    Capacity INT,
    ContactNumber VARCHAR(20)
);

-- Create Movie Table
CREATE TABLE Movie (
    MovieID INT AUTO_INCREMENT PRIMARY KEY,
    Title VARCHAR(255) NOT NULL,
    Genre VARCHAR(100),
    Language VARCHAR(50),
    Duration INT,
    Rating DECIMAL(3, 1)
);

-- Create Show Table
CREATE TABLE Show (
    ShowID INT AUTO_INCREMENT PRIMARY KEY,
    MovieID INT,
    TheatreID INT,
    Date DATE,
    Time TIME,
    Price DECIMAL(6, 2),
    SeatsAvailable INT,
    FOREIGN KEY (MovieID) REFERENCES Movie(MovieID),
    FOREIGN KEY (TheatreID) REFERENCES Theatre(TheatreID)
);

-- Create User Table
CREATE TABLE User (
    UserID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Email VARCHAR(255),
    PhoneNumber VARCHAR(20)
);

-- Create Booking Table
CREATE TABLE Booking (
    BookingID INT AUTO_INCREMENT PRIMARY KEY,
    ShowID INT,
    UserID INT,
    NumTickets INT,
    TotalPrice DECIMAL(8, 2),
    BookingDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (ShowID) REFERENCES Show(ShowID),
    FOREIGN KEY (UserID) REFERENCES User(UserID)
);
```

### P2: Query for Shows on a Given Date at a Given Theatre

```sql
SELECT s.ShowID, m.Title, s.Date, s.Time
FROM Show s
JOIN Movie m ON s.MovieID = m.MovieID
WHERE s.Date = '2024-02-25' AND s.TheatreID = 1;
```
