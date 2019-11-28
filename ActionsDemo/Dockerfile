FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["ActionsDemo/ActionsDemo.csproj", "ActionsDemo/"]
RUN dotnet restore "ActionsDemo/ActionsDemo.csproj"
COPY . .
WORKDIR "/src/ActionsDemo"
RUN dotnet build "ActionsDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ActionsDemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ActionsDemo.dll"]