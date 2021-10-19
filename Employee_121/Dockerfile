#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["Employee_121/Employee_121.csproj", "Employee_121/"]
RUN dotnet restore "Employee_121/Employee_121.csproj"
COPY . .
WORKDIR "/src/Employee_121"
RUN dotnet build "Employee_121.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Employee_121.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Employee_121.dll"]