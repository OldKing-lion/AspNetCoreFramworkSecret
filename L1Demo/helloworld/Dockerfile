#1 指定编译和发布的应用镜像
From mcr.microsoft.com/dotnet/sdk:5.0 AS build

#2 知道工作目录
WORKDIR /app

#3 将.csproj文件复制到工作目录/app，然后执行dotnet restore命令恢复Nuget包
COPY *.csproj ./
RUN dotnet restore

#4 将所有文件复制到工作目录，执行dotnet publish
COPY . ./
RUN dotnet publish -c Release -o out

#5 编译生成docker镜像
#5.1 设置基础镜像
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS runtime
#5.2 设置目录
WORKDIR /app
COPY --from=build /app/out .
ENV ASPNETCORE_URLS http://0.0.0.0:3721
ENTRYPOINT ["dotnet","helloworld.dll"]