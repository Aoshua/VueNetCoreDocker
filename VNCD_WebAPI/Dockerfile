#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["VNCD_WebAPI/VNCD_WebAPI.csproj", "VNCD_WebAPI/"]
RUN dotnet restore "VNCD_WebAPI/VNCD_WebAPI.csproj"
COPY . .
WORKDIR "/src/VNCD_WebAPI"
RUN dotnet build "VNCD_WebAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "VNCD_WebAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VNCD_WebAPI.dll"]