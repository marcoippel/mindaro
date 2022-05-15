FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["app.csproj", "."]
RUN dotnet restore "app.csproj"
COPY . .
RUN dotnet build "app.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "app.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "app.dll"]