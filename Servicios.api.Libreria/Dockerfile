﻿FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["Servicios.api.Libreria/Servicios.api.Libreria.csproj", "Servicios.api.Libreria/"]
RUN dotnet restore "Servicios.api.Libreria/Servicios.api.Libreria.csproj"
COPY . .
WORKDIR "/src/Servicios.api.Libreria"
RUN dotnet build "Servicios.api.Libreria.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "Servicios.api.Libreria.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Servicios.api.Libreria.dll"]
