# 課題1のif文のreturnについて

作成日 2021/01/03  
更新日 2021/01/11  
作成者 VLB 小野 裕己
***

## <span>1</span>そもそもreturnとは

メソッドの定義の際に指定した戻り値を呼び出し元のメソッドへ渡す物となります。  
呼び出し元に戻す為、returnの後の処理は実行される事はありません。  
メソッドの定義に指定した内容によってreturnは変化します。

下の表は、returnの動作についての表です。

| 戻り値のデータ型 | returnで返ってくる値
| :---: | :---: |
| string型 | 文字列 |
| int型 | 整数 |
| void | 他の型と違い何も返さない |

こちらは一部ですが、他のデータ型も同様の動きとなっています。  
これを踏まえて、mainメソッド内部のif文の説明をします。

## <span>2</span>まずは確認してみよう

まず、画像を見てください。

![課題1画像成果物イメージ](https://drive.google.com/uc?export=view&id=1RPO2Uyo6c5SYJ2R4yfjUbmV8KoWznJPB)

この画像は、課題1のページにある成果物のイメージ画像です。  
1番上のコマンドはコンパイルしている物なので、今回は説明は省きます。

二つ目のコマンドからみてください。

```
C:kadai>java Kadai3  
引数を一つ入力してください。
```

とあります。  
その下を見ると  

```
C:kadai>java Kadai3 1 2 
引数を一つ入力してください
```

となっていて、更に下を見ると

```
C:kadai>java Kadai3 あいうえを
１以上の整数を入力してください。
```

と続いています。  
これを意味する事は、 **「意図していないコマンドが入力されていたらアプリケーションを終了している」** ということです。

## <span>3</span>コードを見てreturn理解しよう

まずは、コードを実際に用意しました。  

```java
public static void main(String[] args) {

  // 引数が設定されなかった、または2つ以上設定された場合
  if (args.length != 1) {
   System.out.println("引数を一つ入力してください。");
   return;
  }

  // 入力値が整数値以外の場合
  if (!isNumber(args[0])) {
   System.out.println("1以上の整数を入力してください。");
   return;
  }

  // 入力値をString型からint型にキャスト
  int count = Integer.parseInt(args[0]);
     }
```


```csharp
public static void main(string[] args)
 {
  // 引数が設定されなかった、または2つ以上設定された場合
  if (args.length != 1)
  {
   Console.WriteLine("引数を一つ入力してください。");
   return;
  }

  // 入力値が整数値以外の場合
  // 入力値をString型からint型にキャストできれば整数型の変数countに渡す
  if (!int.TryParse(args[0],out int count))
  {
   Console.WriteLine("1以上の整数を入力してください。");
   return;
  }
    }
```

こちらは、実際に画像の通りに動く用に書いたコードの一部分となります。  
コードを見ると、if文で条件を確認している中にreturnがあります。

これは、指定した条件になったら作業を中断（終了）してねという意味になります。  
もし、if文の中にreturnが無い場合その条件の後も作業を行う為エラーに繋がります。

mainメソッドはvoidですので、returnには何も指定しなません。  
そしてmainメソッドの親となるメソッドはいません。  
その為、アプリケーションが終了するというわけです。

mainメソッドに対して使う必要無いんじゃない？と思うかもしれませんが、コードをじっくりと見ると意味がわかってくると思います。
