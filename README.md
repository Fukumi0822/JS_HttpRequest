# JS_HttpRequest

ネイティブなJavaScriptでAjaxを簡単に使う事が出来るラップクラス

ネイティブなXMLHttpRequestオブジェクトを使う為に必要な記述を使用毎に記述するには大変ですが、
当ラップクラスを使う事でとても簡単な記述でAjaxを使う事が可能になります。

## 特徴

XMLHttpRequestを継承したHttpRequestクラスを使う事でネイティブな記述と拡張された記述で利用可能で、
jQuery等のAjaxと似た記述で利用出来ます。

とても軽量でわざわざその他機能が実装されているライブラリ・フレームワークをインストールする必要はありません。

# インストール

`httpRequest.js`を使いたいページにロードするだけ

# 使用方法

## GET Request

```
let http = new HttpRequest();
http.get('./loadfile.txt', (data, status)=>{
  if(status){
    console.log(data);
  }
});
```

### HttpRequest.get(Filename, [Callback(data, status)])

- Filename
  リクエスト先ファイルやサーバーサイドプログラムを指定します。GETパラメーターを付加する事も可能です。
- Callback
  リクエスト後のloadイベントが発火した際に呼び出すコールバック関数を指定します。
  + data (String)
    リクエスト先のレスポンスを返します。
  + status (Bool)
    ステータスのチェックメソッド`statusCheck()`による結果を返します。


## POST Request

```
let http = new HttpRequest();
http.post('./loadfile.txt', {param1 : "data1", param2 : "data2" }, (data, status)=>{
  if(status){
    console.log(data);
  }
});
```

### HttpRequest.post(Filename, parameter, [Callback(data, status)], RequestHeader)

- Filename
  リクエスト先ファイルやサーバーサイドプログラムを指定します。GETパラメーターを付加する事も可能です。
- parameter
  POSTするデータをセットします。
- Callback
  リクエスト後のloadイベントが発火した際に呼び出すコールバック関数を指定します。
    + data (String)
    リクエスト先のレスポンスを返します。
    + status (Bool)
    ステータスのチェックメソッド`statusCheck()`による結果を返します。 
- RequestHeader
  異なるパラメーター送信方法を使用したい場合に使用可能です。

#### Option RequestHeaderについて

パラメーター送信時に異なる方式でPOST送信したい場合に変更します。
デフォルトでは次の様になっています。
```
RequestHeader = ['Content-Type', 'application/x-www-form-urlencoded'];
```


## ネイティブな記法

当クラスはXMLHttpRequestを継承したサブクラスです。
サブクラスでは親クラスのパブリックプロパティを参照する事が出来る為、
上記リクエスト方法とネイティブなリクエスト方法を混ぜて使用可能です。

また、サブクラスメソッドによってネイティブなリクエスト方法を使いつつ便利な機能を提供しています。

### サブクラス メソッド

- statusCheck(void)
  リクエストステータスをチェックします。this.statusをチェックし、Bool型の戻り値を返します。
- connect(event, [callback( data, status )])
  各種イベントをセットする事が出来ます。
  + event (String)
    文字列のイベントタイプを指定
  + callback( data, status )
    イベント発生時のコールバック関数を指定します。
    * data レスポンスデータを渡します。
    * status 直前に調査したステータスを返します。

### サブクラス プロパティ

- bool_Status
  `statusCheck()`によるBool型結果を保持しています。


# Requirements

当クラスES6以降の記述を使用して作成されています。次のリストにある物が使えるかを調査した上でご利用ください。

- クラス
- ラムダ式
- パラメーター初期化