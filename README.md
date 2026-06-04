# Food Delivery System

A comprehensive Spring Boot-based backend application for a complete food delivery platform with microservices architecture. This system manages customers, restaurants, orders, delivery drivers, ratings, and coupons with comprehensive REST APIs for seamless order management and delivery tracking.

## Project Overview

The Food Delivery System is a full-fledged backend solution designed to handle all aspects of a food delivery business. It provides role-based security, JPA-based data persistence, and a modular structure with clear separation of concerns through controllers, services, DTOs, and custom exception handling.

## Key Features

- **Customer Management**: Register, authenticate, and manage customer profiles
- **Restaurant Management**: Restaurant registration, menu management, and operational control
- **Order Management**: Complete order lifecycle from placement to delivery
- **Delivery Tracking**: Real-time delivery driver assignment and tracking
- **Rating & Reviews**: Customer ratings and reviews for restaurants and delivery experience
- **Coupon System**: Dynamic coupon management and redemption
- **Role-Based Access Control**: Secure endpoints with role-based authorization
- **Exception Handling**: Comprehensive custom exception handling for better error management
- **Data Persistence**: Robust JPA-based ORM with database relationships

## Technology Stack

- **Framework**: Spring Boot 3.5.12
- **Language**: Java 21
- **Database ORM**: JPA (Java Persistence API)
- **Build Tool**: Maven
- **Architecture**: Microservices-based
- **API Style**: RESTful

## Project Structure

```
FoodDeliverySystem/
├── src/
│   ├── main/
│   │   ├── java/com/example/fooddeliverysystem/
│   │   │   ├── config/              # Configuration classes
│   │   │   ├── controller/          # REST Controllers
│   │   │   ├── dto/                 # Data Transfer Objects
│   │   │   ├── entity/              # JPA Entities
│   │   │   ├── exception/           # Custom Exceptions
│   │   │   ├── repository/          # Data Access Layer
│   │   │   ├── security/            # Security Configuration
│   │   │   ├── service/             # Business Logic Layer
│   │   │   └── FooddeliverysystemApplication.java  # Main Application
│   │   └── resources/
│   │       └── application.yaml     # Application Configuration
│   └── test/
│       └── java/                    # Unit & Integration Tests
├── pom.xml                          # Maven Dependencies
└── mvnw/mvnw.cmd                    # Maven Wrapper
```

## Core Entities

### 1. **Customer**
- User account management
- Delivery addresses
- Order history
- Profile information

### 2. **Restaurant**
- Business profile
- Menu items management
- Operating hours
- Location information

### 3. **MenuItem**
- Product details (name, description, price)
- Category classification
- Availability status
- Nutritional information

### 4. **Order**
- Order placement and tracking
- Multi-item support
- Status management
- Customer and restaurant linking

### 5. **OrderItem**
- Individual items in an order
- Quantity and pricing
- Customizations

### 6. **DeliveryDriver**
- Driver profile and authentication
- Current location tracking
- Assignment management
- Performance metrics

### 7. **DeliveryAddress**
- Multiple addresses per customer
- Delivery location details
- Address type classification

### 8. **Coupon**
- Discount code management
- Validity period tracking
- Usage limits and redemption

### 9. **OrderCoupon**
- Coupon application to orders
- Discount calculation
- Redemption history

### 10. **Rating**
- Customer ratings for restaurants
- Delivery experience ratings
- Review and feedback system

## API Endpoints

### Customer Endpoints
```
POST   /api/customers/register        - Register new customer
POST   /api/customers/login           - Customer login
GET    /api/customers/{id}            - Get customer profile
PUT    /api/customers/{id}            - Update customer profile
GET    /api/customers/{id}/orders     - Get customer orders
```

### Restaurant Endpoints
```
POST   /api/restaurants/register      - Register restaurant
GET    /api/restaurants               - Get all restaurants
GET    /api/restaurants/{id}          - Get restaurant details
GET    /api/restaurants/{id}/menu     - Get restaurant menu
```

### Order Endpoints
```
POST   /api/orders                    - Create new order
GET    /api/orders/{id}               - Get order details
GET    /api/orders                    - Get user orders
PUT    /api/orders/{id}/status        - Update order status
```

### Delivery Endpoints
```
GET    /api/deliveries/{id}           - Get delivery details
PUT    /api/deliveries/{id}/location  - Update delivery location
POST   /api/deliveries/{id}/complete  - Complete delivery
```

### Rating Endpoints
```
POST   /api/ratings                   - Submit rating
GET    /api/ratings/restaurant/{id}   - Get restaurant ratings
GET    /api/ratings/delivery/{id}     - Get delivery ratings
```

### Coupon Endpoints
```
GET    /api/coupons                   - Get available coupons
POST   /api/coupons/apply             - Apply coupon to order
GET    /api/coupons/validate/{code}   - Validate coupon code
```

## Getting Started

### Prerequisites
- Java 21 or higher
- Maven 3.6+
- MySQL or any compatible database
- Git

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/shreyasoniii/Food-Delivery-System.git
cd Food-Delivery-System/FoodDeliverySystem
```

2. **Configure Database**
Update `src/main/resources/application.yaml` with your database credentials:
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/food_delivery
    username: root
    password: your_password
  jpa:
    hibernate:
      ddl-auto: update
```

3. **Build the Project**
```bash
./mvnw clean install
```

4. **Run the Application**
```bash
./mvnw spring-boot:run
```

The application will start on `http://localhost:8080`

## Development Workflow

### Building
```bash
./mvnw clean package
```

### Running Tests
```bash
./mvnw test
```

### Code Generation
Maven will automatically generate entity classes and mappings based on the configurations.

## Architecture Overview

### Layered Architecture
```
┌─────────────────────────────────┐
│     REST Controllers            │  - API Endpoints
├─────────────────────────────────┤
│     Service Layer               │  - Business Logic
├─────────────────────────────────┤
│     Repository Layer            │  - Data Access
├─────────────────────────────────┤
│     Entity/Database             │  - Persistence
└─────────────────────────────────┘
```

### Key Design Patterns
- **MVC Pattern**: Controllers → Services → Repositories
- **DTO Pattern**: Data Transfer Objects for API communication
- **Exception Handling**: Global exception handlers
- **Security**: Role-based access control

## Database Schema Relationships

```
Customer 1──→ * DeliveryAddress
Customer 1──→ * Order
Customer 1──→ * Rating

Restaurant 1──→ * MenuItem
Restaurant 1──→ * Order
Restaurant 1──→ * Rating

Order 1──→ * OrderItem
Order 1──→ * OrderCoupon
Order 1──→ * DeliveryDriver
Order 1──→ * Rating

OrderItem 1──→ * MenuItem
OrderCoupon 1──→ * Coupon
```

## Configuration

### Application Properties
Key configurations in `application.yaml`:

```yaml
spring:
  application:
    name: fooddeliverysystem
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
  jpa:
    hibernate:
      dialect: org.hibernate.dialect.MySQL8Dialect
    show-sql: false
    properties:
      hibernate:
        format_sql: true
        jdbc:
          batch_size: 20
          fetch_size: 50
```

## Security

The application implements:
- JWT-based authentication for stateless requests
- Role-based authorization (Customer, Restaurant, Delivery Driver, Admin)
- Password encryption using BCrypt
- CORS configuration for cross-origin requests
- CSRF protection

## Error Handling

Custom exception classes handle various scenarios:
- `ResourceNotFoundException`: When requested resource is not found
- `UnauthorizedException`: When user lacks permissions
- `ValidationException`: When input validation fails
- `BusinessLogicException`: When business rules are violated

## Testing

The project includes unit and integration tests using:
- JUnit 5
- Mockito
- Spring Test Framework

Run tests with:
```bash
./mvnw test
```

## Performance Considerations

- Database connection pooling
- Query optimization with JPA
- Batch processing for bulk operations
- Lazy loading for related entities
- Caching mechanisms for frequently accessed data

## Future Enhancements

- [ ] Real-time notifications using WebSockets
- [ ] Payment gateway integration
- [ ] Advanced analytics and reporting
- [ ] Machine learning for recommendation engine
- [ ] Multi-language support
- [ ] Mobile app integration
- [ ] Admin dashboard
- [ ] Loyalty program system

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contact & Support

- **Developer**: Shreya Soni
- **GitHub**: [@shreyasoniii](https://github.com/shreyasoniii)
- **Email**: For inquiries, please reach out via GitHub

## Acknowledgments

- Spring Boot Community
- JPA/Hibernate Documentation
- Maven Community

---

**Last Updated**: June 4, 2026

For more information about Spring Boot, visit [Spring Boot Documentation](https://spring.io/projects/spring-boot)
