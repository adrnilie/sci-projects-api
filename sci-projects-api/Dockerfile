FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["sci-projects-api/sci-projects-api.csproj", "sci-projects-api/"]
RUN dotnet restore "sci-projects-api/sci-projects-api.csproj"
COPY . .
WORKDIR "/src/sci-projects-api"
RUN dotnet build "sci-projects-api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "sci-projects-api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "sci-projects-api.dll"]