
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /src

COPY Lab04.Api/Lab04.Api.csproj Lab04.Api/

RUN dotnet restore Lab04.Api/Lab04.Api.csproj


COPY . .

WORKDIR /src/Lab04.Api 

RUN dotnet publish -c Release -o /app/publish



FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

WORKDIR /app

COPY --from=build /app/publish .

EXPOSE 8080

ENTRYPOINT ["dotnet", "Lab04.Api.dll"]