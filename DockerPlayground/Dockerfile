FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["DockerPlayground/DockerPlayground.csproj", "DockerPlayground/"]
RUN dotnet restore "DockerPlayground/DockerPlayground.csproj"
COPY . .
WORKDIR "/src/DockerPlayground"
RUN dotnet build "DockerPlayground.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DockerPlayground.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerPlayground.dll"]