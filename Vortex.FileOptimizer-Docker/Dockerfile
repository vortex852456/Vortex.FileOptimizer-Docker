FROM mcr.microsoft.com/dotnet/core/runtime:3.0-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Vortex.FileOptimizer-Docker/Vortex.FileOptimizer-Docker.csproj", "Vortex.FileOptimizer-Docker/"]
RUN dotnet restore "Vortex.FileOptimizer-Docker/Vortex.FileOptimizer-Docker.csproj"
COPY . .
WORKDIR "/src/Vortex.FileOptimizer-Docker"
RUN dotnet build "Vortex.FileOptimizer-Docker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Vortex.FileOptimizer-Docker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Vortex.FileOptimizer-Docker.dll"]