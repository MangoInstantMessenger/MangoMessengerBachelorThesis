
# Mango Messenger Diploma Thesis

![Build](https://img.shields.io/badge/Build-succeeded-brightgreen)
[![SDK](https://img.shields.io/badge/SDK-.NET%20Core%205.0-blue)](https://dotnet.microsoft.com/download/dotnet/5.0)
[![Trello board](https://img.shields.io/badge/Task%20Board-Trello-green)](https://trello.com/b/5kdQBsYE/bachelor-thesis-trello)
[![Mango Data Base Diagramm](https://img.shields.io/badge/Data%20Base%20Diagram-DbDiagram-lightgrey)](https://dbdiagram.io/d/60d66a13dd6a597148203e6b) 
[![Contributors](https://img.shields.io/badge/Contributors-2-red)](https://github.com/kolosovpetro/MangoAPI/graphs/contributors)
[![ORM](https://img.shields.io/badge/ORM-EF%20Core%20-yellow)](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore/5.0.7?_src=template)
[![DBMS](https://img.shields.io/badge/DBMS-PostgreSQL-blue)](https://www.postgresql.org/)
[![Heroku](https://img.shields.io/badge/Deploy-Heroku-green)](https://mango-messenger-app.herokuapp.com/swagger/)



## Build
- Install MikTeX (https://miktex.org/download)
- Update MikTeX
- Install SumatraPDF viewer (https://www.sumatrapdfreader.org/download-free-pdf-viewer)
- Install Intellij IDEA Ultimate (https://www.jetbrains.com/idea/download/#section=windows)
- Activate Intellij IDEA Ultimate, you should have student license
- Install TeXiFy IDEA plugin (https://plugins.jetbrains.com/plugin/9473-texify-idea)
- Clone this repository locally: git clone https://github.com/kolosovpetro/BachelorsThesis.git
- Open diploma-document.iml in IDEA
- Configure Inverse Search in IDEA for SumatraPDF, Tool -> LaTeX -> Configure Inverse Search
- Compile it, Shift + F10

## Links
- Figma: https://www.figma.com/file/cGtLvO1JuJgWmnzaSbM8Re/Mango-Thesis-Screens

## Git flow
- Each task is assigned a number (THESIS-ID)
- Tasks are at Trello board https://trello.com/b/5kdQBsYE/bachelor-thesis-trello
- There are two main branches: master, develop
- Develop will be merged with master when diploma will be ready
- In order to contribute:
  - Clone this repo locally, or pull last changes fropm develop
  - Create new branch, based on develop, name it as task ID, e.g MANGO-ID
  - Solve the task
  - Create pull request to develop

## Planed Technologies

- SDK: **[.NET Core 5.0](https://dotnet.microsoft.com/download/dotnet/5.0)**

- ORM: **[Entity Framework Core 5.0.7](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore/5.0.7?_src=template)**

- SQL Database: **[PostgreSQL 13](https://www.postgresql.org/)**

- EF Core for PostgreSQL Provider: **[Npgsql.EntityFrameworkCore.PostgreSQL 5.0.7](https://www.nuget.org/packages/Npgsql.EntityFrameworkCore.PostgreSQL/5.0.7?_src=template)**

- CI: **[GitHub Actions](https://docs.github.com/en/actions)**

- Mediator pattern library: **[MediatR 9.0.0](https://www.nuget.org/packages/MediatR/9.0.0?_src=template)**

- Validation library: **[Fluent Validation](https://www.nuget.org/packages/FluentValidation/10.2.3?_src=template)**

- JWT library: **[System JWT 6.8.0](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt)**

- JWT auxiliary library: **[System Tokens 6.11.1](https://www.nuget.org/packages/System.IdentityModel.Tokens)**

- JWT Bearer: **[Microsoft Jwt Bearer](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.JwtBearer/5.0.7?_src=template)**

- Swagger library: **[Swashbuckle 6.1.4](https://www.nuget.org/packages/Swashbuckle.AspNetCore/5.6.3?_src=template)**
