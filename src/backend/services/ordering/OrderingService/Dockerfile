FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src
COPY src/backend/services/ordering/OrderingService/ ./app/
WORKDIR /src/app
RUN dotnet restore
RUN dotnet publish -c Release -o /out

FROM mcr.microsoft.com/dotnet/aspnet:10.0
WORKDIR /app
COPY --from=build /out .
EXPOSE 5002
ENTRYPOINT ["dotnet", "OrderingService.dll"]
