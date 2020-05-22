#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/runtime:2.2-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Sample-RequestResponse/Sample-RequestResponse.csproj", "Sample-RequestResponse/"]
COPY ["MessageContracts/MessageContracts.csproj", "MessageContracts/"]
RUN dotnet restore "Sample-RequestResponse/Sample-RequestResponse.csproj"
COPY . .
WORKDIR "/src/Sample-RequestResponse"
RUN dotnet build "Sample-RequestResponse.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Sample-RequestResponse.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Sample-RequestResponse.dll"]