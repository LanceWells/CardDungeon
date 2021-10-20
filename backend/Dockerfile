FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["CardDungeon/CardDungeon.csproj", "CardDungeon/"]
RUN dotnet restore "CardDungeon/CardDungeon.csproj"
COPY . .
WORKDIR "/src/CardDungeon"
RUN dotnet build "CardDungeon.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CardDungeon.csproj" -c Release -o /app/publish

FROM base AS final
ENV ASPNETCORE_URLS: http://+:80
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CardDungeon.dll"]
