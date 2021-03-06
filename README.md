# .NET Core Identity Practice
.NET Core Identity Practice Project

## need .NET Core SDK 3.1
https://docs.microsoft.com/ja-jp/dotnet/core/install/macos

## 作業メモ
- プロジェクト準備
  - `git clone`
  - `touch .gitignore`
    - https://www.toptal.com/developers/gitignore
  - change LICENSE
  - `dotnet new mvc -o .`
  - `dotnet run` で起動確認
- アプリケーションを docker-compose で立ち上げる準備
  - アプリケーションの `Dockerfile` 作成
  - `dotnet dev-certs https -ep ${HOME}/.aspnet/https/aspnetapp.pfx -p passward`
  - `dotnet dev-certs https --trust`
  - アプリケーションだけの `docker-compose.yml` を作成
  - `docker-compose up -d` で動作確認
- Swaggerいれる
  - `dotnet add package Swashbuckle.AspNetCore --version 5.6.3`
  - Startup.cs に Swashbuckle.AspNetCore を使うための設定を追記
  - サンプルAPIを追加
- docker-compose に MySQL など追加
  - adminer, mysql, redis を追加
  - mysql の文字コード設定を確認するクエリ `show variables like '%char%';`
- dapper 他使用パッケージを入れて接続確認
  - `dotnet add package Dapper --version 2.0.35`
  - `dotnet add package MySql.Data --version 8.0.21`
  - `dotnet add package CloudStructures --version 2.3.2`
  - ConnectionString の server はlocalhostではなく container_name(=myql) にする
  - .env ではなく docker-compose 内の environment に環境変数を書く場合はスペースを含んでいても引用符なしで記述
    - NG: APPSETTING_DBCONNECTION="server=mysql; database=hoge"
    - OK: APPSETTING_DBCONNECTION=server=mysql; database=hoge
- 認証認可を入れてみる
  - 今ここ

## 今回は実施してないメモ
- プロジェクトを分けたディレクトリ構成
  - root
    - App
      - Dockerfile
      - docker-compose.yml
    - App.Tests
    - Dockerfile
    - App.sln
      - https://docs.microsoft.com/ja-jp/dotnet/core/testing/unit-testing-with-dotnet-test

## 作業メモの作業メモ
- [x] Stepを参考にDockerコンテナ立てる
  - [x] HTTPS接続させるのにここ見なきゃかも
    - https://docs.microsoft.com/ja-jp/aspnet/core/security/docker-compose-https?view=aspnetcore-3.1
  - [x] Dockerfile作成
    - https://docs.microsoft.com/ja-jp/aspnet/core/host-and-deploy/docker/building-net-docker-images?view=aspnetcore-3.1
- [x] 同様にSwaggerいれる
  - [x] 簡単なAPIも用意しSwaggerUI確認
- [x] 同様にDapperもいれる
  - [x] 簡単なデータベースアクセスもテストする
- [ ] Webエンジニア(仮)の備忘録 を参考に認証認可とSendGridでのメール認証いれる
  - https://techikoma.com/index.php/2020/06/05/asp-net-core-mvc/
  - https://techikoma.com/index.php/2020/06/11/identity-net-core/
  - ここも参照
    - https://docs.microsoft.com/ja-jp/aspnet/core/security/authentication/accconfirm?view=aspnetcore-3.1&tabs=visual-studio

