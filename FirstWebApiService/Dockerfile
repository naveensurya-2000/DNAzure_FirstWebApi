#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
#WORKDIR /src
#COPY ["FirstWebApiService/FirstWebApiService.csproj", "FirstWebApiService/"]
#RUN dotnet restore "FirstWebApiService/FirstWebApiService.csproj"
#COPY . .
#WORKDIR "/src/FirstWebApiService"
#RUN dotnet build "FirstWebApiService.csproj" -c Release -o /app/build
#
#FROM build AS publish
#RUN dotnet publish "FirstWebApiService.csproj" -c Release -o /app/publish
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "FirstWebApiService.dll"]

# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app



# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore
# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out



# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "FirstWebApiService.dll"]