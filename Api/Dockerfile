#Base Image
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env 
#Container içerisinde çalışacağımız klasör adı
WORKDIR /app

#Api.csproj app klasörüne kopyaladık
COPY *.csproj .

#dotnet restore çalıştı
RUN dotnet restore

#İçerisinde bulunduğum tüm dosyaları docker container içerisindeki app klasörüne taşındı
COPY . ./

#Publish işlemi yapıldı
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
#Build edilmiş dosyaları app'in altındaki out altındakilerin tamamını çalışma klasörüne alıyoruz
COPY --from=build-env /app/out .
#dotnet gidip Api.dll çalıştıracak. Öncelikle program.cs içine yazdıklarımız çalışmaya başlayacak
ENTRYPOINT ["dotnet", "Api.dll"]
