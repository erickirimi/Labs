FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Api_gateway/Api_gateway.csproj", "Api_gateway/"]
RUN dotnet restore "Api_gateway/Api_gateway.csproj"
COPY . .
WORKDIR "/src/Api_gateway"
RUN dotnet build "Api_gateway.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Api_gateway.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Api_gateway.dll"]