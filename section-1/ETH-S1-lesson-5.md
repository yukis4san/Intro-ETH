ð£ ã­ã¼ã«ã«ç°å¢ã§ã¹ãã¼ãã³ã³ãã©ã¯ããããã­ã¤ãã
-------------------------------------

å®éã«ã¯ãä»ã¾ã§ `run.js` ã§ãã¹ããè¡ããã³ãä¸è¨ãè¡ããã¦ãã¾ããã

1. ã­ã¼ã«ã«ç°å¢ã§ã¤ã¼ãµãªã¢ã ãããã¯ã¼ã¯ãæ°è¦ã«ä½æããã
2. ã­ã¼ã«ã«ç°å¢ã§ã³ã³ãã©ã¯ããããã­ã¤ããã
3. ãã­ã°ã©ã ãçµäºããã¨ãHardhat ã¯èªåçã«ãã®ã¤ã¼ãµãªã¢ã ãããã¯ã¼ã¯ãåé¤ããã

ãã®ã¬ãã¹ã³ã§ã¯ãã­ã¼ã«ã«ç°å¢ã§ã¤ã¼ãµãªã¢ã ãããã¯ã¼ã¯ãåé¤ããã**å­ç¶**ãããæ¹æ³ãå­¦ã³ã¾ãã

ã¿ã¼ããã«ã§ã**æ°ãã**ã¦ã£ã³ãã¦ãä½æãã¾ãã

`my-wave-portal` ãã£ã¬ã¯ãã«ç§»åãã¦ãä¸è¨ãå®è¡ãã¦ãã ããã

```bash
npx hardhat node
```

ããã«ãããã­ã¼ã«ã«ãããã¯ã¼ã¯ã§ã¤ã¼ãµãªã¢ã ãããã¯ã¼ã¯ãç«ã¡ä¸ããã¾ãã

ã¿ã¼ããã«ã®åºåçµæãè¦ã¦ãããªãã« Hardhat ãã 20 åã®ã¢ã«ã¦ã³ãï¼ `Account` ï¼ãæä¾ããã¦ãããã¨ãããããã¹ã¦ã« `10000 ETH` ãä»ä¸ããã¦ãããã¨ãç¢ºèªãã¦ãã ããã

ãã®ã­ã¼ã«ã«ãããã¯ã¼ã¯ã§ãã¹ãã¼ãã³ã³ãã©ã¯ããããã­ã¤ãã¦ããã¾ãã

`scripts` ãã£ã¬ã¯ããªã®ä¸­ã«ã `deploy.js` ã¨ãããã¡ã¤ã«ãä½æãã¾ãã

- `deploy.js` ã¯ãä»å¾ããªãã®æ§ç¯ãããã­ã³ãã¨ã³ãã¨ãããªãã®ã¹ãã¼ãã³ã³ãã©ã¯ãï¼ `WavePortal.sol` ï¼ãçµã³ã¤ããå½¹å²ãæããã¾ãã
- `run.js` ããã¹ãç¨ã®ãã­ã°ã©ã ãªãã`deploy.js` ã¯æ¬çªç¨ã§ãã

ããã§ã¯ãã¿ã¼ããã«ä¸ã§ `scripts` ãã£ã¬ã¯ããªã«ç§»åãã¦ãä¸è¨ãå®è¡ãã¾ãããã

```bash
touch deploy.js
```

`deploy.js` ãã¡ã¤ã«ã `scripts` ã®ä¸­ã«ä½æããã¾ãã

`ls`ãå®è¡ãã¦ã`scripts` ãã£ã¬ã¯ããªã«å¥ã£ã¦ãããã¡ã¤ã«ãã¿ã¼ããã«ä¸ã«åºåãã¾ãããã

ã¿ã¼ããã«ä¸ã§ `deploy.js`ãä½æããã¦ãããã¨ãç¢ºèªãã¦ãã ããã

ããã§ã¯ã`deploy.js` ãä¸è¨ã®ããã«æ´æ°ãã¦ããã¾ãããã

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

ã³ã¼ãã®ä¸­èº«ã¯ã`run.js` ã¨ã»ã¼åãã§ãã

ð ããã­ã¤ãã
---------

**æ°ããã¿ã¼ããã«ã®ã¦ã£ã³ãã¦ãç«ã¡ä¸ã**ã`scripts` ãã£ã¬ã¯ããªã«ç§»åãã¾ãããã

ä¸è¨ã®ã³ãã³ããå®è¡ãã¦ãããªãã®ã¹ãã¼ãã³ã³ãã©ã¯ãããã­ã¼ã«ã«ãããã¯ã¼ã¯ã«ããã­ã¤ãã¾ãããã

```bash
npx hardhat run deploy.js --network localhost
```
ä¸è¨ã®ãããªåºåçµæãã¿ã¼ããã«ã«è¡¨ç¤ºãããã§ããããï¼

```
Deploying contracts with account:  0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
Account balance:  10000000000000000000000
WavePortal address:  0x5FbDB2315678afecb367f032d93F642f64180aa3
```
ä¸è¨ã®ãããªçµæãããªãã®ã¿ã¼ããã«ã«è¡¨ç¤ºããã¦ããã°ãããã­ã¤ã¯æåã§ãð

- ããªãã®ã¹ãã¼ãã³ã³ãã©ã¯ãã¯ãã­ã¼ã«ã«ç°å¢ä¸ã®ã¤ã¼ãµãªã¢ã ãããã¯ã¼ã¯ã«ããã­ã¤ããã¾ããï¼

è©³ããåºåçµæãè¦ã¦ããã¾ãããã

```
Deploying contracts with account:  0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
```
ããã«ã¯ãã¹ãã¼ãã³ã³ãã©ã¯ããããã­ã¤ããäººï¼ï¼ããã§ããããªãï¼ã®ã¢ãã¬ã¹ãè¡¨ç¤ºããã¦ãã¾ãã

```
Account balance:  10000000000000000000000
```

ããã¯ãããªãã®å£åº§ã«å²ãå½ã¦ãããæ®é«ï¼ **wei** ï¼ãè¡¨ãæå­åã§ããããã©ã«ãå¤ã§ãã `10000000000000000 wei`ï¼ï¼ `10000 ETH` ï¼ãè¡¨ç¤ºããã¦ãã¾ãã
- `Wei` ã¯ãã¤ã¼ãµãªã¢ã ã®æå°é¡é¢ã§ãã
- `1ETH ï¼ 1,000,000,000,000,000 wei` ã§ããã¤ã¾ãã **1wei ã¯ 1,000 ååã® 1ETH** ã¨ãããã¨ã«ãªãã¾ãã

```
WavePortal address:  0x5FbDB2315678afecb367f032d93F642f64180aa3
```
ããã«ã¯ã**ããªãã®ã¹ãã¼ãã³ã³ãã©ã¯ãã®ããã­ã¤åã®ã¢ãã¬ã¹**ãè¡¨ç¤ºããã¦ãã¾ãã

**ããä¸ã¤ã®ã¿ã¼ããã«ã¦ã£ã³ãã¦**ã«ã¯ãä¸è¨ã®ãããªåºåçµæãè¡¨ç¤ºããã¦ããã¯ãã§ããç¢ºèªãã¦ã¿ã¾ãããã

```
  Contract deployment: WavePortal
  Contract address:    0x5fbdb2315678afecb367f032d93f642f64180aa3
  Transaction:         0x01476c51516f5d457af924f87f1d2f3803f4fad1945073215abad6c7a8aac50c
  From:                0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266
  Value:               0 ETH
  Gas used:            354975 of 354975
  Block #1:            0xbc2c2d5a605fa1d91617f9603c1312ac60918cc9271d6676b458e00a84cff2f3
```
**ãã®ã¿ã¼ããã«ã¦ã£ã³ãã¦ããã­ã¼ã«ã«ç°å¢ä¸ã®ã¤ã¼ãµãªã¢ã ãããã¯ã¼ã¯ãç¶­æãã¦ãã¾ãã**

åºåçµæãè©³ããè¦ã¦ããã¾ãããã

- `Contract deployment`: ããªãã®ã³ã³ãã©ã¯ãã®ååã§ãã

- `Contract address`: ããã«åºåããã¦ããããã·ã¥å¤ï¼`0x..`ï¼ã¯ãã¤ã¼ãµãªã¢ã ãããã¯ã¼ã¯ä¸ã§ã³ã³ãã©ã¯ããããã­ã¤ããã¦ããåã®ã¢ãã¬ã¹ã§ãã

- `Transaction`: ããã«åºåããã¦ããããã·ã¥å¤ï¼ `0x..` ï¼ã¯ãåå¼IDã¨ãå¼ã°ããããã­ãã¯ãã§ã¼ã³ã«ãããåå¼ã®ã¦ãã¼ã¯ãªã¢ãã¬ã¹ã§ããåå¼ãè¡ããããã¨ã®è¨¼æã¨ãã¦æ©è½ãã¾ãã

- `From`: ã³ã³ãã©ã¯ãã®ãªã¼ãã¼ã§ããããªãã®ã¢ãã¬ã¹ãåºåããã¦ãã¾ããããã¾ã§ `0x..` ã®å¤ã¯ãHardhat ãçæãããã®ã§ãããã¨ãè¦ãã¦ããã¦ãã ããã

- `Value`: ãã©ã³ã¶ã¯ã·ã§ã³ããã ETH ã®é¡ã§ãã`WavePortal` ã§ã¯éé­ã®ããåãã¯çºçãã¦ããªãã®ã§ãåºåçµæã¯ `0` ã«ãªã£ã¦ãã¾ãã

- `Gas used`: Hardhat Network ã®ãã­ãã¯ãã§ã¼ã³ã§ä½¿ç¨ãããã­ãã¯ã¬ã¹ã®ä¸éãç¤ºãã¦ãã¾ãã

- `Block #`:  ããªãã®ã­ã¼ã«ã«ç°å¢ã«æ§ç¯ãããã¤ã¼ãµãªã¢ã ãããã¯ã¼ã¯ä¸ã«å­å¨ãããã­ãã¯ã®æ°ã§ãã`npx hardhat run deploy.js --network localhost` ãã¿ã¼ããã«ã§å®è¡ãããã³ã«ããã­ãã¯ã®æ°ã¯å¢ãã¦ããã¾ãã

ðââï¸ è³ªåãã
-------------------------------------------
ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-1-help` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã®3ç¹ãè¨è¼ãã¦ãã ããâ¨
```
1. ä½ããããã¨ãã¦ããã
2. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
3. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```
----------------------------------
ããã§ã¨ããããã¾ãðã»ã¯ã·ã§ã³1ãçµäºãã¾ãããæ¬¡ã®ã»ã¯ã·ã§ã³ã«é²ã¿ã¾ãããï¼

<!--
ðã»ã¯ã·ã§ã³ã®ã¾ã¨ã
------------------

è¯ã!ã»ã¯ã·ã§ã³ã®æå¾ã«å°éãã¾ããã[ãã®ãªã³ã¯](https://gist.github.com/adilanchian/9f745fdfa9186047e7a779c02f4bffb7)ããã§ãã¯ã¢ã¦ããã¦ãã³ã¼ããé èª¿ã«é²ãã§ãããã¨ãç¢ºèªãã¦ãã ããã-->
