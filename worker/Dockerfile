# =========================
# Build Stage
# =========================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /src

# Copy csproj and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy remaining source code
COPY . ./

# Publish application
RUN dotnet publish -c Release -o /app/publish

# =========================
# Runtime Stage
# =========================
FROM mcr.microsoft.com/dotnet/runtime:8.0

WORKDIR /app

# Copy published files from build stage
COPY --from=build /app/publish .

# Run worker application
ENTRYPOINT ["dotnet", "Worker.dll"]