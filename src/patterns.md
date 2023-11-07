
## Architectural Patterns

Architectural and enterprise patterns are higher-level design patterns that address the overall structure, organization, and management of a software system or application. They help in defining the software's architecture and organization at a macro level, ensuring that the system is scalable, maintainable, and adheres to best practices. Let's explore these patterns in more detail:

**Architectural Patterns:**

1. **Model-View-Controller (MVC):**
   - **Purpose:** Separates an application into three interconnected components: Model (data and business logic), View (presentation and user interface), and Controller (user input handling and application flow).
   - **Example:** Web applications, where the Model manages data and logic, the View displays the user interface, and the Controller handles user interactions.

2. **Model-View-ViewModel (MVVM):**
   - **Purpose:** Extends the MVC pattern for client applications by adding a ViewModel that abstracts the view's state and behavior. MVVM is commonly used in XAML-based platforms.
   - **Example:** WPF and Xamarin applications, where the ViewModel abstracts the UI behavior and data binding.

3. **Three-Tier Architecture:**
   - **Purpose:** Separates a system into three logical layers: Presentation (UI), Business Logic, and Data Storage. This architecture enhances maintainability and scalability.
   - **Example:** Enterprise applications, web applications, and many client-server systems.

4. **Microservices:**
   - **Purpose:** Decomposes an application into a collection of small, independent services that can be developed, deployed, and scaled individually. Microservices aim to improve agility and scalability.
   - **Example:** Large-scale web applications, e-commerce platforms, and cloud-native systems.

5. **Event-Driven Architecture (EDA):**
   - **Purpose:** Emphasizes the production, detection, consumption, and reaction to events. Events are used to trigger actions and communicate between different parts of the system.
   - **Example:** Real-time applications, financial systems, and IoT platforms.

**Enterprise Patterns:**

1. **Unit of Work:**
   - **Purpose:** Manages database transactions and ensures that changes to the database are performed as a single unit. It helps maintain data consistency and integrity.
   - **Example:** Enterprise-level applications that use ORMs like Entity Framework.

2. **Repository Pattern:**
   - **Purpose:** Separates the domain model from the data access layer. It provides an abstraction for data storage operations, making the code more testable and maintainable.
   - **Example:** Applications that interact with databases, APIs, or other data sources.

3. **Service Locator:**
   - **Purpose:** Provides a centralized registry for services, allowing clients to locate and use services without direct dependencies. It promotes modularity and flexibility.
   - **Example:** Large-scale applications where various services need to be dynamically located and used.

4. **Dependency Injection (DI):**
   - **Purpose:** A technique rather than a pattern, DI involves injecting dependencies into a component rather than having the component create them. It improves testability and reduces coupling.
   - **Example:** Used in conjunction with many other patterns and frameworks, such as ASP.NET Core and Spring.

5. **Message Queue:**
   - **Purpose:** Decouples components and services by using a message queue to transmit messages asynchronously. It enhances scalability and fault tolerance.
   - **Example:** Enterprise applications with distributed components, background processing, or asynchronous communication.

6. **Domain-Driven Design (DDD):**
   - **Purpose:** Focuses on modeling the domain of the software, emphasizing collaboration between domain experts and software developers. DDD promotes a shared understanding of the problem domain.
   - **Example:** Complex business applications and projects where understanding and modeling the domain is crucial.

7. **Enterprise Integration Patterns (EIP):**
   - **Purpose:** Defines a set of patterns and best practices for integrating different systems and applications within an enterprise. It helps handle messaging, routing, and transformation.
   - **Example:** Middleware solutions, enterprise service buses (ESBs), and system integrations.

These architectural and enterprise patterns provide guidelines and best practices for structuring and managing software systems at a high level. They are essential for designing robust, scalable, and maintainable applications, especially in complex enterprise scenarios.

## Design Patterns

### Creational Patterns

Creational design patterns are a subset of design patterns that deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. They promote flexibility in the way objects are created, decoupling the system from the specific classes it needs to instantiate. Here are some of the most common creational design patterns with examples:

1. **Singleton Pattern:**
   - Purpose: Ensures a class has only one instance and provides a global point of access to it.
   - Example: A configuration manager that reads settings from a file and provides access to those settings throughout the application.
   
   ```csharp
   public class Singleton
   {
       private static Singleton instance;
       private Singleton() { }

       public static Singleton Instance
       {
           get
           {
               if (instance == null)
               {
                   instance = new Singleton();
               }
               return instance;
           }
       }
   }
   ```

2. **Factory Method Pattern:**
   - Purpose: Defines an interface for creating an object but lets subclasses alter the type of objects that will be created.
   - Example: A document creation application where you have different document types like PDF and Word. Factory methods create these documents.

   ```csharp
   public abstract class Document
   {
       public abstract void CreateDocument();
   }
   
   public class PDFDocument : Document
   {
       public override void CreateDocument()
       {
           // Create a PDF document
       }
   }
   
   public class WordDocument : Document
   {
       public override void CreateDocument()
       {
           // Create a Word document
       }
   }
   ```

3. **Abstract Factory Pattern:**
   - Purpose: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
   - Example: A UI toolkit that provides platform-specific UI elements like buttons and windows for Windows, macOS, and Linux.

   ```csharp
   public abstract class Button { }
   public abstract class Window { }
   
   public abstract class UIFactory
   {
       public abstract Button CreateButton();
       public abstract Window CreateWindow();
   }
   
   public class WindowsFactory : UIFactory
   {
       public override Button CreateButton()
       {
           return new WindowsButton();
       }
       
       public override Window CreateWindow()
       {
           return new WindowsWindow();
       }
   }
   ```

4. **Builder Pattern:**
   - Purpose: Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.
   - Example: Building a complex document or HTML page step by step.

   ```csharp
   public class DocumentBuilder
   {
       private Document document = new Document();

       public void AddHeader(string text)
       {
           // Add a header to the document
       }

       public void AddBody(string text)
       {
           // Add body content to the document
       }

       public Document Build()
       {
           return document;
       }
   }
   ```

5. **Prototype Pattern:**
   - Purpose: Creates new objects by copying an existing object, known as the prototype.
   - Example: Creating instances of complex objects based on existing instances, like copying an existing database configuration.

   ```csharp
   public class DatabaseConfiguration
   {
       public string ConnectionString { get; set; }
       public string Username { get; set; }
       public string Password { get; set; }

       public DatabaseConfiguration Clone()
       {
           return (DatabaseConfiguration)this.MemberwiseClone();
       }
   }
   ```


### Behavioral Patterns

Behavioral design patterns focus on the communication and interaction between objects and classes. They provide solutions for how objects collaborate and operate together. Here are some of the top behavioral design patterns with examples:

1. **Observer Pattern:**
   - **Purpose:** Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
   - **Example:** Implementing event handling in a graphical user interface or managing subscriptions to a news feed.

   ```csharp
   public interface IObserver
   {
       void Update(string message);
   }

   public class ConcreteObserver : IObserver
   {
       private string name;

       public ConcreteObserver(string name)
       {
           this.name = name;
       }

       public void Update(string message)
       {
           Console.WriteLine($"{name} received the message: {message}");
       }
   }

   public class Subject
   {
       private List<IObserver> observers = new List<IObserver>();

       public void Attach(IObserver observer)
       {
           observers.Add(observer);
       }

       public void Notify(string message)
       {
           foreach (var observer in observers)
           {
               observer.Update(message);
           }
       }
   }
   ```

2. **Strategy Pattern:**
   - **Purpose:** Defines a family of algorithms, encapsulates each one, and makes them interchangeable. It lets the algorithm vary independently from clients that use it.
   - **Example:** Implementing different sorting algorithms (e.g., quicksort, bubblesort) as interchangeable strategies for a sorting algorithm.

   ```csharp
   public interface ISortStrategy
   {
       void Sort(int[] data);
   }

   public class QuickSort : ISortStrategy
   {
       public void Sort(int[] data)
       {
           // Implement quicksort algorithm
       }
   }

   public class BubbleSort : ISortStrategy
   {
       public void Sort(int[] data)
       {
           // Implement bubblesort algorithm
       }
   }

   public class SortContext
   {
       private ISortStrategy strategy;

       public SortContext(ISortStrategy strategy)
       {
           this.strategy = strategy;
       }

       public void SetStrategy(ISortStrategy strategy)
       {
           this.strategy = strategy;
       }

       public void Sort(int[] data)
       {
           strategy.Sort(data);
       }
   }
   ```

3. **Command Pattern:**
   - **Purpose:** Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.
   - **Example:** Implementing a remote control that can execute different commands (e.g., turning on/off devices or adjusting volume).

   ```csharp
   public interface ICommand
   {
       void Execute();
   }

   public class Light
   {
       public void TurnOn() { /* ... */ }
       public void TurnOff() { /* ... */ }
   }

   public class LightOnCommand : ICommand
   {
       private Light light;

       public LightOnCommand(Light light)
       {
           this.light = light;
       }

       public void Execute()
       {
           light.TurnOn();
       }
   }

   public class RemoteControl
   {
       private ICommand command;

       public void SetCommand(ICommand command)
       {
           this.command = command;
       }

       public void PressButton()
       {
           command.Execute();
       }
   }
   ```

4. **Memento Pattern:**
   - **Purpose:** Captures and externalizes an object's internal state so the object can be restored to this state later.
   - **Example:** Creating an "undo" feature in a text editor to revert changes made to a document to previous states.

   ```csharp
   public class Memento
   {
       public string State { get; }

       public Memento(string state)
       {
           State = state;
       }
   }

   public class Originator
   {
       private string state;

       public string State
       {
           get => state;
           set => state = value;
       }

       public Memento CreateMemento()
       {
           return new Memento(state);
       }

       public void RestoreFromMemento(Memento memento)
       {
           state = memento.State;
       }
   }

   public class Caretaker
   {
       public List<Memento> Mementos { get; } = new List<Memento>();
   }
   ```

### Structural Patterns

Structural design patterns focus on simplifying the composition of objects and classes to form larger structures. They help in managing relationships between objects, making it easier to build complex systems while keeping them flexible and efficient. Here are some structural design patterns with examples:

1. **Adapter Pattern:**
   - **Purpose:** Allows the interface of an existing class to be used as another interface.
   - **Example:** Suppose you have a legacy class with a non-standard interface, and you need to adapt it to work with a new system that expects a standard interface. The adapter pattern can bridge the gap.

   ```csharp
   class LegacyRectangle
   {
       public int GetWidth() { /* ... */ }
       public int GetHeight() { /* ... */ }
   }

   interface IShape
   {
       int GetArea();
   }

   class RectangleAdapter : IShape
   {
       private LegacyRectangle adaptee;

       public RectangleAdapter(LegacyRectangle rect)
       {
           adaptee = rect;
       }

       public int GetArea()
       {
           return adaptee.GetWidth() * adaptee.GetHeight();
       }
   }
   ```

2. **Bridge Pattern:**
   - **Purpose:** Separates an object's abstraction from its implementation.
   - **Example:** Consider a shape hierarchy with different drawing engines. The bridge pattern allows you to change the shape's rendering without modifying the shape itself.

   ```csharp
   interface IRenderer
   {
       void Render();
   }

   abstract class Shape
   {
       protected IRenderer renderer;

       public Shape(IRenderer renderer)
       {
           this.renderer = renderer;
       }

       public abstract void Draw();
   }

   class Circle : Shape
   {
       public Circle(IRenderer renderer) : base(renderer) { }

       public override void Draw()
       {
           renderer.Render();
       }
   }
   ```

3. **Composite Pattern:**
   - **Purpose:** Composes objects into tree structures to represent part-whole hierarchies.
   - **Example:** Create a hierarchical structure of components, where both individual objects and compositions of objects are treated uniformly.

   ```csharp
   interface IGraphic
   {
       void Draw();
   }

   class Circle : IGraphic { /* ... */ }
   class Square : IGraphic { /* ... */ }

   class CompositeGraphic : IGraphic
   {
       private List<IGraphic> children = new List<IGraphic>();

       public void Add(IGraphic graphic)
       {
           children.Add(graphic);
       }

       public void Draw()
       {
           foreach (var child in children)
           {
               child.Draw();
           }
       }
   }
   ```

4. **Decorator Pattern:**
   - **Purpose:** Attaches additional responsibilities to an object dynamically.
   - **Example:** Add features to an object at runtime without altering its structure. For instance, adding borders or scrollable behavior to a window in a GUI application.

   ```csharp
   interface IComponent
   {
       void Operation();
   }

   class ConcreteComponent : IComponent
   {
       public void Operation() { /* ... */ }
   }

   abstract class Decorator : IComponent
   {
       protected IComponent component;

       public Decorator(IComponent component)
       {
           this.component = component;
       }

       public virtual void Operation()
       {
           component.Operation();
       }
   }

   class ConcreteDecoratorA : Decorator
   {
       public ConcreteDecoratorA(IComponent component) : base(component) { }

       public override void Operation()
       {
           base.Operation();
           // Additional behavior
       }
   }
   ```

5. **Facade Pattern:**
   - **Purpose:** Provides a simplified interface to a set of interfaces in a subsystem.
   - **Example:** Create a facade that simplifies complex operations or hides the complexity of multiple components. For instance, a video conversion system might have a facade to handle encoding, muxing, and streaming.

   ```csharp
   class VideoConverterFacade
   {
       private VideoEncoder encoder;
       private VideoMuxer muxer;
       private VideoStreamer streamer;

       public VideoConverterFacade()
       {
           encoder = new VideoEncoder();
           muxer = new VideoMuxer();
           streamer = new VideoStreamer();
       }

       public void ConvertAndStream(string videoFilePath)
       {
           Video video = encoder.Encode(videoFilePath);
           Video muxedVideo = muxer.Mux(video);
           streamer.Stream(muxedVideo);
       }
   }
   ```