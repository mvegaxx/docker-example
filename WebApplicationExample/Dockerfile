# Dockerfile optimizado para aplicaciones Native AOT

# Usamos una imagen base de Debian para la etapa de compilación
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Instalamos las dependencias necesarias para Native AOT
RUN apt-get update && apt-get install -y clang zlib1g-dev

WORKDIR /src
COPY ["WebApplicationExample.csproj", "./"]
RUN dotnet restore "./WebApplicationExample.csproj"
COPY . .

# Compilamos la aplicación con Native AOT
RUN dotnet publish "WebApplicationExample.csproj" -c Release -o /app/publish

# Usamos una imagen base mínima para la etapa final
FROM mcr.microsoft.com/dotnet/runtime-deps:8.0 AS final
WORKDIR /app

# Copiamos los archivos publicados
COPY --from=build /app/publish .

# Configuramos los puertos
EXPOSE 8080
EXPOSE 8081

# Configuramos el usuario no-root
USER $APP_UID

# El punto de entrada es el ejecutable nativo generado
ENTRYPOINT ["./WebApplicationExample"]
