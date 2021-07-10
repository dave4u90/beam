- [Microsoft Blazor Installation and setup guide](#microsoft-blazor-installation-and-setup-guide)


# Microsoft Blazor Installation and setup guide

- Download and install [VSCode for Mac](https://code.visualstudio.com/download)
- Download and install [.NET Core SDK latest version(5.0)](https://dotnet.microsoft.com/download/dotnet/thank-you/sdk-5.0.301-macos-x64-installer)
- Download and install Docker Desktop for Mac
- Check if `dotnet` successfully installed
- Download and run the MSSQL Server docker image in a container.

    `$ docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=@#^fcIen&*asd" -p 1433:1433 --name mssqlserver -d mcr.microsoft.com/mssql/server`

- Observe from the Docker desktop that the container is running successfully, password policies can be a trouble so choose a password that matches the policy.

- From CLI use the following command to check all the available templates. This should show **blazorserver** and **blazorwasm** should be available.

    `$ dotnet new`

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
