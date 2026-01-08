Day 7 – Databases (MySQL)

These are my practice notes for database concepts using MySQL in a Spring Boot application. The focus is on JPA mappings, transactions, concurrency handling, and auditing, from a real-world backend perspective.

Q1. Modeling Orders, OrderItems, and Users in Spring Boot
Q1.A Which JPA relationships would you use and why?

For this scenario:

A User can have multiple Orders, so I use a One-to-Many relationship from User to Order.

Each Order belongs to one User, so I use Many-to-One from Order to User.

An Order can have multiple OrderItems, so I use One-to-Many from Order to OrderItem.

Each OrderItem belongs to one Order, so I use Many-to-One from OrderItem to Order.

These relationships reflect real-world ownership and make querying easier.

Q1.B How do you handle cascading and orphan removal for OrderItems?

For Order and OrderItems:

I use cascade operations so that when an Order is saved or deleted, its OrderItems are also saved or deleted.

I use orphanRemoval = true so that if an OrderItem is removed from the Order, it is also removed from the database.

This helps keep the database consistent and avoids unused records.

Q1.C How do you enforce status transitions at the entity level?

I usually store order status as an enum like PENDING, PAID, SHIPPED.

To enforce valid transitions, I add checks inside entity or service methods. For example, an order should not move directly from PENDING to SHIPPED.

This ensures that invalid state changes are blocked early.

Q1.D Which annotations are essential for mapping?

Some important annotations used for mapping are:

@Entity to mark a class as a JPA entity

@Table to map the entity to a database table

@Id and @GeneratedValue for primary keys

@OneToMany and @ManyToOne for relationships

@JoinColumn to define foreign keys

Q2. Handling concurrency when two users purchase the last item
Q2.A How do you define transaction boundaries using @Transactional?

I use @Transactional at the service layer to ensure that all database operations within a method are executed as a single unit.

If any step fails, the transaction is rolled back, which prevents partial updates.

Q2.B Which isolation level would you choose and why?

In most cases, I prefer READ COMMITTED because it provides a good balance between consistency and performance.

For critical operations like reducing inventory count for the last item, SERIALIZABLE can be used to avoid race conditions, but it comes with performance overhead.

Q2.C Would you use optimistic or pessimistic locking?

I generally prefer optimistic locking for better performance when conflicts are rare. It is implemented using a @Version field in the entity.

For high-contention scenarios like inventory updates, pessimistic locking can be used to lock the row until the transaction completes.

Q2.D How do you handle deadlocks or retries?

I handle deadlocks by:

Keeping transactions short

Retrying failed transactions

Letting Spring retry logic or database retry mechanisms handle temporary failures

This improves system stability under load.

Q3. Implementing auditing for all entities
Q3.A Which annotations and listeners help achieve auditing?

To track who created or modified an entity, I use:

@CreatedBy

@LastModifiedBy

@CreatedDate

@LastModifiedDate

These annotations work with JPA auditing listeners.

Q3.B How do you integrate Spring Security context for auditing?

I implement an auditor provider that fetches the currently logged-in user from the Spring Security context.

This user information is automatically stored in createdBy and updatedBy fields.

Q3.C What limitations exist with detached entities?

Auditing does not work automatically for detached entities. If an entity is updated outside the persistence context, audit fields may not get updated.

To avoid this, entities should be updated within a managed transaction.

Q3.D How do you enable JPA auditing globally?

I enable auditing by adding @EnableJpaAuditing in a configuration class and registering the auditor provider.

This activates auditing for all entities across the project.
