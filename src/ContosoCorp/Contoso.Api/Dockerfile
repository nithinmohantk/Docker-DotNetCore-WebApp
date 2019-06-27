FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Contoso.Api/Contoso.Api.csproj", "Contoso.Api/"]
RUN dotnet restore "Contoso.Api/Contoso.Api.csproj"
COPY . .
WORKDIR "/src/Contoso.Api"
RUN dotnet build "Contoso.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Contoso.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Contoso.Api.dll"]