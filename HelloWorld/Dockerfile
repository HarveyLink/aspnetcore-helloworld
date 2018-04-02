FROM microsoft/aspnetcore:2.0 AS base
#sha256:d4270777fe6896c184e9c360503aa6549bdce3d8dd4d6341912f51d64d8b563c
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
#sha256:618d25f23747bd42d7fe023e539b4559094cc9f7bba96954580fa6625c6b028f
WORKDIR /src
COPY HelloWorld.sln ./
COPY HelloWorld/HelloWorld.csproj HelloWorld/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/HelloWorld
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloWorld.dll"]
