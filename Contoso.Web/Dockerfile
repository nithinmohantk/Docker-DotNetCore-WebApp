FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY Contoso.Web/Contoso.Web.csproj Contoso.Web/
RUN dotnet restore Contoso.Web/Contoso.Web.csproj
COPY . .
WORKDIR /src/Contoso.Web
RUN dotnet build Contoso.Web.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Contoso.Web.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Contoso.Web.dll"]
