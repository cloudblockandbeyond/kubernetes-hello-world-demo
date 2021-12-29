FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src

COPY kubernetes-hello-world-demo.csproj .
RUN dotnet restore

COPY . .
RUN dotnet publish --configuration Release --output /out

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS runtime
WORKDIR /app
COPY --from=build /out .
ENV RuntimeEnvironment="Dockerfile"
EXPOSE 80/tcp
ENTRYPOINT [ "dotnet", "kubernetes-hello-world-demo.dll" ]