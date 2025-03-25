FROM mcr.microsoft.com/dotnet/sdk:9.0

ENV DOTNET_USE_POLLING_FILE_WATCHER=1
ENV DOTNET_ENVIRONMENT=Development
ENV ASPNETCORE_URLS=https://+:8080
ENV ASPNETCORE_Kestrel__Certificates__Default__Password="password"
ENV ASPNETCORE_Kestrel__Certificates__Default__Path="/app/https-cert.pfx"
ENV PATH="/root/.dotnet/tools:/opt/mssql-tools18/bin:${PATH}"
ENV ACCEPT_EULA=Y

# Database environment variables with defaults for local dev
ENV DB_HOST="sqlserver"
ENV DB_PORT="1433"
ENV DB_NAME="TodoDb"
ENV DB_USER="sa"
ENV DB_PASSWORD="V3ryW34kP455w0rd!"
ENV DB_CONNECTION_STRING="Server=${DB_HOST},${DB_PORT};Database=${DB_NAME};User Id=${DB_USER};Password=${DB_PASSWORD};TrustServerCertificate=True"

# Also set these so that sqlcmd works without arguments
ENV SQLCMDSERVER="${DB_HOST},${DB_PORT}"
ENV SQLCMDDBNAME=$DB_NAME
ENV SQLCMDUSER=$DB_USER
ENV SQLCMDPASSWORD=$DB_PASSWORD
RUN echo alias sqlcmd=\"sqlcmd -C\" >> /etc/bash.bashrc

RUN apt-get update && apt-get install -y curl iputils-ping telnet

# Install mssql-tools18 to provide sqlcmd for command line MS-SQL access
RUN curl -O https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb
RUN dpkg -i packages-microsoft-prod.deb
RUN rm packages-microsoft-prod.deb
RUN apt-get update && apt-get install -y mssql-tools18

WORKDIR /app
COPY . $WORKDIR

RUN dotnet restore
RUN dotnet tool install --global dotnet-ef
COPY https-cert.pfx /app/https-cert.pfx

ENTRYPOINT ["dotnet"]
CMD ["watch", "run"]



