# Etapa de compilação e publicação
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /src

# Copia o arquivo do projeto e restaura as dependências
COPY OrbitBoard.Api/OrbitBoard.Api.csproj ./OrbitBoard.Api/
RUN dotnet restore OrbitBoard.Api/OrbitBoard.Api.csproj

# Copia o restante do código
COPY . ./

# Publica o projeto
RUN dotnet publish OrbitBoard.Api/OrbitBoard.Api.csproj \
    --configuration Release \
    --output /app/publish \
    --no-restore \
    /p:UseAppHost=false

# Etapa de execução
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

WORKDIR /app

COPY --from=build /app/publish .

# Define a porta interna da API
ENV ASPNETCORE_URLS=http://+:8080

EXPOSE 8080

ENTRYPOINT ["dotnet", "OrbitBoard.Api.dll"]