🔥 スマートコントラクトをテスト環境で実行しよう
-----------------------------------------------

前回のレッスンでは、`WavePortal.sol` というスマートコントラクトを作成しました。

今回のレッスンでは下記を実行します。
1. `WavePortal.sol` をコンパイルします。
2. `WavePortal.sol` をテスト環境（=ローカル環境）でブロックチェーン上にデプロイします。
3. 上記が完了したら、`console.log` の中身がターミナル上に表示されます。

このプロジェクトの最終ゴールは、あなたのスマートコントラクトをブロックチェーン上にのせ、あなたのWEBアプリを介して世界中の人々がそのスマートコントラクトにアクセスできる状態を実現することです。

まずは、本番環境で実際に行うことをテスト環境で行います。

📝 コントラクトを実行するためのプログラムを作成する
-------------------------------------

`scripts` ディレクトリに移動し、`run.js` という名前のファイルを作成してください。

**`run.js` はローカル環境でスマートコントラクトのテストを行うためのプログラムです。**

`run.js` の中身に、以下を記入しましょう。

```javascript
// run.js
const main = async () => {
  const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
  const waveContract = await waveContractFactory.deploy();
  const wavePortal = await waveContract.deployed();

  console.log("Contract deployed to:", wavePortal.address);
};

const runMain = async () => {
  try {
    await main();
    process.exit(0);
  } catch (error) {
    console.log(error);
    process.exit(1);
  }
};

runMain();
```

それでは、1行ずつコードの理解を深めましょう。

```javascript
// run.js
const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
```
これにより、`WavePortal` コントラクトがコンパイルされます。
そして、コントラクトを操作するために必要なファイルが `my-wave-portal` ディレクトリの直下に存在する `artifacts` ディレクトリに生成されます。

✍️: `hre.ethers.getContractFactory` について
> `getContractFactory` 関数は、デプロイをサポートするライブラリのアドレスと `WavePortal` コントラクトの連携を行っています。
>
> `hre.ethers` は、Hardhat プラグインの仕様です。

✍️: `const main = async ()` と `await` について

> Javascript でコードを書いていると、コードの上から順に実行されなくて困ることがあります。これを同期処理に関する問題といいます。
>
> 解決法の一つとして、ここでは `async` / `await` を使用します。
>
> これを使うと、`await` が先頭についている処理が終わるまで、`main` 関数の他の処理は行われません。
>
> つまり、`hre.ethers.getContractFactory("WavePortal")` の処理が終わるまで、`main` 関数の中に記載されている他の処理は実行されないということです。

次に、下記の処理を見ていきましょう。

```javascript
// run.js
const waveContract = await waveContractFactory.deploy();
```

この処理は「ユーザーがあなたに「👋（wave）」を送ったことを記録するために、Hardhat がテスト環境でイーサリアムネットワークを作成する」ことを意味しています。

処理が完了すると、一度作成されたイーサリアムネットワークは終了します。

この処理のおかげで、`WavePortal` のコントラクトが実行されるたびに、ブロックチェーン上に新しい記録が残ります。

これは、プログラムを実行するたびにローカルサーバーを更新するようなものです。

次に下記の処理を見ていきましょう。

```javascript
// run.js
const wavePortal = await waveContract.deployed();
```

この処理は、`WavePortal` コントラクトがテスト環境のブロックチェーンに正式にデプロイされるまでは、これ以降に発生する処理を行わないことを意味しています。

最後に、下記の処理を見ていきましょう。
```javascript
// run.js
console.log("Contract deployed to:", wavePortal.address);
```

`WavePortal` コントラクトがテスト環境のブロックチェーンにデプロイされると、 `wavePortal.address` がデプロイされたコントラクトのアドレスを提供します。

そして、`console.log` が提供されたアドレスをターミナルに出力します。

- 実際のブロックチェーン上には何百万ものコントラクトが存在しますが、このアドレスはユニークなので、コントラクトを特定したいときに役立ちます。

🪄 実行してみよう
-----------------------------------------------

ターミナル上で、`scripts` ディレクトリに移動して下記を実行してみましょう。

```bash
npx hardhat run run.js
```

ターミナル上で `console.log` の中身とコントラクトアドレスが表示されていることを確認してください。

例）ターミナル上でのアウトプット:
```
Compiling 1 file with 0.8.4
Solidity compilation finished successfully
Here is my first smart cotract!
Contract deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3
```
上記のようなアウトプットターミナルに表示されていればテストは成功です🎉

🎩 Hardhat Runtime Environment について
--------------------------------

`run.js` の中で、`hre.ethers` が登場します。

しかし、`hre` はどこにもインポートされていません。それはなぜでしょうか？

それは、ずばり、Hardhat が Hardhat Runtime Environment（HRE） を呼び出しているからです。

HRE は、Hardhat が用意した全ての機能を含むオブジェクト（＝コードの束）です。`hardhat` で始まるターミナルコマンドを実行するたびに、HRE にアクセスしているので、`hre` を `run.js` にインポートする必要はありません。

詳しくは、[Hardhat 公式ドキュメント（英語）](https://hardhat.org/advanced/hardhat-runtime-environment.html) にて確認できます。

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
ターミナル上に `console.log` の中身とコントラクトアドレスを出力できたら、次のレッスンに進んでください🎉

<!--
🚨[次のレッスン]をクリックする前に
-------------------------------------------

*注：これを行わないと、shimuraは非常に悲しくなります：(。*

#progressに移動し、出力とともに端末のスクリーンショットを投稿します。

そのconsole.logを好きなようにしてください!これで、独自のコントラクトを作成し、ローカルブロックチェーンWOOOOOOOOOO LETSGOOOにデプロイして実行しました。-->
