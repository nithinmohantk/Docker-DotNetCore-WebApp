FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY Contoso.Api/Contoso.Api.csproj Contoso.Api/
RUN dotnet restore Contoso.Api/Contoso.Api.csproj
COPY . .
WORKDIR /src/Contoso.Api
RUN dotnet build Contoso.Api.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Contoso.Api.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Contoso.Api.dll"]
