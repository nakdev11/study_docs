# SpringBoot勉強会

- SpringBoot2プログラミング入門という書籍をベースに勉強します。
- 当資料見出しの（1.1）などの番号は、書籍の章を示しています。

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
    
    - コントローラークラスをコーディングする時のポイント
        - @RestController
            - レストコントローラーに付与するアノテーション
        - @RequestMapping
            - リクエストしてきたURLパスと紐付けるメソッドに付与するアノテーション（URLマッピング）
            - このようなメソッドをリクエストハンドラという

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

- パス変数を使ってみる （リスト3-9）
    - URLのパス部分の一部を変数（パス変数）として利用する
    - http://localhost:8080/100 の100の部分
    - @PathVariableでメソッドの引数に受け取る


- TEXTではなくJSONでレスポンスしてみる（リスト3-10）
    - リクエストハンドラの戻り値をClassにすると、Springが勝手にJSONに変換して、クライアントに返してくれる
    - JSONとは
      - データ定義言語
      - {"id": 1, "name": "yamada", "age": 28, "Birthplace": "Tokyo"}
      - Key：Value形式、全体を波括弧で括る、ダブルクオーテーションで括る、数値は括らない
      - 詳しくは → [JSON入門](http://www.tohoho-web.com/ex/json.html){:target="_blank"}

## ControllerとThymeleafを利用する（3.4）

- テンプレート（View）を表示する

    ![MVCアーキテクチャ概要図](MVC2.png)

    - Controllerクラスを作る（リスト3-13）
        - @Controller
        - return "パス/HTMLファイル名（拡張子除く）"
        - パスは、src/main/resources/templates からの相対パス
    
    - テンプレートファイルを作る（リスト3-14）
            - /resources/templates配下に保存
    
    - http://localhost:8080 へアクセス
    
    - （お題）templates配下にフォルダを作って、そこに新たなHTMLを作り表示してみる
      - src/resources/templates/hoge/fuga.html


- テンプレートに値を表示する

    ![MVCアーキテクチャ概要図](MVC3.png)

    - リクエストURLのパスに入っている値をHTMLに表示してレスポンスする

        - Controllerが、パス変数を受け取り、Modelに保存する

        - Viewが、Modelから値を取得してHTMLを作る

        - Controllerが、HTMLをレスポンスする
    
    - テンプレートを作る（リスト3-15）
        - th:text="${hoge}"
            - ModelにhogeというKeyで保存した値を表示する

    - Controllerを作る（リスト3-16）
        - model.addAttribute("hoge", 値)
            - modelにhogeというKeyで値を保存する

    - Modelって何？
        - ControllerとView間で値をやり取りするためのクラス
        - Springが予め準備しているクラス
        - Key:Value形式で値を保存出来る
        - 値を保存する時、addAttributeメソッドを使う
        - htmlに表示する時は、th:text="${hoge}"と書く

## おまけ（時間があれば）

    - 勉強会レジュメ作成の流れ
      - 環境準備
        - vscodeインストール
        - vscodeにDraw.io Integrationを入れる
      - レジュメ作成
        - markdownでレジュメを書く
        - Draw.ioで図表を書く
      - レジュメをGitHubへアップして、インターネットに公開する
        - GitHubに勉強会用のリポジトリを作成
        - ローカルのレジュメをGitHubへ登録
      - GitHub Pagesの設定
      - インターネットに公開した自分のレジュメを見てみる
      - 参照 → [GitHubを使ってMarkdown文書を５ステップでホームページとして公開する方法](https://qiita.com/MahoTakara/items/3800e9dc83b530d0a050){:target="_blank"}

## 次回、発表したい人、募集中🎶

    - 勉強会は発表する人が一番勉強出来ます！
    - 勉強会に向けてモチベーションが上がります！
    - P150〜159まで、3章コンプリートしたい。
    - 何人かで分担するといいかも。
      - ModelAndViewクラスを使ってみる　p150〜151
        - ModelとModelAndViewの違いを抑えたい
      - フォームを利用する　p152〜153
      - その他のフォームコントロール　
    - 私が作ったレジュメをgithubで協同編集しますか？
