ð² 0.001ETHãéãã¦ã¼ã¶ã¼ãã©ã³ãã ã«é¸ã¶
-----------------------

ç¾å¨ãã³ã³ãã©ã¯ãã¯å¨ã¦ã®ã¦ã¼ã¶ã¼ã« 0.001ETH ãéãããã«è¨­å®ããã¦ãã¾ãã

ããããããã§ã¯ãã³ã³ãã©ã¯ãã¯ããã«è³éãä½¿ãæããã¦ãã¾ãã§ãããã

ãããé²ãããã«ãããããä¸è¨ã®æ©è½ã `WavePortal.sol` ã«å®è£ãã¦ããã¾ãã

```javascript
// SPDX-License-Identifier: UNLICENSED

pragma solidity ^0.8.0;

import "hardhat/console.sol";

contract WavePortal {
    uint256 totalWaves;

    /* ä¹±æ°çæã®ããã®åºç¤ã¨ãªãã·ã¼ãï¼ç¨®ï¼ãä½æ */
    uint256 private seed;

    event NewWave(address indexed from, uint256 timestamp, string message);

    struct Wave {
        address waver;
        string message;
        uint256 timestamp;
    }

    Wave[] waves;

    constructor() payable {
        console.log("We have been constructed!");
        /*
         * åæã·ã¼ããè¨­å®
         */
        seed = (block.timestamp + block.difficulty) % 100;
    }

    function wave(string memory _message) public {
        totalWaves += 1;
        console.log("%s has waved!", msg.sender);

        waves.push(Wave(msg.sender, _message, block.timestamp));

        /*
         * ã¦ã¼ã¶ã¼ã®ããã«ä¹±æ°ãçæ
         */
        seed = (block.difficulty + block.timestamp + seed) % 100;

        console.log("Random # generated: %d", seed);

        /*
         * ã¦ã¼ã¶ã¼ãETHãç²å¾ããç¢ºçã50ï¼ã«è¨­å®
         */
        if (seed <= 50) {
            console.log("%s won!", msg.sender);

            /*
             * ã¦ã¼ã¶ã¼ã«ETHãéãããã®ã³ã¼ãã¯ä»¥åã¨åã
             */
            uint256 prizeAmount = 0.0001 ether;
            require(
                prizeAmount <= address(this).balance,
                "Trying to withdraw more money than the contract has."
            );
            (bool success, ) = (msg.sender).call{value: prizeAmount}("");
            require(success, "Failed to withdraw money from contract.");
        } else {
            console.log("%s did not win.", msg.sender);
		}

        emit NewWave(msg.sender, block.timestamp, _message);
    }

    function getAllWaves() public view returns (Wave[] memory) {
        return waves;
    }

    function getTotalWaves() public view returns (uint256) {
        return totalWaves;
    }
}
```

ã³ã¼ããè¦ã¦ããã¾ãããã

```javascript
// WavePortal.sol
uint256 private seed;
```
ããã§ã¯ãä¹±æ°ãçæããããã«ä½¿ç¨ããåæã·ã¼ãï¼ä¹±æ°ã®ç¨®ï¼ãå®ç¾©ãã¦ãã¾ãã

```javascript
// WavePotal.sol
constructor() payable {
	console.log("We have been constructed!");
	/* åæã·ã¼ããè¨­å® */
	seed = (block.timestamp + block.difficulty) % 100;
}
```
ããã§ã¯ã`constructor` ã®ä¸­ã«ã¦ã¼ã¶ã¼ã®ããã«çæãããä¹±æ°ã `seed` ã«æ ¼ç´ãã¦ãã¾ãã

`block.difficulty` ã¨ `block.timestamp` ã®2ã¤ã¯ãSolidityããä¸ããããæ°å¤ã§ãã

- `block.difficulty` ã¯ããã­ãã¯æ¿èªï¼ï¼ãã¤ãã³ã°ï¼ã®é£æåº¦ããã¤ãã¼ã«éç¥ããããã®å¤ã§ãããã­ãã¯åã®ãã©ã³ã¶ã¯ã·ã§ã³ãå¤ãã»ã©ãé£æåº¦ã¯é«ããªãã¾ãã

- `block.timestamp` ã¯ããã­ãã¯ãå¦çããã¦ããæã®Unixã¿ã¤ã ã¹ã¿ã³ãã§ãã

ããã¦ã`ï¼100` ã«ãããæ°å¤ã0ã100ã®ç¯å²ã«è¨­å®ãã¦ãã¾ãã

æ¬¡ã«ä¸è¨ã®ã³ã¼ããç¢ºèªãã¾ãããã
```javascript
// WavePotal.sol
function wave(string memory _message) public {
	totalWaves += 1;
	console.log("%s has waved!", msg.sender);

	waves.push(Wave(msg.sender, _message, block.timestamp));

	/* ã¦ã¼ã¶ã¼ã®ããã«ä¹±æ°ãçæ */
	seed = (block.difficulty + block.timestamp + seed) % 100;
	:
```

ããã§ãã¦ã¼ã¶ã¼ã `wave` ãéä¿¡ãããã³ã« `seed` ãæ´æ°ãã¦ãã¾ãã

ããã«ãããã©ã³ãã æ§ã®æä¿ãè¡ã£ã¦ãã¾ããã©ã³ãã æ§ãå¼·åãããã¨ã«ãããããã«ã¼ããã®æ»æãé²ããããã«ãªãã¾ãã

æå¾ã«ä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã
```javascript
// WavePortal.sol
if (seed <= 50) {
	console.log("%s won!", msg.sender);
	:
```

ããã§ã¯ã`seed` ã®å¤ãã50ä»¥ä¸ã§ãããã©ãããç¢ºèªããããã«ã`if` ã¹ãã¼ãã¡ã³ããå®è£ãã¦ãã¾ãã

`seed` ã®å¤ã 50 ä»¥ä¸ã®å ´åãã¦ã¼ã¶ã¼ã¯ ETH ãç²å¾ãããã¨ãã§ãã¾ãã

âï¸: ä¹±æ°ããã©ã³ãã ã§ãããã¨ãã®éè¦æ§

> ãã¦ã¼ã¶ã¼ã« ETH ãã©ã³ãã ã§éå¸ãããããããªã²ã¼ã æ§ã®ãããµã¼ãã¹ã«ããã¦ãããã«ã¼ããã®æ»æãé²ããã¨ã¯å¤§å¤éè¦ã§ãã
>
> ãã­ãã¯ãã§ã¼ã³ä¸ã«ã³ã¼ãã¯å¬éããã¦ããã®ã§ãä¿¡é ¼ã§ããä¹±æ°çæã®ã¢ã«ã´ãªãºã ã¯ãæåã§ä½ãå¿è¦ãããã¾ãã
>
> ä¹±æ°ã®çæã¯ãä¸è¦é¢åã§ã¯ããã¾ãããä½ç¾ä¸äººãã®ã¦ã¼ã¶ã¼ãã¢ã¯ã»ã¹ãã dApp ãæ§ç¯ããå ´åã¯ãã¨ã¦ãéè¦ãªä½æ¥­ã¨ãªãã¾ãã

âï¸ ãã¹ããå®è¡ãã
-------

ä¸è¨ã®ããã«ã`run.js` ãæ´æ°ãã¦ãã¦ã¼ã¶ã¼ã«ã©ã³ãã ã«ETHãéããããã¹ããã¦ã¿ã¾ãããã

```javascript
// run.js
const main = async () => {
  const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
   /*
   * ããã­ã¤ããé0.1ETHãã³ã³ãã©ã¯ãã«æä¾ãã
   */
  const waveContract = await waveContractFactory.deploy({
    value: hre.ethers.utils.parseEther("0.1"),
  });
  await waveContract.deployed();
  console.log("Contract deployed to: ", waveContract.address);

  /*
   * ã³ã³ãã©ã¯ãã®ãã©ã³ã¹ãåå¾ï¼0.1ETHï¼ã§ãããã¨ãç¢ºèª
   */
  let contractBalance = await hre.ethers.provider.getBalance(
    waveContract.address
  );
  console.log(
    "Contract balance:",
    hre.ethers.utils.formatEther(contractBalance)
  );

  /*
   * 2å waves ãéãã·ãã¥ã¬ã¼ã·ã§ã³ãè¡ã
   */
  const waveTxn = await waveContract.wave("This is wave #1");
  await waveTxn.wait();

  const waveTxn2 = await waveContract.wave("This is wave #2");
  await waveTxn2.wait();

  /*
   * ã³ã³ãã©ã¯ãã®ãã©ã³ã¹ãåå¾ããWaveãåå¾ããå¾ã®çµæãåºå
   */
  contractBalance = await hre.ethers.provider.getBalance(waveContract.address);
  /*
   *å¥ç´ã®æ®é«ãã0.0001ETHå¼ããã¦ãããã¨ãç¢ºèª
   */
  console.log(
    "Contract balance:",
    hre.ethers.utils.formatEther(contractBalance)
  );

  let allWaves = await waveContract.getAllWaves();
  console.log(allWaves);
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

ããã§ã¯ãã¿ã¼ããã«ä¸ã§ `my-wave-portal` ã«ç§»åããä¸è¨ã®ã³ã¼ããå®è¡ãã¦ã¿ã¾ãããã

```
npx hardhat run scripts/run.js
```

æ¬¡ã®ãããªçµæããã¿ã¼ããã«ã«åºåãããã§ããããï¼

```bash
Compiling 1 file with 0.8.4
Solidity compilation finished successfully
We have been constructed!
Contract deployed to:  0x5FbDB2315678afecb367f032d93F642f64180aa3
Contract balance: 0.1
0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 has waved!
Random # generated: 89
0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 did not win.
0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 has waved!
Random # generated: 31
0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 won!
Contract balance: 0.0999
[
  [
    '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266',
    'This is wave #1',
    BigNumber { value: "1643887441" },
    waver: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266',
    message: 'This is wave #1',
    timestamp: BigNumber { value: "1643887441" }
  ],
  [
    '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266',
    'This is wave #2',
    BigNumber { value: "1643887442" },
    waver: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266',
    message: 'This is wave #2',
    timestamp: BigNumber { value: "1643887442" }
  ]
]
```

ä¸è¨ãè¦ã¦ã¿ã¾ãããã

ä¸äººç®ã®ã¦ã¼ã¶ã¼ã¯ãä¹±æ°ã®çµæ `89` ã¨ããå¤ãåå¾ããã®ã§ãETH ãç²å¾ãããã¨ãã§ãã¾ããã§ããã`Contract balance` ã¯ 0.1ETH ã®ã¾ã¾ã§ãã

```bash
0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 has waved!
Random # generated: 89
0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 did not win.
Contract balance: 0.1
```

æ¬¡ã«ãäºäººç®ã®ã¦ã¼ã¶ã¼ã®çµæãè¦ã¦ã¿ã¾ãããã
```
0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 has waved!
Random # generated: 31
0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 won!
Contract balance: 0.0999
```
äºäººç®ã®ã¦ã¼ã¶ã¼ã¯ãä¹±æ°ã®çµæ `31` ã¨ããå¤ãåå¾ããã®ã§ãETHãç²å¾ãã¾ããã

`Contract balance` ãã0.0999ETH ã«æ´æ°ããã¦ãããã¨ãç¢ºèªãã¦ãã ããã

ð ã¹ãã ãé²ãããã®ã¯ã¼ã«ãã¦ã³ãå®è£ãã
-----------------------------

æå¾ã«ãã¹ãã ãé²ãããã®ã¯ã¼ã«ãã¦ã³æ©è½ãå®è£ãã¦ããã¾ãã

ããã§ããã¹ãã ã¯ãããªãã®WEBã¢ããªããé£ç¶ãã¦ `wave` ãéã£ã¦ãETH ãç¨¼ããã¨ããåä½ãæå³ãã¾ãã

ããã§ã¯ãä¸è¨ã®ããã« `WavePortal.sol` ãæ´æ°ãã¾ãããã

```javascript
// SPDX-License-Identifier: UNLICENSED

pragma solidity ^0.8.0;

import "hardhat/console.sol";

contract WavePortal {
    uint256 totalWaves;
    uint256 private seed;

    event NewWave(address indexed from, uint256 timestamp, string message);

    struct Wave {
        address waver;
        string message;
        uint256 timestamp;
    }

    Wave[] waves;

    /*
     * "address => uint mapping"ã¯ãã¢ãã¬ã¹ã¨æ°å¤ãé¢é£ä»ãã
     */
    mapping(address => uint256) public lastWavedAt;

    constructor() payable {
        console.log("We have been constructed!");
        /*
         * åæã·ã¼ãã®è¨­å®
         */
        seed = (block.timestamp + block.difficulty) % 100;
    }

    function wave(string memory _message) public {
        /*
         * ç¾å¨ã¦ã¼ã¶ã¼ãwaveãéä¿¡ãã¦ããæå»ã¨ãååwaveãéä¿¡ããæå»ã15åä»¥ä¸é¢ãã¦ãããã¨ãç¢ºèªã
         */
        require(
            lastWavedAt[msg.sender] + 15 minutes < block.timestamp,
            "Wait 15m"
        );

        /*
         * ã¦ã¼ã¶ã¼ã®ç¾å¨ã®ã¿ã¤ã ã¹ã¿ã³ããæ´æ°ãã
         */
        lastWavedAt[msg.sender] = block.timestamp;

        totalWaves += 1;
        console.log("%s has waved!", msg.sender);

        waves.push(Wave(msg.sender, _message, block.timestamp));

        /*
         *  ã¦ã¼ã¶ã¼ã®ããã«ä¹±æ°ãè¨­å®
         */
        seed = (block.difficulty + block.timestamp + seed) % 100;

        if (seed <= 50) {
            console.log("%s won!", msg.sender);

            uint256 prizeAmount = 0.0001 ether;
            require(
                prizeAmount <= address(this).balance,
                "Trying to withdraw more money than they contract has."
            );
            (bool success, ) = (msg.sender).call{value: prizeAmount}("");
            require(success, "Failed to withdraw money from contract.");
        }

        emit NewWave(msg.sender, block.timestamp, _message);
    }

    function getAllWaves() public view returns (Wave[] memory) {
        return waves;
    }

    function getTotalWaves() public view returns (uint256) {
        return totalWaves;
    }
}
```

æ°ããè¿½å ããã³ã¼ããè¦ã¦ããã¾ãããã

```javascript
// WavePortal.sol
mapping(address => uint256) public lastWavedAt;
```
ããã§ã¯ã`mapping` ã¨å¼ã°ããç¹å¥ãªãã¼ã¿æ§é ãä½¿ç¨ãã¦ãã¾ãã

Solidityã® `mapping` ã¯ãä»ã®è¨èªã«ãããããã·ã¥ãã¼ãã«ãè¾æ¸ã®ãããªå½¹å²ãæããã¾ãã

ãããã¯ãä¸è¨ã®ããã« `_Key` ã¨ `_Value` ã®ãã¢ã®å½¢å¼ã§ãã¼ã¿ãæ ¼ç´ããããã«ä½¿ç¨ããã¾ãã

```solidity
mappingï¼_Key=> _Valueï¼public mappingName
```

ä»åã¯ãã¦ã¼ã¶ã¼ã®ã¢ãã¬ã¹ï¼= `_Key` = `address` ï¼ããã®ã¦ã¼ã¶ã¼ã `wave` ãéä¿¡ããæå»ï¼= `_Value` = `unit256` ï¼ã«é¢é£ä»ããããã« `mapping` ãä½¿ç¨ãã¾ããã

çè§£ãæ·±ããããã«ãæ¬¡ã®ã³ã¼ããè¦ã¦ããã¾ãããã
```javascript
// WavePortal.sol
function wave(string memory _message) public {
	/* ç¾å¨ã¦ã¼ã¶ã¼ãwaveãéä¿¡ãã¦ããæå»ã¨ãååwaveãéä¿¡ããæå»ã15åä»¥ä¸é¢ãã¦ãããã¨ãç¢ºèªã*/
	require(
		lastWavedAt[msg.sender] + 15 minutes < block.timestamp,
		"Wait 15m"
	);
```
ããã§ã¯ãWEBã¢ããªä¸ã§ç¾å¨ã¦ã¼ã¶ã¼ã `wave` ãéããã¨ãã¦ããæå»ã¨ããã®ã¦ã¼ã¶ã¼ãåå `wave` ãéã£ãæå»ãæ¯è¼ãã¦ã15åä»¥ä¸çµéãã¦ãããæ¤è¨¼ãã¦ãã¾ãã

`lastWavedAt[msg.sender]` ã®åæå¤ã¯ `0` ãªã®ã§ãã¾ã ä¸åº¦ã `wave` ãéã£ããã¨ããªãã¦ã¼ã¶ã¼ã¯ã`wave` ãéä¿¡ãããã¨ãã§ãã¾ãã

15åå¾ããã« `wave` ãéããã¨ãã¦ããã¦ã¼ã¶ã¼ã«ã¯ã`"Wait 15min"` ã¨ããã¢ã©ã¼ããè¿ãã¾ããããã«ãããã¹ãã ãé²æ­¢ãã¦ãã¾ãã

æå¾ã«ãä¸è¨ã®ã³ã¼ããç¢ºèªãã¦ãã ããã
```javascript
// WavePortal.sol
lastWavedAt[msg.sender] = block.timestamp;
```

ããã§ãã¦ã¼ã¶ã¼ã `wave` ãéã£ãæå»ãã¿ã¤ã ã¹ã¿ã³ãã¨ãã¦è¨é²ããã¾ãã

`mapping(address => uint256) public lastWavedAt` ã§ã¦ã¼ã¶ã¼ã®ã¢ãã¬ã¹ã¨ `lastWavedAt` ãç´ã¥ãã¦ããã®ã§ãããã§æ¬¡ã«åãã¦ã¼ã¶ã¼ã `wave` ãéã£ã¦ããæã«ã15åçµéãã¦ãããæ¤è¨¼ãããã¨ãã§ãã¾ãã

ð§ââï¸ ãã¹ããå®è¡ãã
------------

ã¿ã¼ããã«ä¸ã§ `my-wave-portal` ã«ç§»åããä¸è¨ãç¶ãã¦**2å**å®è¡ãã¦ã¿ã¾ãããã

```
npx hardhat run scripts/run.js
```

ä¸è¨ã®ãããªã¨ã©ã¼ãã¿ã¼ããã«ã«åºåããã¦ããã§ããããï¼
```
Error: VM Exception while processing transaction: reverted with reason string 'Wait 15m'
```

`WavePortal.sol` ã«è¨è¼ããã¦ãã `15 minutes` ã `0 minutes` ã«å¤æ´ãã`npx hardhat run scripts/run.js` ãããä¸åº¦å®è¡ããã¨ãã¨ã©ã¼ã¯ãªããªãã¾ãð

ð§ââï¸ ããã­ã¤ããï¼
------------

`deploy.js` ãæ´æ°ããå¿è¦ã¯ãªãã®ã§ãããã¾ã§ã®ããã­ã¤ã¯ä»»æã§ãã

ããªãã® WavePortal ãã©ã®ããã«æ§ç¯ãããã¯ãããªãã®èªç±ã§ãð

ããã¾ã§ã®ã¬ãã¹ã³ãåèã«ãã¦ãä¸è¨ãèªç±ã«è¨­å®ãã¦ã¿ã¾ããããããªãã ãã®WEBã¢ããªãå®æããã¦ãã ããã
- `WavePortl.sol` ã® `uint256 prizeAmount` ãæ´æ°ãã¦ãã¦ã¼ã¶ã¼ã«éã ETH ã®éé¡ãåè¨­å®ãã
- `deploy.js` ã® `hre.ethers.utils.parseEther("0.001")` ãæ´æ°ãã¦ãã³ã³ãã©ã¯ãã«æä¾ããè³éãåè¨­å®ãã
- `WavePortal.sol` ã«è¨è¼ããã¦ãã `15 minutes` ãèª¿æ´ãã¦ããããã¡æéãèª¿æ´ããï¼â»ãã¹ãã«é¢ãã¦ã¯ã`30 seconds` ãæ¨å¥¨ãã¦ãã¾ãï¼

ðââï¸ è³ªåãã
-------------------------------------------
ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-4-help` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã®3ç¹ãè¨è¼ãã¦ãã ããâ¨
```
1. ä½ããããã¨ãã¦ããã
2. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
3. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```
--------------
ãã­ã¸ã§ã¯ãã¯ã»ã¼å®æã§ããæ¬¡ã®ã¬ãã¹ã³ã«é²ã¿ã¾ãããð
