FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Project/Project.csproj", "Project/"]
RUN dotnet restore "Project/Project.csproj"
COPY . .
WORKDIR "/src/Project"
RUN dotnet build "Project.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Project.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Project.dll"]