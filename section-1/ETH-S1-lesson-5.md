👀 ローカル環境でスマートコントラクトをデプロイする
-------------------------------------

実際には、今まで`run.js`を実行するたび、下記が行われていました。

1. ローカル環境でイーサリアムネットワークを新規に作成する。
2. ローカル環境でコントラクトをデプロイする。
3. プログラムが終了すると、Hardhatは自動的にそのイーサリアムネットワークを削除する。

このレッスンでは、ローカル環境でイーサリアムネットワークを削除せず、**存続**させる方法を学びます。

ターミナルで、**新しい**ウィンドウを作成します。

`my-wave-portal`ディレクトに移動して、下記を実行してください。

```bash
npx hardhat node
```

ローカルネットワークでイーサリアムネットワークを立ち上げました。ターミナルの出力結果を見て、あなたにHardhatから20個のアカウント（`Account`）が提供されていること、それらすべてに`10000 ETH`が付与されていることを確認してください。

このローカルネットワークで、スマートコントラクトをデプロイしていきます。

`scripts`フォルダーの中に、 `deploy.js`というファイルを作成します。

ターミナル上で`scripts`フォルダに移動して、下記を実行しましょう。

```bash
touch deploy.js
```
`ls`というそのフォルダに入っているファイルをターミナル上に出力するコマンドがあります。実行してみてください。ターミナル上で `deploy.js`が作成されていることを確認しましょう。

 `deploy.js`に下記を記入しましょう。

```javascript
// deploy.js
const main = async () => {
	const [deployer] = await hre.ethers.getSigners();
	const accountBalance = await deployer.getBalance();
	const waveContract = await hre.ethers.getContractFactory('WavePortal');
	const wavePortal = await waveContract.deploy();

	console.log("Deploying contracts with account: ", deployer.address);
	console.log("Account balance: ", accountBalance.toString());
	console.log("Contract deployed to: ", wavePortal.address);
	console.log("Contract deployed by: ", deployer.address);
  };

  const runMain = async () => {
	try {
	  await main();
	  process.exit(0);
	} catch (error) {
	  console.error(error);
	  process.exit(1);
	}
  };

  runMain();
```

コードの中身は、`run.js`とほぼ同じです。

🎉 デプロイする
---------

新しくターミナルのウィンドウを立ち上げ、`scripts`ディレクトリに移動しましょう。

あなたのスマートコントラクトを、ローカルネットワークにデプロイするために実行するコマンドは次のとおりです。

```bash
npx hardhat run deploy.js --network localhost
```
下記のような出力結果がターミナルに表示されたでしょうか？

例）ターミナルの出力結果
```
Deploying contracts with account:  0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
Account balance:  10000000000000000000000
WavePortal address:  0x5FbDB2315678afecb367f032d93F642f64180aa3
```
このような結果があなたのターミナルに表示されていれば、あなたのスマートコントラクトは、あなたが立ち上げたローカル環境上のイーサリアムネットワークにデプロイされています。

詳しく出力結果を見ていきましょう。

```
Deploying contracts with account:  0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
```
ここには、スマートコントラクトをデプロイした人（=ここでいうあなた）のアドレスが表示されています。

```
Account balance:  10000000000000000000000
```

これは、あなたの口座に割り当てられた残高(**wei**)を表す文字列です。デフォルト値である`10000000000000000` wei (=`10000 ETH`)が表示されています。`Wei`は、イーサリアムの最小額面です。1ETH ＝ 1,000,000,000,000,000 wei です。つまり、**1weiは1,000億分の1ETH**ということになります。

```
WavePortal address:  0x5FbDB2315678afecb367f032d93F642f64180aa3
```
ここには、あなたのスマートコントラクトのデプロイ先のアドレスが表示されています。


ローカル環境上のイーサリアムネットワークを維持するもう一つのターミナルウィンドウには、下記のような出力結果が表示されているはずです。

```
  Contract deployment: WavePortal
  Contract address:    0x5fbdb2315678afecb367f032d93f642f64180aa3
  Transaction:         0x01476c51516f5d457af924f87f1d2f3803f4fad1945073215abad6c7a8aac50c
  From:                0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266
  Value:               0 ETH
  Gas used:            354975 of 354975
  Block #1:            0xbc2c2d5a605fa1d91617f9603c1312ac60918cc9271d6676b458e00a84cff2f3
```

詳しく見ていきましょう。

- `Contract deployment`: あなたのコントラクトの名前です。

- `Contract address`: ここに出力されているハッシュ値（`0x..`）は、イーサリアムネットワーク上でコントラクトがデプロイされているアドレスです。

- `Transaction`: ここに出力されているハッシュ値（`0x..`）は、取引IDとも呼ばれる、ブロックチェーンにおける取引のユニークなアドレスです。取引が行われたことの証明として機能します。

- `From`: コントラクトのオーナーであるあなたのアドレスが出力されています。あくまで`0x..`の値は、Hardhatが生成したものであることを覚えておいてください。

- `Value`: トランザクションされたETHの額です。`WavePortal`では金銭のやり取りは発生していないので、出力結果は`0`になっています。

- `Gas used`: Hardhat Networkのブロックチェーンで使用するブロックガスの上限を示しています。

- `Block #`:  あなたのローカル環境に構築されたイーサリアムネットワーク上に存在するブロックの数です。`npx hardhat run deploy.js --network localhost`をターミナルで実行するたびに、ブロックの数は増えていきます。

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
おめでとうございます🎉セクション1が終了しました。次のセクションに進みましょう！

<!--
🎁セクションのまとめ
------------------

良い!セクションの最後に到達しました。[このリンク](https://gist.github.com/adilanchian/9f745fdfa9186047e7a779c02f4bffb7)をチェックアウトして、コードが順調に進んでいることを確認してください。-->
