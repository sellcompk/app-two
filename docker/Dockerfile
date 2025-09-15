FROM mcr.microsoft.com/dotnet/aspnet:8.0

WORKDIR /app

ENV ASPNETCORE_URLS=http://+:80

COPY \
    . /app

ENTRYPOINT ["dotnet", "src/app-two/app-two.dll"]

EXPOSE 80
