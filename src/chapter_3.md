# .NET Core

The primary differences between .NET Framework and .NET Core (which has evolved into .NET 5.0 and later .NET 6.0 and beyond) are as follows:

**Deployment:**

- **.NET Framework:**
  - Deployment typically involves installing the required version of the .NET Framework on the target machine. Applications are framework-dependent.
  - .NET Framework applications are usually deployed as Windows applications or web applications on IIS.

- **.NET Core:**
  - .NET Core offers more flexibility in deployment. You can choose between framework-dependent, self-contained, and native deployments.
  - Self-contained deployments bundle the necessary runtime, making the application independent of the target system.

**Containerization:**

- **.NET Framework:**
  - .NET Framework applications can be containerized, but they are larger and less suited for containerization due to their dependencies on the installed framework.

- **.NET Core:**
  - .NET Core is well-suited for containerization. Its lightweight nature and support for self-contained deployments make it a popular choice for containerized applications.

**Development experience:**

- **.NET Framework:**
  - .NET Framework development primarily uses Visual Studio and other IDEs like Visual Studio Code. Language servers like OmniSharp are less common.
  - Project structure and build is tied to visual studio and msbuild.

- **.NET Core:**
  - .NET Core development is supported in various editors including Visual Studio, Visual Studio Code, and JetBrains Rider. Language servers like OmniSharp provide code analysis and IntelliSense.
  - comes with cli sdk to manage projects and builds

**Performance:**

- **Kestrel:**
  - Kestrel is a lightweight and high-performance web server used in ASP.NET Core. It's designed for scalability and performance.

- **Language Enhancements:**
  - .NET Core includes various language enhancements and new performance-oriented abstractions, making it more efficient in terms of memory and CPU usage.

- **Native AOT (Ahead-of-Time Compilation):**
  - .NET Core offers the option for Ahead-of-Time compilation, improving startup performance and reducing memory usage.

**Modular:**

- **.NET Framework:**
  - .NET Framework is less modular, and it relies more on built-in components. Extending or customizing the framework often involves extensive configuration in XML files.

- **.NET Core:**
  - .NET Core emphasizes modularity, and many components like configuration, logging, and Web API are added or removed through NuGet packages. This allows developers to create more tailored and lightweight applications.

In summary, .NET Core offers advantages in terms of deployment flexibility, containerization support, editors and language servers, performance enhancements, and modularity when compared to the traditional .NET Framework. These factors have contributed to the popularity and adoption of .NET Core and its successor, .NET 5 and beyond, for modern application development.


### Nuget Package management
NuGet is a package manager for .NET that allows you to manage and consume libraries and dependencies in your .NET projects. The two main approaches to managing NuGet packages are "PackageReference" and "packages.config." Here's a comparison of these two methods:

**PackageReference**:

1. **csproj Integration**: PackageReference is the newer and recommended way of managing NuGet packages in .NET projects. It integrates directly into the project's `.csproj` file, making it part of the project's configuration.

2. **Concise and Modern**: PackageReference simplifies the project file by eliminating the need for a separate `packages.config` file. All package references are defined in the `.csproj` file, making it more concise and modern.

3. **Transitive Dependencies**: PackageReference handles transitive dependencies automatically. When you reference a package, it also brings in its dependencies, simplifying dependency management.

4. **NuGet Restore**: NuGet packages are restored during the build process, which means you don't need to run a separate `nuget restore` command.

5. **Version Range Support**: You can specify version ranges for packages, allowing you to receive updates within a certain range while maintaining compatibility.

6. **Support for SDK-Style Projects**: PackageReference is fully compatible with SDK-style projects, which are the recommended project format in modern .NET development.

**packages.config**:

1. **Legacy Approach**: packages.config is the older and now considered a legacy approach to managing NuGet packages.

2. **Separate XML File**: It uses a separate XML file, usually named `packages.config`, to list the packages and their versions.

3. **Explicit References**: In packages.config, you explicitly specify each package and version, which can make the file larger and harder to manage as the number of dependencies grows.

4. **Transitive Dependencies**: In this approach, you must explicitly include all the dependencies you need, including transitive ones, which can be more cumbersome.

5. **NuGet Restore**: To restore packages, you need to run a separate `nuget restore` command before building your project.

6. **Common in Older Projects**: packages.config is commonly found in older projects created with older versions of Visual Studio and .NET. It's less common in newer projects.

In summary, PackageReference is the recommended and more modern way to manage NuGet packages in .NET projects. It offers better integration, automatic handling of transitive dependencies, and a cleaner project file. packages.config is still supported but is considered a legacy approach and is mainly used in older projects. If you're starting a new project or migrating an existing one to a more modern .NET environment, it's advisable to use PackageReference.

