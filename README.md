- [Microsoft Blazor Installation and setup guide (MAC OS - Big Sur 11.4)](#microsoft-blazor-installation-and-setup-guide-mac-os---big-sur-114)
- [Abstraction of a Blazor WebAssembly App to use a Entity Framework App](#abstraction-of-a-blazor-webassembly-app-to-use-a-entity-framework-app)


# Microsoft Blazor Installation and setup guide (MAC OS - Big Sur 11.4)

- Download and install [VSCode for Mac](https://code.visualstudio.com/download)
- Download and install [.NET Core SDK latest version(5.0)](https://dotnet.microsoft.com/download/dotnet/thank-you/sdk-5.0.301-macos-x64-installer)
- Download and install Docker Desktop for Mac
- Check if `dotnet` successfully installed
- Download and run the MSSQL Server docker image in a container.

    `$ docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=@#^fcIen&*asd" -p 1433:1433 --name mssqlserver -d mcr.microsoft.com/mssql/server`

- Observe from the Docker desktop that the container is running successfully, password policies can be a trouble so choose a password that matches the policy.

- From CLI use the following command to check all the available templates. This should show **blazorserver** and **blazorwasm** should be available.

    `$ dotnet new`

- Install template for unit testing from bUnit

    `dotnet new --install bunit.template`

- Create a solution named Beam and move inside it
     ```
       $ dotnet new sln -o Beam
    
       $ cd Beam
     ```

- Create blazorwasm projects with name Beam. These will be our client components for the application solution

    `$ dotnet new blazorwasm -o Beam.Client`

- Create a global JSON file

    `$ dotnet new globaljson`

- Create a dotnet gitignore file

    `$ dotnet new gitignore`

- Now add Beam.Client project to Beam.sln

    `$ dotnet sln add Beam.Client`

- Now create a tool manifest file

    `$ dotnet new tool-manifest`

- Install dotnet Entity Framework tool, this will get used as DB tool for our project

    `$ dotnet tool install dotnet-ef`

- Now check if dotnet restore, dotnet tool restore and dotnet build are running successfully

    ```
      $ dotnet restore
    
      $ dotnet tool restore
    
      $ dotnet build
    ```

- Now inside the client project, run the client project

    ```
      $ cd Beam.Client
    
      $ dotnet run
    ```

- Open [https://127.0.0.1:5000](https://127.0.0.1:5000/) or [https://127.0.0.1:5001](https://127.0.0.1:5001/) and you should see the following &quot;Hello World&quot; application running

- Now with everything running and set up, create a GitHub repository and connect the remote with the present solution directory, i.e. Beam. Then upload the entire solution to GitHub

    ```
      $ git add ./
    
      $ git commit -m 'Initial Commit';
    
      $ git push origin master
    ```

# Abstraction of a Blazor WebAssembly App to use a Entity Framework App

- Create a new console project under `Beam` folder and move inside it

    `dotnet new console -o Beam.Data`

- Add MSSQL Server package
  
    `dotnet add package Microsoft.EntityFrameworkCore.SqlServer`

- Add the `Beam.data` project into solution from root folder

    `dotnet sln add Beam.Data`

- Add the models in `BeamContext.cs` and a connect class `Configure.cs` in `Beam.Data` project

- Add the EF Core Design and ASP.NET EF Core and Identity packages for `Beam.Data` project

    ```
      $ dotnet add package Microsoft.EntityFrameworkCore.Design
      $ dotnet add package Microsoft.AspNetCore
      $ dotnet add package Microsoft.AspNetCore.Identity
      $ dotnet add package Microsoft.AspNetCore.Identity.EntityFrameWorkCore
    ```

- Create the `Beam.Shared` project as a class library and place all the models there

    `dotnet new classlib -o Beam.Shared`

- Add the `Beam.Shared` project to the solution

    `$ dotnet sln add Beam.Shared`

- Add the dependency of `Beam.Shared` project in `Beam.Server`

    `dotnet add Beam.Server/Beam.Server.csproj reference Beam.Shared/Beam.Shared.csproj`

- Now add all the mapper classes in `Beam.Server/Mappers` folder

- Since our `DbConText` is in `Beam.Data` and we are initializing the connection string in `Beam.Server`, we will need the following command to generate migrations from `Beam.Server` project

    `dotnet ef migrations add InitialCreate --project ../Beam.Data/Beam.Data.csproj --context BeamContext --output-dir ../Beam.Data/Migrations`

- Now run the migrations from `Beam.Server` project

    `dotnet ef database update --project ../Beam.Data/Beam.Data.csproj --context BeamContext`
