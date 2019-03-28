FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["AspNetCoreApiLoggingSample/AspNetCoreApiLoggingSample.csproj", "AspNetCoreApiLoggingSample/"]
RUN dotnet restore "AspNetCoreApiLoggingSample/AspNetCoreApiLoggingSample.csproj"
COPY . .
WORKDIR "/src/AspNetCoreApiLoggingSample"
RUN dotnet build "AspNetCoreApiLoggingSample.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AspNetCoreApiLoggingSample.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspNetCoreApiLoggingSample.dll"]