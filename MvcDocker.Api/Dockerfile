# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /source

# Copy csproj and restore as distinct layers
COPY ["MvcDocker.Api/MvcDocker.Api.csproj", "MvcDocker.Api/"]
COPY . .
RUN dotnet restore

# Copy everything else and build
COPY MvcDocker.Api/. ./MvcDocker.Api/
WORKDIR /source/MvcDocker.Api/
RUN dotnet publish "MvcDocker.Api/MvcDocker.Api.csproj" -c release -o /app -r  --no-restore

# final stage/image
FROM mcr.microsoft.com/dotnet/runtime:6.0
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "MvcDocker.dll"]