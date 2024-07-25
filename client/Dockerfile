# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["client/client.csproj", "client/"]
RUN dotnet restore "client/client.csproj"
COPY . .
WORKDIR "/src/client"
RUN dotnet publish "client.csproj" -c Release -o /app/publish

# Final stage
FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
COPY --from=build /app/publish/wwwroot .
COPY ["client/nginx.conf", "/etc/nginx/nginx.conf"]
EXPOSE 8080
ENTRYPOINT ["nginx", "-g", "daemon off;"]



