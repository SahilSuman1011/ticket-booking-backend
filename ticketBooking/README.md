# 🎫 Ticket Booking System Engine

A comprehensive train ticket booking system built with Core Java, demonstrating object-oriented programming principles, functional programming with Stream API, and JSON-based data persistence.

## 📋 Features

- **User Authentication**: Secure sign-up and login with BCrypt password hashing
- **Train Search**: Search trains by source and destination stations with multi-station route validation
- **Seat Booking**: Real-time seat availability tracking with 24-seat inventory management
- **Booking Management**: View and cancel existing bookings
- **Data Persistence**: JSON-based storage for users and trains using Jackson serialization

## 🛠️ Technologies Used

- **Core Java 8**: Stream API, lambda expressions, functional interfaces
- **Jackson**: Object mapping and JSON serialization (`jackson-databind:2.12.6`)
- **BCrypt**: Password hashing and security (`jbcrypt:0.4`)
- **Lombok**: Boilerplate code reduction (`lombok:1.18.22`)
- **Gradle**: Build automation and dependency management

## 📁 Project Structure

```
ticketBooking/
├── app/
│   ├── src/
│   │   ├── main/java/ticket/booking/
│   │   │   ├── App.java                      # Main application entry point
│   │   │   ├── entities/
│   │   │   │   ├── User.java                 # User entity with tickets
│   │   │   │   ├── Train.java                # Train entity with seats
│   │   │   │   └── Ticket.java               # Ticket entity
│   │   │   ├── service/
│   │   │   │   ├── UserBookingService.java   # User and booking operations
│   │   │   │   └── TrainService.java         # Train search and management
│   │   │   ├── util/
│   │   │   │   └── UserServiceUtil.java      # Password hashing utilities
│   │   │   └── localDB/
│   │   │       ├── users.json                # User data storage
│   │   │       └── trains.json               # Train data storage
│   │   └── test/
│   └── build.gradle                          # Gradle build configuration
└── settings.gradle
```

## 🚀 Getting Started

### Prerequisites

- Java Development Kit (JDK) 8 or higher
- Gradle (included via wrapper)

### Installation

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd ticketBooking
   ```

2. **Build the project**

   ```bash
   ./gradlew build
   ```

3. **Run the application**
   ```bash
   ./gradlew run
   ```

## 💻 Usage

The application provides an interactive command-line interface with the following options:

1. **Sign Up**: Create a new user account with secure password hashing
2. **Login**: Authenticate existing users
3. **Fetch Bookings**: View all your current ticket bookings
4. **Search Trains**: Find trains between source and destination stations
5. **Book a Seat**: Reserve a seat on selected train
6. **Cancel Booking**: Cancel an existing reservation
7. **Exit**: Close the application

### Example Workflow

```
1. Sign up with username and password
2. Login with credentials
3. Search trains (e.g., source: "bangalore", destination: "delhi")
4. Select a train from search results
5. View available seats (24-seat grid: 4 rows × 6 columns)
6. Book a seat by entering row and column
7. Fetch bookings to confirm reservation
```

## 🔧 Technical Implementation

### Stream API & Functional Programming

- **User Authentication**: Uses `stream().filter()` with lambda expressions for credential validation

  ```java
  userList.stream()
      .filter(user1 -> user1.getName().equals(user.getName()) &&
                       UserServiceUtil.checkPassword(password, user1.getHashedPassword()))
      .findFirst();
  ```

- **Train Search**: Implements route validation through functional predicates
  ```java
  trainList.stream()
      .filter(train -> validTrain(train, source, destination))
      .collect(Collectors.toList());
  ```

### Data Persistence

- **Jackson ObjectMapper**: Custom object-to-JSON serialization
- **Snake Case Mapping**: `@JsonNaming(PropertyNamingStrategy.SnakeCaseStrategy.class)`
- **Type-Safe Deserialization**: `TypeReference<List<User>>()` for generic type handling

### Security

- **BCrypt Hashing**: Industry-standard password encryption with salt generation
- **Password Validation**: Secure comparison without plain-text storage

### Entity Models

- **User**: Manages authentication, tickets, and user profile
- **Train**: Handles seat inventory (4×6 matrix), stations, and schedules
- **Ticket**: Links users to trains with source, destination, and travel dates

## 📊 Data Format

### Trains JSON Structure

```json
{
  "train_id": "bacs",
  "train_no": 12345,
  "seats": [
    [0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0],
    [0, 0, 0, 0, 0, 0]
  ],
  "station_times": { "bangalore": "13:50:00", "delhi": "18:30:00" },
  "stations": ["bangalore", "jaipur", "delhi"]
}
```

### Users JSON Structure

```json
{
  "name": "username",
  "hashed_password": "$2a$10$...",
  "tickets_booked": [...],
  "user_id": "uuid-string"
}
```

## 🎯 Key Features Implemented

✅ **3 Core Entity Models**: User, Train, Ticket with full OOP encapsulation  
✅ **Stream API Operations**: filter, map, collect, findFirst with lambda expressions  
✅ **BCrypt Security**: Password hashing with salt generation  
✅ **JSON Persistence**: Jackson-based serialization/deserialization  
✅ **Multi-Station Validation**: Route checking with indexed station ordering  
✅ **24-Seat Management**: Real-time availability tracking (4 rows × 6 columns)

## 🔮 Future Enhancements

- Add ticket pricing and payment processing
- Implement date-based train scheduling
- Add concurrency control for seat booking (thread-safe operations)
- REST API wrapper for web/mobile clients
- Database integration (replace JSON files with PostgreSQL/MongoDB)
- Admin panel for train and route management

## 📝 License

This project is created for educational purposes.

## 👤 Author

Your Name - [GitHub Profile](https://github.com/yourusername)

---

**Built with ❤️ using Core Java, Stream API, and Jackson**
