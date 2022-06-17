#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CloudDemoApplication1/CloudDemoApplication1.csproj", "CloudDemoApplication1/"]
RUN dotnet restore "CloudDemoApplication1/CloudDemoApplication1.csproj"
COPY . .
WORKDIR "/src/CloudDemoApplication1"
RUN dotnet build "CloudDemoApplication1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CloudDemoApplication1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CloudDemoApplication1.dll"]