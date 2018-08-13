FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 50769
EXPOSE 44347

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Swagger_Example/Swagger_Example.csproj Swagger_Example/
RUN dotnet restore Swagger_Example/Swagger_Example.csproj
COPY . .
WORKDIR /src/Swagger_Example
RUN dotnet build Swagger_Example.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Swagger_Example.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Swagger_Example.dll"]
