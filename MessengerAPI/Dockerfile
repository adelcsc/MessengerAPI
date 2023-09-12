FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["MessengerAPI/MessengerAPI.csproj", "MessengerAPI/"]
RUN dotnet restore "MessengerAPI/MessengerAPI.csproj"
COPY . .
WORKDIR "/src/MessengerAPI"
RUN dotnet build "MessengerAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MessengerAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MessengerAPI.dll"]
