FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Contoso.Web/Contoso.Web.csproj", "Contoso.Web/"]
RUN dotnet restore "Contoso.Web/Contoso.Web.csproj"
COPY . .
WORKDIR "/src/Contoso.Web"
RUN dotnet build "Contoso.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Contoso.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Contoso.Web.dll"]