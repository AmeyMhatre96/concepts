# .NET Core Security

## Microsoft Identity

Microsoft Identity is a framework for managing user identities. It enables authentication and authorization for your apps. It also provides a framework for handling user accounts that supports account confirmation, password reset, and more.

Microsoft Identity is built on top of ASP.NET Core Identity. It's a set of libraries that can be used to add authentication and authorization to your apps. It's also a set of services that can be used to manage user accounts.

#### Packages
- Microsoft.AspNetCore.Identity
- Microsoft.AspNetCore.Identity.EntityFrameworkCore

#### Setting up user management in ASP.NET Core

1. Install the Microsoft.AspNetCore.Identity and Microsoft.AspNetCore.Identity.EntityFrameworkCore packages. 

>These pacakges are pre-installed in ASP.NET 5.0+ projects as part of shared framework

2. Add user entities
    
    ```csharp
    public class ApplicationUser : IdentityUser
    {
        public string FirstName { get; set; }
        public string LastName { get; set; }
    }
    ```
3. Add DbContext

    ```csharp
    public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }
    }
    ```

4. Add services to the DI container

    ```csharp
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(
            Configuration.GetConnectionString("DefaultConnection")));

    services.AddIdentityCore<ApplicationUser>(options => options.SignIn.RequireConfirmedAccount = true)
        .AddEntityFrameworkStores<ApplicationDbContext>();
        .AddSignInManager<SignInManager<ApplicationUser>>();

    services.AddAuthentication();
    services.AddAuthorization();
    ```

5. Add user management controller
    ```csharp
    // Finding user by email
    var user = await _userManager.FindByEmailAsync(Input.Email);

    // Creating user'
    var user = new ApplicationUser { UserName = Input.Email, Email = Input.Email };
    var result = await _userManager.CreateAsync(user, Input.Password);

    // Signing in user
    var result = await _signInManager.PasswordSignInAsync(Input.Email, Input.Password, Input.RememberMe, lockoutOnFailure: false);
     ```          



## Authentication


## Authorization

