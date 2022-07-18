# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /source

# Copy csproj and restore as distinct layers
COPY ["MvcDocker.Api/MvcDocker.Api.csproj", "MvcDocker.Api/"]
COPY . .
RUN dotnet restore

# Copy everything else and build
COPY MvcDocker.Api/. ./MvcDocker.Api/
WORKDIR /source/MvcDocker.Api/ 
RUN dotnet publish "./MvcDocker.Api.csproj" -c release -o /app 

# final stage/image'
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "MvcDocker.Api.dll"]