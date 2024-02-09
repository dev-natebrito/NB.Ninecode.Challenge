FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["NB.Ninecode.Challenge.Api/NB.Ninecode.Challenge.Api.csproj", "NB.Ninecode.Challenge.Api/"]
RUN dotnet restore "NB.Ninecode.Challenge.Api/NB.Ninecode.Challenge.Api.csproj"
COPY . .
WORKDIR "/src/NB.Ninecode.Challenge.Api"
RUN dotnet build "NB.Ninecode.Challenge.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NB.Ninecode.Challenge.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NB.Ninecode.Challenge.Api.dll"]
