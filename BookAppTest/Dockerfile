FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BookAppTest.csproj", "BookAppTest/"]
RUN dotnet restore "BookAppTest/BookAppTest.csproj"
COPY . .
WORKDIR "/src/BookAppTest"
RUN dotnet build "BookAppTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BookAppTest.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BookAppTest.dll"]
