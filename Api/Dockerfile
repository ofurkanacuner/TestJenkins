#Base Image
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env 
#Container içerisinde çalýþacaðýmýz klasör adý
WORKDIR /app

#Api.csproj app klasörüne kopyaladýk
COPY *.csproj .

#dotnet restore çalýþtý
RUN dotnet restore

#Ýçerisinde bulunduðum tüm dosyalarý docker container içerisindeki app klasörüne taþýndý
COPY . ./

#Publish iþlemi yapýldý
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
#Build edilmiþ dosyalarý app'in altýndaki out altýndakilerin tamamýný çalýþma klasörüne alýyoruz
COPY --from=build-env /app/out .
#dotnet gidip Api.dll çalýþtýracak. Öncelikle program.cs içine yazdýklarýmýz çalýþmaya baþlayacak
ENTRYPOINT ["dotnet", "Api.dll"]