FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY DotNetCoreBundle/Contoso.Api.csproj DotNetCoreBundle/
RUN dotnet restore DotNetCoreBundle/Contoso.Api.csproj
COPY . .
WORKDIR /src/DotNetCoreBundle
RUN dotnet build Contoso.Api.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Contoso.Api.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Contoso.Api.dll"]
