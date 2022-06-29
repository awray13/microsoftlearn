FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY backend.csproj .
RUN dotnet restore
COPY . . 
RUN dotnet publish -c release -o /app

# This will perform the following steps sequentially when invoked

# Pull the mcr.microsoft.com/dotnet/sdk:6.0 image and name the image build
# Set the working directory within the image to /src
# Copy the file named backend.csproj found locally to the /src directory that was just created
# Calls dotnet restore on the project
# Copy everything in the local working directory to the image
# Calls dotnet publish on the project

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=build /app .
ENTRYPOINT [ "dotnet", "backend.dll" ]

# This will perform the following steps sequentially when invoked:

# Pull the mcr.microsoft.com/dotnet/aspnet:6.0 image
# Set the working directory within the image to /app
# Expose port 80 and 443
# Copy everything from the /app directory of the build image created above into the app directory of this image
# Sets the entrypoint of this image to dotnet passes backend.dll as an argument