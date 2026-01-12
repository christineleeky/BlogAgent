FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["BlogAgent/BlogAgent.csproj", "BlogAgent/"]
COPY ["../BlogAgent.Domain/BlogAgent.Domain.csproj", "../BlogAgent.Domain/"]
RUN dotnet restore "BlogAgent.csproj"
COPY . .
WORKDIR "/src/BlogAgent"
RUN dotnet build "BlogAgent.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlogAgent.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlogAgent.dll"]
