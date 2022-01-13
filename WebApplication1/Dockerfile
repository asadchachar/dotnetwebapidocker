#Get base SDK image from microsoft
from mcr.microsoft.com/dotnet/sdk:5.0 AS build-env
WORKDIR	/app

#Copy csproj file and restore any dependencies using NUGET
COPY *.csproj ./	
RUN dotnet restore

#Copy the project files and build our release
COPY . ./
RUN dotnet publish -c Release -o out

#Genetate RunTime Image
from mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
EXPOSE 80
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "WebApplication1.dll"]
