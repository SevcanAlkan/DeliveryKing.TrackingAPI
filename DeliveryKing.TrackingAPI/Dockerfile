#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DeliveryKing.TrackingAPI/DeliveryKing.TrackingAPI.csproj", "DeliveryKing.TrackingAPI/"]
RUN dotnet restore "DeliveryKing.TrackingAPI/DeliveryKing.TrackingAPI.csproj"
COPY . .
WORKDIR "/src/DeliveryKing.TrackingAPI"
RUN dotnet build "DeliveryKing.TrackingAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DeliveryKing.TrackingAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DeliveryKing.TrackingAPI.dll"]