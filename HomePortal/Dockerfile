#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["HomePortal/HomePortal.csproj", "HomePortal/"]
RUN dotnet restore "HomePortal/HomePortal.csproj"
COPY . .
WORKDIR "/src/HomePortal"
RUN dotnet build "HomePortal.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HomePortal.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HomePortal.dll"]