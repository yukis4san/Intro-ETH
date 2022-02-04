👩‍💻 コントラクトを作成する
-------------------------------------------

「👋（wave）」の総数をトラッキングするスマートコントラクトを作成します。

- ここで作成するスマートコントラクトは、後でユースケースに合わせて自由に変更することが可能です。

`contracts` ディレクトリの下に `WavePortal.sol` という名前のファイルを作成します。

Terminal上で新しくファイルを作成する場合は、下記のコマンドが役立ちます。

1. `my-wave-portal` ディレクトリに移動: `cd my-wave-portal`
2. `contracts` ディレクトリに移動: `cd contracts`
3. `WavePortal.sol` ファイルを作成: `touch WavePortal.sol`

Hardhat を使用する場合、ファイル構造は非常に重要なので、注意する必要があります。ファイル構造が下記のようになっていれば大丈夫です😊
```bash
my-wave-portal
    |_ contracts
           |_  WavePortal.sol
```

次に、コードエディタでプロジェクトのコードを開きます。

ここでは、VS Code の使用をお勧めします。ダウンロードは[こちら](https://azure.microsoft.com/ja-jp/products/visual-studio-code/)から。

VS Code をターミナルから起動する方法は[こちら](https://maku.blog/p/f5iv9kx/)をご覧ください。今後 VS Code を起動するのが一段と楽になるので、ぜひ導入してみてください。

それでは、これから `WavePortal.sol` の中身の作成していきます。`WavePortal.sol` を VS Code で開き、下記を入力します。

```solidity
// SPDX-License-Identifier: UNLICENSED

pragma solidity ^0.8.0;

import "hardhat/console.sol";

contract WavePortal {
    constructor() {
        console.log("Here is my first smart contract!");
    }
}
```

コーディングのサポートツールとして、VS Code 上で Solidity の拡張機能をダウンロードすることをおすすめします。ダウンロードは [こちら](https://marketplace.visualstudio.com/items?itemName=JuanBlanco.solidity) から。

```solidity
// WavePortal.sol
// SPDX-License-Identifier: UNLICENSED
```
これは「SPDXライセンス識別子」と呼ばれ、ソフトウェア・ライセンスの種類が一目でわかるようにするための識別子です。

```solidity
// WavePortal.sol
pragma solidity ^0.8.0;
```
これは、コントラクトで使用する Solidity コンパイラのバージョンです。上記の場合「このコントラクトを実行するときは、Solidity コンパイラのバージョン0.8.0のみを使用し、それ以下のものは使用しません。」という意味です。コンパイラのバージョンが `hardhat.config.js` で同じであることを確認してください。

もし、`hardhat.config.js` の中に記載されている Solidity のバージョンが `0.8.0` でなかった場合は、`WavePortal.sol` の中身を `hardhat.config.js` に記載されているバージョンに変更しましょう。

```solidity
// WavePortal.sol
import "hardhat/console.sol";
```

コントラクトを実行する際、コンソールログをターミナルに出力するために Hardhat の`console.sol` のファイルをインポートしています。これは、今後スマートコントラクトのデバッグが発生した場合に、とても役立つツールです。

```solidity
// WavePortal.sol
contract WavePortal {
    constructor() {
        console.log("Here is my first smart contract!");
    }
}
```
`contract` は、他の言語でいうところの「[クラス](https://wa3.i-3-i.info/word1120.html)」のようなものなのです。この `contract` を初めて初期化すると、`contructor` が実行されて `console.log` の中身がターミナル上に表示されます。

🔩 `contructor`とは
-------------------------------------------
`contructor` はオプションの関数で、`contract` の状態変数を初期化するために使用されます。これから詳しく説明していくので、`contructor` に関しては、まず以下の特徴を理解してください。

- `contract` は 1 つの `contructor` しか持つことができません。

- `contructor` は、スマートコントラクトの作成時に一度だけ実行され、`contract` の状態を初期化するために使用されます。

- `contructor` が実行された後、最終的なコードがブロックチェーンにデプロイされます。

🙋‍♂️ 質問する
-------------------------------------------
ここまでの作業で何かわからないことがある場合は、Discord の `#section-1-help` で質問をしてください。

ヘルプをするときのフローが円滑になるので、エラーレポートには下記の3点を記載してください✨
```
1. 何をしようとしていたか
2. エラー文をコピー&ペースト
3. エラー画面のスクリーンショット
```
----------------------------------
テストの出力が完了したら次のステップに進んでください🎉

次のレッスンでは、スマートコントラクトを実行します。

<!-- 🚨[次のレッスン]をクリックする前に
-------------------------------------------

*注：これを行わないと、Farzaは非常に悲しくなります：(。*

#progressに移動し、WavePortal.solファイルにファンシーコントラクトのスクリーンショットを投稿してください:)。-->
