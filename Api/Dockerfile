FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["EventSourcingExample/EventSourcingExample.csproj", "EventSourcingExample/"]
RUN dotnet restore "EventSourcingExample/EventSourcingExample.csproj"
COPY . .
WORKDIR "/src/EventSourcingExample"
RUN dotnet build "EventSourcingExample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EventSourcingExample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EventSourcingExample.dll"]
