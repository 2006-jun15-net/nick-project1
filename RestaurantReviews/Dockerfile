FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build

WORKDIR /app/src

# RUN dotnet tool install --global dotnet-sonarscanner

# copy just csproj/sln files
COPY RestaurantReviews.DataAccess/*.csproj RestaurantReviews.DataAccess/
COPY RestaurantReviews.Domain/*.csproj RestaurantReviews.Domain/
COPY RestaurantReviews.Tests/*.csproj RestaurantReviews.Tests/
COPY RestaurantReviews.WebUI/*.csproj RestaurantReviews.WebUI/
COPY *.sln ./
RUN dotnet restore

# copy rest of build context into /app/src
COPY . ./

# RUN dotnet sonarscanner begin ...

# FROM mcr.microsoft.com/dotnet/core/sdk:3.1-alpine AS test

# RUN dotnet build

# FROM mcr.microsoft.com/dotnet/core/sdk:3.1-alpine AS analyze

# COPY

# RUN dotnet test

# RUN dotnet sonarscanner end

# publish to /app/publish
RUN dotnet publish RestaurantReviews.WebUI -o ../publish

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS runtime

WORKDIR /app

# copy assemblies from build stage into this stage
COPY --from=build /app/publish ./

CMD dotnet RestaurantReviews.WebUI.dll
