#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Aya3/Aya3.csproj", "Aya3/"]
RUN dotnet restore "Aya3/Aya3.csproj"
COPY . .
WORKDIR "/src/Aya3"
RUN dotnet build "Aya3.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Aya3.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Aya3.dll"]