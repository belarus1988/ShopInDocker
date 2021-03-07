#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 81
ENV ASPNETCORE_URLS=http://*:81

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["ShopApi.csproj", ""]
RUN dotnet restore "./ShopApi.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "ShopApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ShopApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ShopApi.dll"]