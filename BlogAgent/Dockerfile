FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Copy everything first to ensure references are preserved
COPY . .
RUN dotnet restore "BlogAgent/BlogAgent.csproj"

WORKDIR "/src/BlogAgent"
# We add --no-restore because we already did it above
RUN dotnet build "BlogAgent.csproj" -c Release -o /app/build --no-restore

FROM build AS publish
RUN dotnet publish "BlogAgent.csproj" -c Release -o /app/publish --no-restore

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlogAgent.dll"]