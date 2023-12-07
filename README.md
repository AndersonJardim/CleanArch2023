# CleanArch2023

 Resumo documentado do meu modo de montar meu ambiente em **Clean Arch em .NET 5**.0, memso tendo as versões 6, 7 e 8. Mas que pode ser atualizado, com pouco esforço.

<h1 align="center">
    <img src="./public/dotnet.jpg" width="300"/>
</h1>

## 💻 Verificações de SDKs instaladas, mas usei a 5
```bash
dotnet --list-sdks
3.1.426 [C:\Program Files\dotnet\sdk]
5.0.416 [C:\Program Files\dotnet\sdk]
6.0.100 [C:\Program Files\dotnet\sdk]
7.0.100 [C:\Program Files\dotnet\sdk]
7.0.101 [C:\Program Files\dotnet\sdk]
7.0.102 [C:\Program Files\dotnet\sdk]
7.0.404 [C:\Program Files\dotnet\sdk]
8.0.100 [C:\Program Files\dotnet\sdk]

dotnet --version
8.0.100
```

## 🚀 Passo 1: Preparando o ambiente
```bash
dotnet new gitignore
touch README.md
code .
```

## Passo 2.1: Criando a solução (Blank Solution)
```bash
dotnet new sln --name CleanArch
```

## Passo 2.2: Criando os primeiros 4 projetos (Class Library - .NET Core)
```bash
dotnet new classlib --name CleanArch.Domain -f net5.0
dotnet new classlib --name CleanArch.Application -f net5.0
dotnet new classlib --name CleanArch.Infra.Data -f net5.0
dotnet new classlib --name CleanArch.Infra.IoC -f net5.0
```

## Em seguida será o MVC: dotnet new mvc --name CleanArch.WebUI -f net5.0

## Passo 2.3: Criando o projeto 5 em MVC (ASP.NET Core Web Application - ASP.NET Core 5.0)
Usando o Visual Studio 2019: ASP.NET Core: ASP.NET Core Web App(Model-View-Controller)<br />
Deveria marcar a opçao avancada  - Configure HTTPS<br />
Para esse projeto foi habilitado o Razor runtime compilation<br />
```bash
dotnet new mvc --name CleanArch.WebUI -f net5.0
```

## Passo 2.4: Adicionado os projetos na solucão

### Resumo do passo 2.4
Domain - Não depende de nenhum.<br />
Application - Dependêcia com o projeto: Domain<br />
Infra.Data - Dependêcia com o projeto: Domain<br />
Infra.IoC - Dependêcia com o projeto: Domain, Application, Infra.Data<br />
WebUI - Dependêcia com o projeto: Infra.IoC<br />

## Opção 1:
```bash
dotnet sln add CleanArch.Domain/CleanArch.Domain.csproj
dotnet sln add CleanArch.Infra.Data/CleanArch.Infra.Data.csproj
dotnet sln add CleanArch.Infra.IoC/CleanArch.Infra.IoC.csproj
```
## Opção 2:
```bash
dotnet sln CleanArch.sln add CleanArch.Domain/CleanArch.Domain.csproj
dotnet sln CleanArch.sln add CleanArch.Infra.Data/CleanArch.Infra.Data.csproj
dotnet sln CleanArch.sln add CleanArch.Infra.IoC/CleanArch.Infra.IoC.csproj
```

### Passo 2.5: Adicionado Referências
### Passo 2.5.1 # Adicionado Referências na camada Application, referencie a camada Domain
```bash
dotnet add CleanArch.Application/CleanArch.Application.csproj reference CleanArch.Domain/CleanArch.Domain.csproj
```

### Passo 2.5.2 # Adicionado Referências na camada Infra.Data, referencie a camada Domain
```bash
dotnet add CleanArch.Infra.Data/CleanArch.Infra.Data.csproj reference CleanArch.Domain/CleanArch.Domain.csproj
```

### Passo 2.5.3 # Adicionado Referências na camada Infra.IoC, referencie as camadas Application e Infra.Data
```bash
dotnet add CleanArch.Infra.IoC/CleanArch.Infra.IoC.csproj reference CleanArch.Domain/CleanArch.Domain.csproj
dotnet add CleanArch.Infra.IoC/CleanArch.Infra.IoC.csproj reference CleanArch.Application/CleanArch.Application.csproj
dotnet add CleanArch.Infra.IoC/CleanArch.Infra.IoC.csproj reference CleanArch.Infra.Data/CleanArch.Infra.Data.csproj
```

### Passo 2.5.4 # Adicionado Referências na camada WebIU, referencie a camada Infra.IoC
```bash
dotnet add CleanArch.WebIU/CleanArch.WebIU.csproj reference CleanArch.Infra.IoC/CleanArch.Infra.IoC.csproj
```

## Executando direto na pasta inicial
```bash
cls
dotnet restore
dotnet build
dotnet run --project .\CleanArch.WebUI\CleanArch.WebUI.csproj
```

Este projeto está em constantes melhorias.<br />
Anderson Jardim

## Minhas Redes

Meu site: [anderson-jardim](https://www.linkedin.com/in/anderson-jardim/) &nbsp;&middot;&nbsp; 

Github: [@AndersonJardim](https://github.com/AndersonJardim) &nbsp;&middot;&nbsp;
