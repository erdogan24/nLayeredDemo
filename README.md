🧩 nLayeredDemo (Java)

A concise N-Layered Architecture demo in Java, showcasing clean separation of concerns, loose coupling, and the Adapter pattern. 
The domain is a simple product catalog. The app runs in the console and illustrates how the Business, Data Access, Core (cross-cutting), and Entities layers interact.

🎯 Purpose

This project exists to teach and demonstrate layered design and SOLID principles without heavy dependencies. It shows how to:
	•	Define business contracts and implement them with dependency injection.
	•	Swap data access implementations (Hibernate DAO vs a fake ABC DAO) without touching business code.
	•	Integrate a third-party logger via an Adapter, keeping the core code clean.

⚙️ What It Does
	•	Entity Model: A Product with fields like id, categoryId, name, unitPrice, and unitsInStock.
	•	Business Layer: ProductService (interface) and ProductManager (implementation) coordinate product operations and logging.
	•	Data Access Layer: ProductDao (interface) with two concrete DAOs:
	•	HibernateProductDao (simulated Hibernate-style data access)
	•	AbcProductDao (another concrete DAO to show plug-and-play switching)
	•	Core (Cross-cutting): LoggerService (interface) and JLoggerManagerAdapter which adapts a third-party logger (JLoggerManager) to your own logging contract.
	•	Console Demo: Main.java wires everything together (e.g., new ProductManager(new AbcProductDao(), new JLoggerManagerAdapter())) and performs sample operations, printing results to the console.

You’ll see console messages like “J Logger ile logland: …” coming from the adapter, proving that the business layer only knows about LoggerService, not the third-party logger.

🧱 Architecture (Layers in Plain English)
	•	Entities: Pure data structures (e.g., Product) implementing marker interfaces (e.g., Entity) to distinguish domain models.
	•	DataAccess: Abstract interface ProductDao plus multiple implementations (HibernateProductDao, AbcProductDao). Business code depends only on the interface, so implementations are swappable.
	•	Business: ProductService defines what the app should do; ProductManager contains the use-case logic and relies on ProductDao and LoggerService abstractions.
	•	Core: Cross-cutting services and adapters. JLoggerManagerAdapter implements your LoggerService and internally calls third-party JLoggerManager, achieving decoupling.
	•	jLogger: A mock third-party logger (JLoggerManager) standing in for any external library you might need to adapt.

🔌 Design Principles & Patterns
	•	SOLID: Especially Dependency Inversion — high-level modules (business) depend on abstractions (ProductDao, LoggerService), not concrete classes.
	•	Adapter Pattern: JLoggerManagerAdapter maps an external logger’s API to your own interface so the rest of your code stays clean.
	•	Loose Coupling: Switch data access or logging strategies without breaking business code.

🚀 How to Run
	1.	Ensure you have JDK 8+ installed.
	2.	Compile and run from the project root:
javac -d out $(find nLayeredDemo-master/nLayeredDemo/src -name "*.java")
java -cp out nLayeredDemo.Main


  3.	Watch the console output as the program:
	•	Creates a ProductService with a chosen DAO (AbcProductDao or HibernateProductDao)
	•	Logs actions via JLoggerManagerAdapter
	•	Executes simple product operations to demonstrate the flow

🧠 Why This Matters
	•	Shows clean boundaries between layers and how to keep business rules independent from frameworks.
	•	Demonstrates testability: swap DAOs or loggers with fakes/mocks for unit tests.
	•	Serves as a starter template for bigger systems that need maintainability and easy refactoring.

  
