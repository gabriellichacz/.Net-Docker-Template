# Use the official .NET SDK image for building the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy only the .csproj file(s) first for caching
COPY ../App/*.csproj ./

# Restore dependencies
RUN dotnet restore

# Copy the rest of the application files
COPY ../App/ ./

# Copy appsettings.json and any other configuration files (if necessary)
COPY ../App/appsettings.json ./appsettings.json
COPY ../App/appsettings.Development.json ./appsettings.Development.json

# Build the application
RUN dotnet publish -c Release -o /publish

# Use the official .NET runtime image for running the application
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Update package list and install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libssl-dev \
    libicu-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libzip-dev \
    libonig-dev \
    zip \
    unzip \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Copy the published application from the build stage
COPY --from=build /publish .

# Copy the entrypoint script
COPY ./deploy/entrypoint.sh /app/entrypoint.sh
RUN chmod +x /app/entrypoint.sh

# Expose the application port
EXPOSE 5028

# Set the entry point
ENTRYPOINT ["dotnet", "App.dll"]