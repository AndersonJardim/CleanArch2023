## Resumo documentado do meu modo de montar meu ambiente em Clean Arch em .NET 5.0, memso tendo as versões 6, 7 e 8
dotnet --list-sdks
3.1.426 [C:\Program Files\dotnet\sdk]
5.0.416 [C:\Program Files\dotnet\sdk]
6.0.100 [C:\Program Files\dotnet\sdk]
7.0.100 [C:\Program Files\dotnet\sdk]
7.0.101 [C:\Program Files\dotnet\sdk]
7.0.102 [C:\Program Files\dotnet\sdk]
7.0.404 [C:\Program Files\dotnet\sdk]
8.0.100 [C:\Program Files\dotnet\sdk]

## Passo 1: Preparando o ambiente
dotnet new gitignore
touch README.md

## Passo 2.1: Criando a solução (Blank Solution)
dotnet new sln --name CleanArch

## Passo 2.2: Criando os primeiros 4 projetos (Class Library - .NET Core)
dotnet new classlib --name CleanArch.Domain -f net5.0
dotnet new classlib --name CleanArch.Application -f net5.0
dotnet new classlib --name CleanArch.Infra.Data -f net5.0
dotnet new classlib --name CleanArch.Infra.IoC -f net5.0

## Em seguida será o MVC: dotnet new mvc --name CleanArch.WebUI -f net5.0

## Passo 2.3: Criando o projeto 5 em MVC (ASP.NET Core Web Application - ASP.NET Core 5.0)
### Usando o Visual Studio 2019: ASP.NET Core: ASP.NET Core Web App(Model-View-Controller)
### Deveria marcar a opçao avancada  - Configure HTTPS
### Para esse projeto foi habilitado o Razor runtime compilation
dotnet new mvc --name CleanArch.WebUI -f net5.0

## Passo 2.4: Adicionado os projetos na solucão
## dotnet sln add CleanArch.Domain/CleanArch.Domain.csproj
## dotnet sln add CleanArch.Infra.Data/CleanArch.Infra.Data.csproj
## dotnet sln add CleanArch.Infra.IoC/CleanArch.Infra.IoC.csproj
## ou
dotnet sln CleanArch.sln add CleanArch.Domain/CleanArch.Domain.csproj
dotnet sln CleanArch.sln add CleanArch.Infra.Data/CleanArch.Infra.Data.csproj
dotnet sln CleanArch.sln add CleanArch.Infra.IoC/CleanArch.Infra.IoC.csproj


