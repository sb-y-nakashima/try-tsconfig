# try-tsconfig
TypeScriptのtsconfigに挑戦

## target
コンパイルしたときに出力されるJavaScriptのバージョン  
https://www.typescriptlang.org/tsconfig/#target  
最新のブラウザはES6のすべての機能をサポートしているためES6を選択

## lib
targetに指定しているjsのバージョンには含まれていない、組み込みライブラリを使用する  
https://www.typescriptlang.org/tsconfig/#lib  
値  | 内容
-- | -- 
dom | DOM定義 - window、document、など
dom.iterable | DOMのインターフェース（NodeListやHTMLCollectionなど）が反復可能（iterable）であることを認識します。
esnext | ESNext	ESNext で利用可能な追加の API - これは JavaScript 仕様の進化に応じて変更されます

## module
出力されるJavaScriptが、どのようにモジュールを読み込むか指定します。  
https://www.typescriptlang.org/tsconfig/#module  
基本はesnextでしょうか？バックエンドならcommonjs？
>--アドバイスいただきました！--  
>パフォーマンスに違いもありますがケースバイケース。  
>typescript系のネタだと、yarnはちょっと前までもてはやされてましたが、最近はpnpmも熱いみたいです。

## strict
広範囲の型チェック動作が有効になり、プログラムの正確性がより強力に保証されます。  
厳密モードのオプションをすべて有効にする。  
https://www.typescriptlang.org/tsconfig/#strict  
これは絶対にtrueでしょ！
オプション | 内容
-- | -- 
noImplicitAny | 型が推論不能のときにコンパイルエラーにする（型の書き忘れや推論の失敗を防ぐ）
noImplicitThis | 	暗黙の「any」タイプを持つ「this」式でエラーを発生させます。
alwaysStrict | ソース ファイルごとに「use strict」を発行します。
strictBindCallApply | bind(),call(),apply()メソッドを厳格に型付けする
strictNullChecks | nullやundefinedを代入したい場合、明示的に指定する必要がある。（nullやundefinedを安全に検査する）
strictFunctionTypes | 関数のパラメーターがより正確にチェックされます
strictPropertyInitialization | クラス プロパティが宣言されていてもコンストラクターに設定されていない場合、TypeScript はエラーを発生させます。
useUnknownInCatchVariables | catchの例外変数のデフォルトの型がunknownになる

## noUncheckedIndexedAccess
未チェックのインデックス付きアクセスは禁止  
https://www.typescriptlang.org/tsconfig/#noUncheckedIndexedAccess

## noImplicitReturns
関数の戻り値がvoid以外のときにreturnを必須にします。  
https://www.typescriptlang.org/tsconfig/#noImplicitReturns  

## noFallthroughCasesInSwitch
switch文で、caseをbreakやreturnで終えていることを必須にします。  
https://www.typescriptlang.org/tsconfig/#noFallthroughCasesInSwitch

## noImplicitOverride
スーパークラスのメソッドをオーバーライドする時、overrideを必須にします。  
https://www.typescriptlang.org/tsconfig/#noImplicitOverride

## sourceMap
動作させるときにデバッガーが元のTypeScriptソースファイルを表示できるようします。　　
https://www.typescriptlang.org/tsconfig/#sourceMap
セキュリティの問題もあるので状況によってtrue、falseを切り替えるかも...
ViteやNext.jsなどの場合は不要かな...  

inlineSourceMapと排他なので同時に使用することはできません。

## forceConsistentCasingInFileNames
実行されているファイルシステムの大文字と小文字の区別規則に従う  
推奨はtrue（OSによっては、大文字小文字を区別出来ない場合があるため）  
https://www.typescriptlang.org/tsconfig/#forceConsistentCasingInFileNames

## noEmit
JavaScript ソース コード、ソースマップ、宣言などのコンパイラ出力ファイルを出力しない　　
https://www.typescriptlang.org/tsconfig/#noEmit

## moduleResolution
モジュールをどのように解決するのかを指定します。  
https://www.typescriptlang.org/tsconfig/#moduleResolution  
一般的には'node10'(以前は'node'と呼ばれていました)との記事もあるが、  
新しいNode.jsでは'node16'または'nodenext'を試してとある。  
Node.js v12 以降は ECMAScript import と CommonJS require の両方をサポートしている。  

nodenextに設定されているときに、moduleオプションもnodenextに設定されている必要があります。

## experimentalDecorators
実験的なデコレーター  
https://www.typescriptlang.org/tsconfig/#experimentalDecorators  
TypeScriptでClassを使う機会が少ないと思うのでどちらでも...とりあえずtrueで。

## isolatedModules
各ファイルを独立して変換する際に、解釈できないコードがある場合に警告するコンパイラオプションです。　　
https://www.typescriptlang.org/tsconfig/#isolatedModules

これはtrueでしょ。　　
https://typescriptbook.jp/reference/tsconfig/isolatedModules#%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E3%81%A7%E3%81%AA%E3%81%84%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB

## resolveJsonModule
jsonファイルのインポートを可能にする  
https://www.typescriptlang.org/tsconfig/#resolveJsonModule  
不要かな...falseで。状況によってtrueにする。  

## allowJs
JavaScript（JSファイル）を許可する。  
https://www.typescriptlang.org/tsconfig/#allowJs  
不要だと思います。falseで。

## skipLibCheck
宣言ファイルの型チェックをスキップします。  
型システムの精度は犠牲になりますが、コンパイル時の時間を節約できます。  
https://www.typescriptlang.org/tsconfig/#skipLibCheck  

## esModuleInterop
ESモジュールの相互運用性  
https://www.typescriptlang.org/tsconfig/#esModuleInterop  
問題を修正してくれるのでtrueかな。  

## incremental
出力ディレクトリにtsbuildinfoファイルを作成する。  
これにより差分でコンパイルするので初回以外は早くなる。  
tsconfigを変えたらtsBuildInfoファイルを削除して最初からコンパイルした方が良い。  
https://www.typescriptlang.org/tsconfig/#incremental

## outDir
JavaScriptファイルの出力先  
https://www.typescriptlang.org/tsconfig/#outDir  

## include
コンパイル対象
https://www.typescriptlang.org/tsconfig/#include

## exclude
includeを解決する際のスキップ対象  
https://www.typescriptlang.org/tsconfig/#exclude  
