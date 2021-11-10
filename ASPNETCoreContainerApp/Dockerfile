#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["ASPNETCoreContainerApp/ASPNETCoreContainerApp.csproj", "ASPNETCoreContainerApp/"]
RUN dotnet restore "ASPNETCoreContainerApp/ASPNETCoreContainerApp.csproj"
COPY . .
WORKDIR "/src/ASPNETCoreContainerApp"
RUN dotnet build "ASPNETCoreContainerApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASPNETCoreContainerApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASPNETCoreContainerApp.dll"]