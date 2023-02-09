FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["mslearn-improve-api-developer-experience-with-swagge/mslearn-improve-api-developer-experience-with-swagge.csproj", "mslearn-improve-api-developer-experience-with-swagge/"]
RUN dotnet restore "mslearn-improve-api-developer-experience-with-swagge/mslearn-improve-api-developer-experience-with-swagge.csproj"
COPY . .
WORKDIR "/src/mslearn-improve-api-developer-experience-with-swagge"
RUN dotnet build "mslearn-improve-api-developer-experience-with-swagge.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "mslearn-improve-api-developer-experience-with-swagge.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "mslearn-improve-api-developer-experience-with-swagge.dll"]
