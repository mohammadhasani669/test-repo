# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# کپی فایل csproj و restore کردن دپندنسی‌ها
COPY WebApplicationTest.csproj .
RUN dotnet restore

# کپی کل پروژه و build
COPY . .
RUN dotnet publish -c Release -o /app

# Stage 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app .

# پورت پیش‌فرض ASP.NET Core
EXPOSE 5283

ENV ASPNETCORE_URLS=http://+:5283

# دستور اجرا
ENTRYPOINT ["dotnet", "WebApplicationTest.dll"]
