FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["dockerapp/dockerapp.csproj", "dockerapp/"]
RUN dotnet restore "dockerapp/dockerapp.csproj"
COPY . .
WORKDIR "/src/dockerapp"
RUN dotnet build "dockerapp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "dockerapp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "dockerapp.dll"]