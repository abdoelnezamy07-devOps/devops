# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS builder
WORKDIR /src
COPY ["worker.csproj", "./"]
RUN dotnet restore
COPY . .
RUN dotnet publish "worker.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Stage 2: Final Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0-alpine
WORKDIR /app
COPY --from=builder --chown=app:app /app/publish .
USER app
# ENV ASPNETCORE_URLS=http://+:8080
# EXPOSE 8080
ENTRYPOINT ["dotnet", "worker.dll"]
