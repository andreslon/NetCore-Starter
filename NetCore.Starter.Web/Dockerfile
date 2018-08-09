FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 47966
EXPOSE 44392

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY NetCore.Starter.Web/NetCore.Starter.Web.csproj NetCore.Starter.Web/
RUN dotnet restore NetCore.Starter.Web/NetCore.Starter.Web.csproj
COPY . .
WORKDIR /src/NetCore.Starter.Web
RUN dotnet build NetCore.Starter.Web.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish NetCore.Starter.Web.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCore.Starter.Web.dll"]
