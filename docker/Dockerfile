# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy solution file and restore dependencies
COPY ["src/app-two.sln", "src/"]
COPY ["src/app-two/app-two.csproj", "src/app-two/"]
RUN dotnet restore "src/app-two.sln"

# Copy source code and build
COPY . .
WORKDIR "/src"
RUN dotnet build "app-two.sln" -c Release -o /app/build

# Publish stage
FROM build AS publish
WORKDIR "/src"
RUN dotnet publish "app-two/app-two.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .

# Set environment variables
ENV ASPNETCORE_URLS=http://+:80

EXPOSE 80

ENTRYPOINT ["dotnet", "app-two.dll"]