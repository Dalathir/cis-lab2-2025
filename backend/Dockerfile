# ============ 1 Стадия: сборка ============
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Создать рабочую директорию
WORKDIR /app

# 1) Скопировать файл проекта
COPY *.csproj ./

# 2) Выполнить dotnet restore
RUN dotnet restore

# 3) Скопировать оставшийся код
COPY . .

# 4) Выполнить dotnet build
RUN dotnet build -c Release -o /app/build

# 5) Выполнить dotnet publish
RUN dotnet publish -c Release -o /app/publish

# ============ 2 Стадия: рантайм ============
FROM mcr.microsoft.com/dotnet/aspnet:8.0

# Создать рабочую директорию
WORKDIR /app

# 1) Скопировать результат сборки из первой стадии
COPY --from=build /app/publish .

# 2) Запустить приложение
ENTRYPOINT ["dotnet", "Backend.dll"]