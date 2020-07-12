# SpringBoot勉強会

- SpringBoot2プログラミング入門という書籍をベースに勉強します。
- 当資料見出しの（1.1）などの番号は、書籍の章を示しています。

## 今日勉強したいこと

- SpringBootって何？
- STSを触ってみる
- プロジェクトを作ってみる
- HelloWorldを表示してみる

## Spring Bootって何？（1.1）

- JavaでWebアプリケーションを開発するためのフレームワーク

    - Spring Frameworkというフレームワーク群があり、その中の１つ


- フレームワークとは
    - 枠組み、骨組み
    - ライブラリとほぼ同じ意味
        - 何かプログラムを組む時、あらかじめ誰かが作ったプログラムを利用する。  
        その誰かが作ったプログラムのこと。
        - 例えば、java.util.Date、java.timeなど
        - フレームワークも誰かが作ったプログラム
    - ライブラリとフレームワークの違い
        - 呼び出し方向が違う
        - 自分のプログラムがライブラリを呼び出す
        - フレームワークが自分のプログラムを呼び出す


- Webアプリケーション関連のフレームワーク（Java）

    - MVCフレームワーク
        - Struts
        - JSF
        - Spring MVC

    - DBアクセスフレームワーク
        - Hibernate
        - iBatis
        - JDBC
            - Javaからデータベースにアクセスするための標準的なAPI
            - 何でも出来るが、自分で全てコーディング必要
        - JPA
            - なるべくSQLを書かないで済むことを目指しているフレームワーク
            - 比較的単純なSQLを発行するシステムに適する
            - 複雑なSQLを書かざる得ないシステムで適合しないことあり
        - myBatis
            - SQLは自分で書く。複雑なSQLでも対応可
            - SQLを外部ファイルで管理可
            - DB接続やエラー処理などある程度自動化
            - 現場で一番使われていると感じる


- その他言語のWebアプリケーションフレームワーク
    - Ruby -> Rails
    - Python -> Django
    - PHP -> Larabel


- Spring Bootとは
    - Spring MVCの完成形
    - "Railsライク"とも言われる高速開発可能なフレームワーク
    - Spring Framework群を組み合わせて最良のWebアプリケーション環境を素早く構築するためのスターターキット的なライブラリ
    - Spring Bootは、非常にシンプルにWebアプリケーションを構築することが出来る
    - 大規模システム開発現場でも採用されている


- Spring用の専用開発ツール Spring Tool Suite
    - STSと呼ぶ
    - Eclipseベース


- Spring Frameworkの概要
    - p6〜７参照


- Spring FrameworkによるWebアプリケーション開発
    - MVCアーキテクチャ
        - プログラムの整理整頓
            - Controllerは、プログラム全体を制御する役目のプログラム
            - Modelは、業務ロジック、データ管理をつかさどるプログラム
            - Viewは、画面の表示を扱う役目のプログラム
    

![MVCアーキテクチャ概要図](MVC.png)

## STSを触ってみる（1.3）

- ビュー

- パースペクティブ
    - Springバースペクティブはどこ？


## プロジェクトを作って実行してみる（3.2）

- STSでMavenベースのプロジェクト作成／実行

    - プロジェクトを作る
        - Spring Starter Project

    - プロジェクトを実行する
        - Run As > Spring Boot App

    - ブラウザからアクセスする

        - http://localhost:8080
            - Springが起動しているので、Springのエラーページが見える
            - SpringBootはサーバー内蔵方式なので、プロジェクトを起動するだけで、アプリケーションを実行出来る。  
            サーバーへのデプロイは不要。

        - Springを停止し、再度アクセス
            - Springが止まっているので、アクセス出来ない

    - pom.xmlについて
        - 重要だけど一旦飛ばす

- STSでGradleベースのプロジェクト作成／実行
    - 飛ばす


## RestControllerを利用する（3.3）


![MVCアーキテクチャ概要図](MVC_REST.png)

- まず、RestControllerを使ってみる
    - RESTとは
        - Representational State Transferの略
        - 分散システムのアーキテクチャ
        - 外部システムにアクセスし、必要な情報を取得するような仕組みで利用される
        - 取得する情報の形式はJSONが多い（今回はTEXTをレスポンスする）

- ブラウザが、あるURLをリクエストする
    - http://localhost:8080 へGETでリクエスト
- RestControllerが、リクエストされたURLに紐づくメソッドを実行し、ブラウザへレスポンスする
    - 文字列”Hello Spring!!"を返す


- ブラウザが、あるURLをリクエストする
    - http://localhost:8080/morning へGETでリクエスト
- RestControllerが、リクエストされたURLに紐づくメソッドを実行し、ブラウザへレスポンスする
    - 文字列”Good Morning!!"を返す


- httpのRequestとResponseを見てみる

    - chrome developer toolsを使う

    - Request Headers

        ```
        GET /morning HTTP/1.1
        Host: localhost:8080
        〜以下省略
        ```
    - Response Header

        ```
        HTTP/1.1 200
        Content-Type: text/html;charset=UTF-8
        Content-Length: 14
        Date: Sun, 12 Jul 2020 10:46:26 GMT
        Keep-Alive: timeout=60
        Connection: keep-alive
        ```

    - Response Body

        ```
        Good Morning!!
        ```

