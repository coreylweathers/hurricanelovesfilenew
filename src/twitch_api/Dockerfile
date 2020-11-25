#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster AS build
WORKDIR /src
COPY ["src/twitch_api/twitch_api.csproj", "src/twitch_api/"]
RUN dotnet restore "src/twitch_api/twitch_api.csproj"
COPY . .
WORKDIR "/src/src/twitch_api"
RUN dotnet build "twitch_api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "twitch_api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "twitch_api.dll"]