Practice Questions – Day 8  
MongoDB & Persistence Framework

------------------------------------------------------------

1. How do you integrate MongoDB with a Spring Boot application?  
What dependencies and configuration are required?

a) Dependencies required  
To integrate MongoDB with a Spring Boot application, I use **Spring Data MongoDB**.  
This dependency provides built-in support for connecting to MongoDB and performing database operations.

Main dependency used:
- spring-boot-starter-data-mongodb

This starter internally includes the MongoDB driver and Spring Data support.

------------------------------------------------------------

b) Configuration required  
MongoDB configuration is done using the `application.properties` (or `application.yml`) file.

Common configurations include:
- MongoDB connection URI
- Database name
- Host and port (if URI is not used)

Example properties:
- spring.data.mongodb.uri  
- spring.data.mongodb.database  

Once configured, Spring Boot automatically establishes the MongoDB connection.

------------------------------------------------------------

c) Repository setup  
To interact with MongoDB, I create a repository interface that extends `MongoRepository`.

This allows:
- Saving documents  
- Fetching data  
- Updating and deleting records  

No implementation class is required because Spring Boot provides it automatically.

------------------------------------------------------------

d) Overall flow  
1. Add MongoDB dependency  
2. Configure MongoDB in properties file  
3. Create model class  
4. Create repository interface  
5. Use repository in service layer  

============================================================

2. Difference between MongoDB and JPA / Hibernate

| Feature            | MongoDB (NoSQL)                 | JPA / Hibernate (SQL)        |
|--------------------|----------------------------------|------------------------------|
| Database type      | Document-based                   | Relational                   |
| Data structure     | JSON-like documents              | Tables (rows & columns)      |
| Schema             | Schema-less                      | Fixed schema                 |
| Relationships      | Embedded / manual references     | Joins & foreign keys         |
| Transactions       | Limited support                  | Full ACID support            |
| Scalability        | High                             | Moderate                     |

Key understanding:
- MongoDB is suitable for flexible and scalable applications  
- JPA/Hibernate is suitable for highly relational data  

============================================================

3. What is the difference between MongoRepository and CrudRepository?  
When would you prefer MongoRepository?

a) CrudRepository  
- Provides basic CRUD operations  
- Database independent  
- Lightweight and minimal  

Common methods:
- save()  
- findById()  
- findAll()  
- deleteById()  

------------------------------------------------------------

b) MongoRepository  
- Extends CrudRepository  
- Specifically designed for MongoDB  
- Provides additional MongoDB-specific features  

Extra features:
- Pagination  
- Sorting  
- MongoDB query methods  

------------------------------------------------------------

c) When I prefer MongoRepository  
I prefer MongoRepository when:
- The application uses MongoDB  
- Pagination or sorting is required  
- MongoDB-specific queries are needed  

For small applications, CrudRepository is sufficient, but for real-world projects, MongoRepository is preferred.

============================================================

4. How is a MongoDB document mapped to a Java class in Spring Boot?  
Explain using annotations.

a) @Document  
- Used at class level  
- Maps the class to a MongoDB collection  

Example:
- @Document(collection = "users")

------------------------------------------------------------

b) @Id  
- Marks the primary key of the document  
- Maps to MongoDB’s `_id` field  

------------------------------------------------------------

c) @Field  
- Maps Java fields to MongoDB fields  
- Useful when field names differ  

------------------------------------------------------------

d) Other annotations  
- @Transient → field not stored in database  
- @Indexed → creates index on a field  

------------------------------------------------------------

e) Summary  
Spring Data MongoDB automatically converts Java objects into MongoDB documents using these annotations.

============================================================

5. How do you handle indexing and performance optimization in MongoDB  
when used with Spring Boot?

a) Indexing  
Indexes improve query performance by reducing document scan time.

Spring Boot supports indexing using:
- @Indexed  
- @CompoundIndex  

------------------------------------------------------------

b) Query optimization  
- Avoid fetching unnecessary fields  
- Use indexed fields in queries  
- Write efficient query methods  

------------------------------------------------------------

c) Pagination  
Pagination avoids loading large datasets into memory.  
Spring Data MongoDB provides pagination support using `Pageable`.

------------------------------------------------------------

d) Embedded documents  
Embedding related data instead of joins improves read performance in MongoDB.

------------------------------------------------------------

e) Overall approach  
1. Create indexes on frequently queried fields  
2. Use pagination for large datasets  
3. Avoid unindexed queries  
4. Design document structure properly  

------------------------------------------------------------
