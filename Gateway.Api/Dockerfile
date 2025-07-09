# Etapa 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copia o arquivo .csproj e restaura as dependências
COPY Gateway.Api/API/API.csproj ./API/
RUN dotnet restore ./API/API.csproj

# Copia o restante do código da aplicação
COPY Gateway.Api/API/. ./API/
WORKDIR /src/API
RUN dotnet publish -c Release -o /app/publish

# Etapa 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

# Expõe a porta da aplicação
EXPOSE 8080
ENTRYPOINT ["dotnet", "API.dll"]
