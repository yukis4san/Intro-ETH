👩‍💻 コントラクトを作成する
-------------------------------------------

まず、「👋（wave）」の総数をトラッキングするスマートコントラクトを作成します。ここで作成するスマートコントラクトは、後でユースケースに合わせて自由に変更することが可能です。

`contracts`ディレクトリの下に`WavePortal.sol`という名前のファイルを作成します。Terminal上で新しくファイルを作成する場合は、下記のコマンドが役立ちます。

1. `my-wave-portal`のディレクトリに移動:`cd my-wave-portal`
2. `contract`のディレクトリに移動: `cd contract`
3. WavePortal.solのファイルを作成: `touch WavePortal.sol`

Hardhatを使用する場合、ファイル構造は非常に重要なので、注意する必要があります。ファイル構造が下記のようになっていれば大丈夫です😊
```bash
my-wave-portal
    |_ contract
           |_  WavePortal.sol
```

次に、お気に入りのコードエディタでプロジェクトのコードを開きます。VS Codeの使用をお勧めします。ダウンロードは[こちら](https://azure.microsoft.com/ja-jp/products/visual-studio-code/)から。

VS Code をターミナルから起動する方法は[こちら](https://maku.blog/p/f5iv9kx/)をご覧ください。今後VS Codeを起動するのが一段と楽になるので、ぜひ導入してみてください。

それでは、これからWavePortal.solの中身の作成していきます。`WavePortal.sol`をコードエディタで開き、下記を入力します。

```solidity
// SPDX-License-Identifier: UNLICENSED

pragma solidity ^0.8.0;

import "hardhat/console.sol";

contract WavePortal {
    constructor() {
        console.log("Yo yo, I am a contract and I am smart");
    }
}
```

コーディングのサポートツールとして、VS Code上でSolidityの拡張機能をダウンロードすることをおすすめします。ダウンロードは[こちら](https://marketplace.visualstudio.com/items?itemName=JuanBlanco.solidity)から。

```solidity
// SPDX-License-Identifier: UNLICENSED
```
これは「SPDXライセンス識別子」と呼ばれ、ソフトウェア・ライセンスの種類が一目でわかるようにするための識別子です。

```solidity
pragma solidity ^0.8.0;
```
これは、コントラクトで使用するSolidityコンパイラのバージョンです。上記の場合「このコントラクトを実行するときは、Solidityコンパイラのバージョン0.8.0のみを使用し、それ以下のものは使用しません。」という意味です。コンパイラのバージョンが`hardhat.config.js`で同じであることを確認してください。

もし、`hardhat.config.js`の中に記載されているsolidityのバージョンが`0.8.0`でなかった場合は、`WavePortal.sol`の中身を`hardhat.config.js`に記載されているバージョンに変更しましょう。

```solidity
import "hardhat/console.sol";
```

コントラクトを実行する際、コンソールログをターミナルに出力するためにHardhatの`console.sol`のファイルをインポートしています。これは、今後スマートコントラクトのデバッグが発生した場合に、とても役立つツールです。

```solidity
contract WavePortal {
    constructor() {
        console.log("Here is my first smart contract!");
    }
}
```
`contract`は、他の言語でいうところの「[クラス](https://wa3.i-3-i.info/word1120.html)」のようなものなのです。この`contract`を初めて初期化すると、`contructor`が実行されて`console.log`の中身がターミナル上に表示されます。

🔩 `contructor`とは
-------------------------------------------
`contructor`はオプションの関数で、`contract`の状態変数を初期化するために使用されます。これから詳しく説明していくので、`contructor`に関しては、まず以下の特徴を理解してください。

- `contract`は 1 つの`contructor`しか持つことができません。

- `contructor`は、スマートコントラクトの作成時に一度だけ実行され、`contract`の状態を初期化するために使用されます。

- `contructor`が実行された後、最終的なコードがブロックチェーンにデプロイされます。

🙋‍♂️ 質問する
-------------------------------------------
ここまでの作業で何かわからないことがある場合は、Discordの`#section-1-help`で質問をしてください。

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
