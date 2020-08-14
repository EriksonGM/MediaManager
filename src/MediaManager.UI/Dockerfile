#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["src/MediaManager.UI/MediaManager.UI.csproj", "src/MediaManager.UI/"]
RUN dotnet restore "src/MediaManager.UI/MediaManager.UI.csproj"
COPY . .
WORKDIR "/src/src/MediaManager.UI"
RUN dotnet build "MediaManager.UI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MediaManager.UI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MediaManager.UI.dll"]