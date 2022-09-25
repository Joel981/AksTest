#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["AksTest/AksTest.csproj", "AksTest/"]
RUN dotnet restore "AksTest/AksTest.csproj"
COPY . .
WORKDIR "/src/AksTest"
RUN dotnet build "AksTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AksTest.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AksTest.dll"]