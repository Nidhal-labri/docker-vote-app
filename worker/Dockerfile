FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /app

# Copy only the necessary files first to leverage Docker caching
COPY src/Worker/*.csproj src/Worker/
WORKDIR /app/src/Worker
RUN dotnet restore

# Copy the rest of the source code
COPY src/ /app/src/

# Build and publish the application
RUN dotnet publish -c Release -o /app/out

# Use a smaller runtime image for final execution
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out .

CMD ["dotnet", "Worker.dll"]

