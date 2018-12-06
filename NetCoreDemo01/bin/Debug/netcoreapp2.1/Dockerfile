FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 55411
EXPOSE 44377

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY NetCoreDemo01/NetCoreDemo01.csproj NetCoreDemo01/
RUN dotnet restore NetCoreDemo01/NetCoreDemo01.csproj
COPY . .
WORKDIR /src/NetCoreDemo01
RUN dotnet build NetCoreDemo01.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish NetCoreDemo01.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreDemo01.dll"]
