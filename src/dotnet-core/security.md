# .NET Core Security

.NET Core provides flexibility to support authentication, authorization in varying ways
1. Custom setup including middleware based authentication
   Custom setup is required when you want to use custom authentication scheme or custom authorization logic or both. 
    This is the most flexible approach but requires more work.
    You can realize this approach by using middleware based authentication and authorization. 

2. Microsoft identity
    Microsoft identity is a framework for managing user identities. It enables authentication and authorization for your apps. It also provides a framework for handling user accounts that supports account confirmation, password reset, and more.


3. External Auth2 providers
    External authentication providers are services that authenticate users for you. They include Google, Facebook, Twitter, and more. They're often referred to as social logins.



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


## Json Web Tokens (JWT)

Json Web Tokens (JWT) are an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA.

## Cookies



## Refresh Tokens

Refresh tokens are credentials used to obtain access tokens. Refresh tokens are issued to the client by the authorization server and are used to obtain a new access token when the current access token becomes invalid or expires, or to obtain additional access tokens with identical or narrower scope (access tokens may have a shorter lifetime and fewer permissions than authorized by the resource owner). Issuing a refresh token is optional at the discretion of the authorization server.
