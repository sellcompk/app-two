# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy project file and restore dependencies
COPY ["src/app-two/app-two.csproj", "src/app-two/"]
RUN dotnet restore "src/app-two/app-two.csproj"

# Copy source code and build
COPY . .
WORKDIR "/src/app-two"
RUN dotnet build "app-two.csproj" -c Release -o /app/build

# Publish stage
FROM build AS publish
RUN dotnet publish "app-two.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .

# Set environment variables
ENV ASPNETCORE_URLS=http://+:80

EXPOSE 80

ENTRYPOINT ["dotnet", "app-two.dll"]