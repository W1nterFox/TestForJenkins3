#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 8084
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["WebApplication3Tanya/WebApplication3Tanya.csproj", "WebApplication3Tanya/"]
RUN dotnet restore "WebApplication3Tanya/WebApplication3Tanya.csproj"
COPY . .
WORKDIR "/src/WebApplication3Tanya"
RUN dotnet build "WebApplication3Tanya.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication3Tanya.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication3Tanya.dll"]