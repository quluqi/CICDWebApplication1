#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["CICDWebApplication1/CICDWebApplication1.csproj", "CICDWebApplication1/"]
RUN dotnet restore "CICDWebApplication1/CICDWebApplication1.csproj"
COPY . .
WORKDIR "/src/CICDWebApplication1"
RUN dotnet build "CICDWebApplication1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CICDWebApplication1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CICDWebApplication1.dll"]