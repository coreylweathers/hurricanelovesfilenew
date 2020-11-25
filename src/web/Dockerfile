FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY web.csproj .
RUN dotnet restore "web.csproj"
COPY . .
RUN dotnet build "web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "web.csproj" -c Release -o /app/publish

FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/web/dist .
COPY nginx.conf /etc/nginx/nginx.conf