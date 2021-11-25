#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Esdc.Ccoe.CI.WebApi.Demo/Esdc.Ccoe.CI.WebApi.Demo.csproj", "Esdc.Ccoe.CI.WebApi.Demo/"]
RUN dotnet restore "Esdc.Ccoe.CI.WebApi.Demo/Esdc.Ccoe.CI.WebApi.Demo.csproj"
COPY . .
WORKDIR "/src/Esdc.Ccoe.CI.WebApi.Demo"
RUN dotnet build "Esdc.Ccoe.CI.WebApi.Demo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Esdc.Ccoe.CI.WebApi.Demo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Esdc.Ccoe.CI.WebApi.Demo.dll"]