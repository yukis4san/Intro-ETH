ð¦ æ§é ä½ãä½¿ç¨ãã¦ã¡ãã»ã¼ã¸ãéåã«ä¿å­ãã
-------------------------------------------

ããã¾ã§ã®ã¬ãã¹ã³ã§ããã­ãã¯ãã§ã¼ã³ã¨éä¿¡ã§ããWEBã¢ããªãå®è£ãã¾ããã

ã¬ãã¹ã³ã®æå¾ã«ãæ¬¡ã®æ©è½ãå®è£ãã¾ãã

1. ã¦ã¼ã¶ã¼ã¯ãðï¼waveï¼ãã¨ä¸ç·ã«ã¡ãã»ã¼ã¸ãéä¿¡ããã

2. ãã®ãã¼ã¿ããã­ãã¯ãã§ã¼ã³ã«ä¿å­ããã

3. WEBã¤ãã«ãã®ãã¼ã¿ãè¡¨ç¤ºããã

ããã§ã¯ã`WavePortal.sol` ãæ´æ°ãã¦ããã¾ãã

```javascript
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.4;
import "hardhat/console.sol";
contract WavePortal {
    uint256 totalWaves;
    /*
    * NewWaveã¤ãã³ãã®ä½æ
    */
    event NewWave(address indexed from, uint256 timestamp, string message);
    /*
    * Waveã¨ããæ§é ä½ãä½æã
    * æ§é ä½ã®ä¸­èº«ã¯ãã«ã¹ã¿ãã¤ãºãããã¨ãã§ãã¾ãã
    */
    struct Wave {
        address waver; //ãðï¼waveï¼ããéã£ãã¦ã¼ã¶ã¼ã®ã¢ãã¬ã¹
        string message; // ã¦ã¼ã¶ã¼ãéã£ãã¡ãã»ã¼ã¸
        uint256 timestamp; // ã¦ã¼ã¶ã¼ããðï¼waveï¼ããéã£ãç¬éã®ã¿ã¤ã ã¹ã¿ã³ã
    }
    /*
    * æ§é ä½ã®éåãæ ¼ç´ããããã®å¤æ°wavesãå®£è¨ã
    * ããã§ãã¦ã¼ã¶ã¼ãéã£ã¦ãããã¹ã¦ã®ãðï¼waveï¼ããä¿æãããã¨ãã§ãã¾ãã
    */
    Wave[] waves;
    constructor() {
        console.log("WavePortal - Smart Contract!");
    }
    /*
    * _messageã¨ããæå­åãè¦æ±ããããã«waveé¢æ°ãæ´æ°ã
    * _messageã¯ãã¦ã¼ã¶ã¼ããã­ã³ãã¨ã³ãããéä¿¡ããã¡ãã»ã¼ã¸ã§ãã
    */
    function wave(string memory _message) public {
        totalWaves += 1;
        console.log("%s waved w/ message %s", msg.sender, _message);
        /*
         * ãðï¼waveï¼ãã¨ã¡ãã»ã¼ã¸ãéåã«æ ¼ç´ã
         */
        waves.push(Wave(msg.sender, _message, block.timestamp));
        /*
         * ã³ã³ãã©ã¯ãå´ã§emitãããã¤ãã³ãã«é¢ããéç¥ããã­ã³ãã¨ã³ãã§åå¾ã§ããããã«ããã
         */
        emit NewWave(msg.sender, block.timestamp, _message);
    }
    /*
     * æ§é ä½éåã®wavesãè¿ãã¦ãããgetAllWavesã¨ããé¢æ°ãè¿½å ã
     * ããã§ãç§ãã¡ã®WEBã¢ããªããwavesãåå¾ãããã¨ãã§ãã¾ãã
     */
    function getAllWaves() public view returns (Wave[] memory) {
        return waves;
    }
    function getTotalWaves() public view returns (uint256) {
        // ã³ã³ãã©ã¯ããåºåããå¤ãã³ã³ã½ã¼ã«ã­ã°ã§è¡¨ç¤ºããã
        console.log("We have %d total waves!", totalWaves);
        return totalWaves;
    }
}
```

ä¸è¨ã®æ´æ°ã§ãã¤ã³ãã¨ãªã£ã¦ããã®ããã¤ãã³ãã®ä½æã§ãã

**â±: ã¤ãã³ãã¨ `emit`**

ä»åã®å®è£ã¯ã`NewWave` ã®ã¤ãã³ãã `emit` ããããã¨ã«ãã³ã³ãã©ã¯ãã«æ¸ãè¾¼ã¾ãããã¼ã¿ãWEBã¢ããªã®ãã­ã³ãã¨ã³ãã«åæ ããããã¨ãç®çã¨ãã¦ãã¾ãã

ä¸è¨ã®ã³ã¼ãã«æ³¨ç®ãã¦ãã ããã

```solidity
// WavePortal.sol
event NewWave(address indexed from, uint256 timestamp, string message);
```

ããã§ã¯ã`NewWave` ã¤ãã³ããå®ç¾©ããã¦ãã¾ããå¼æ°ã¨ãã¦åãå¤ã¯ãä¸è¨ã«ãªãã¾ãã
- ã¦ã¼ã¶ã¼ã®ã¢ãã¬ã¹ï¼ `address` ï¼
- ã¦ã¼ã¶ã¼ã `wave` ãã¦ããæå»ï¼ `timestamp` ï¼
- ã¦ã¼ã¶ã¼ã®ã¡ãã»ã¼ã¸ï¼ `message` ï¼

æ¬¡ã«ä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã

```solidity
// WavePortal.sol
emit NewWave(msg.sender, block.timestamp, _message);
```

ã³ã³ãã©ã¯ãã§ã¤ãã³ãã `emit` ãããã¨ããã­ã³ãã¨ã³ãï¼ `App.js` ï¼ã§ãã®æå ±ãåãåãã¾ãã
`NewWave` ã¤ãã³ã ã `emit` ãããéããã­ã³ãã¨ã³ãï¼ `App.js` ï¼ã§ä½¿ç¨ããå¤æ° `msg.sender`, `block.timestamp`, `_message` ããã­ã³ãã¨ã³ãã«éä¿¡ãã¦ãã¾ãã

æ¬¡ã«ã`App.js` ã®ä¸­ã«ãã `getAllWaves` é¢æ°ã `NewWave` ã®ã¤ãã³ããåãåããããã«å¤æ´ãã¦ããã¾ãã

```javascript
// App.js
const getAllWaves = async () => {
	const { ethereum } = window;

	try {
	  if (ethereum) {
		const provider = new ethers.providers.Web3Provider(ethereum);
		const signer = provider.getSigner();
		const wavePortalContract = new ethers.Contract(contractAddress, contractABI, signer);
	  /* ã³ã³ãã©ã¯ãããgetAllWavesã¡ã½ãããå¼ã³åºã */
		const waves = await wavePortalContract.getAllWaves();
    /* UIã«å¿è¦ãªã®ã¯ãã¢ãã¬ã¹ãã¿ã¤ã ã¹ã¿ã³ããã¡ãã»ã¼ã¸ã ããªã®ã§ãä»¥ä¸ã®ããã«è¨­å® */
		const wavesCleaned = waves.map(wave => {
		  return {
			address: wave.waver,
			timestamp: new Date(wave.timestamp * 1000),
			message: wave.message,
		  };
		});

    /* React Stateã«ãã¼ã¿ãæ ¼ç´ãã */
		setAllWaves(wavesCleaned);
	  } else {
		console.log("Ethereum object doesn't exist!");
	  }
	} catch (error) {
	  console.log(error);
	}
  };

  /**
   * `emit`ãããã¤ãã³ãã«åå¿ãã
   */
  useEffect(() => {
	let wavePortalContract;

	const onNewWave = (from, timestamp, message) => {
	  console.log("NewWave", from, timestamp, message);
	  setAllWaves(prevState => [
		...prevState,
		{
		  address: from,
		  timestamp: new Date(timestamp * 1000),
		  message: message,
		},
	  ]);
	};

  /* NewWaveã¤ãã³ããã³ã³ãã©ã¯ãããçºä¿¡ãããã¨ãã«ãæå ±ããåãåãã¾ã */
  if (window.ethereum) {
    const provider = new ethers.providers.Web3Provider(window.ethereum);
    const signer = provider.getSigner();

    wavePortalContract = new ethers.Contract(contractAddress, contractABI, signer);
    wavePortalContract.on("NewWave", onNewWave);
  }
  /*ã¡ã¢ãªãªã¼ã¯ãé²ãããã«ãNewWaveã®ã¤ãã³ããè§£é¤ãã¾ã*/
  return () => {
    if (wavePortalContract) {
    wavePortalContract.off("NewWave", onNewWave);
    }
  };
  }, []);
```

ä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã

```javascript
// App.js
const onNewWave = (from, timestamp, message) => {
  console.log("NewWave", from, timestamp, message);
  setAllWaves(prevState => [
  ...prevState,
  {
    address: from,
    timestamp: new Date(timestamp * 1000),
    message: message,
  },
  ]);
};
```
`onNewWave` é¢æ°ã§ã¯ãä¸è¨2ã¤ã®åä½ãå®è¡ãã¦ãã¾ãã

1 \. ã³ã³ãã©ã¯ãå´ã§æ°ãã `NewWave` ã¤ãã³ãã `emit` ãããæãä¸è¨ã®æå ±ãåå¾ããã

- `sender` ã®ã¢ãã¬ã¹

- `sender` ã `NewWave` ã `emit` ããã¨ãã®ã¿ã¤ã ã¹ã¿ã³ã

- `message` ã®åå®¹

ä¸è¨ã®ã³ã¼ããå®è£ãããã¨ã«ããããã­ã³ãã¨ã³ããããããã®ãã¼ã¿ã«ã¢ã¯ã»ã¹ã§ããããã«ãªãã¾ãã

2 \. `NewWave` ã¤ãã³ãããã­ã³ãã¨ã³ããåãåã£ãã¨ãã« `setAllWaves` ãå®è¡ããã
- `NewWave` ã¤ãã³ãã `emit` ãããéã«ãä¸è¨ã§åå¾ããã¦ã¼ã¶ã¼ã«é¢ãã3ã¤ã®æå ±ã `allWaves` éåã«è¿½å ãããã
- ããã«ãããWEBã¢ããªã®ãã­ã³ãã¨ã³ãã«åæ ãããã¼ã¿ãèªåã§æ´æ°ã§ããããã«ãªãã¾ãã

ãã® `onNewWave` é¢æ°ã¯ã`NewWave` ã®ã¤ãã³ããªã¹ãã¼ã®åãããã¦ãã¾ãã

- ã¤ãã³ããªã¹ãã¼ã¨ã¯ããã¼ã¸ãè¡¨ç¤ºãããããããã¿ã³ãã¯ãªãã¯ããããªã©ã®åä½ã®ãã¨ãè¡¨ãã¾ããããã§ã¯ãããã­ã³ãã¨ã³ãã§ã¦ã¼ã¶ã¼ã `wave` ãéã£ããåä½ãåãåãã¾ãã

- Javascriptã§ã¯ããã­ã³ãã¨ã³ãã§ã¤ãã³ããçºçããéã«åä½ããããã«å¯¾å¿ä»ãã¦ãããé¢æ°ã®ãã¨ããã¤ãã³ããªã¹ãã¼ãã¨å¼ã³ã¾ãã

æ¬¡ã«ãä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã
```javascript
if (window.ethereum) {
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  const signer = provider.getSigner();

  wavePortalContract = new ethers.Contract(contractAddress, contractABI, signer);
  /* ããã«æ³¨ç® */
  wavePortalContract.on("NewWave", onNewWave);
}
```

`wavePortalContract.on("NewWave", onNewWave)`ã«ãããä¸è¨ã§å®ç¾©ãã`onNewWave`ãå¼ã³åºããã¾ãã

æå¾ã«ä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã
```javascript
// App.js
return () => {
  if (wavePortalContract) {
  /* ããã«æ³¨ç® */
  wavePortalContract.off("NewWave", onNewWave);
  }
};
}, []);
```

`wavePortalContract.on("NewWave", onNewWave)` ã«ããããã­ã³ãã¨ã³ãã¯ã`NewWave` ã¤ãã³ããã³ã³ãã©ã¯ãããçºä¿¡ãããã¨ãã«ãæå ±ãåãåãã¾ããããã«ãããæå ±ããã­ã³ãã¨ã³ãã«åæ ããã¾ãã

ãã®ãã¨ãã**ã³ã³ãã¼ãã³ãï¼æå ±ï¼ããã¦ã³ãï¼ãã­ã³ãã¨ã³ãã«åæ ï¼ããã**ã¨è¨ãã¾ãã

ã³ã³ãã¼ãã³ãããã¦ã³ããããç¶æããã®ã¾ã¾ã«ãã¦ããã¨ãã¡ã¢ãªãªã¼ã¯ï¼ã³ã³ãã¥ã¼ã¿ãåä½ããã¦ããåã«ãä½¿ç¨å¯è½ãªã¡ã¢ãªã®å®¹éãæ¸ã£ã¦ãã£ã¦ãã¾ãç¾è±¡ï¼ãçºçããå¯è½æ§ãããã¾ãã

ã¡ã¢ãªãªã¼ã¯ãé²ãããã«ã`wavePortalContract.off("NewWave", onNewWave)` ã§ã¯ã`onNewWave` é¢æ°ã®ç¨¼åãæ­¢ãã¦ãã¾ããããã¯ãã¤ãã³ããªã¹ãã¼ãæ­¢ãããã¨ãæå³ãã¦ãã¾ãã

ð§ ãã¹ããå®è¡ãã
----------

`WavePortal.sol` ã³ã³ãã©ã¯ããå¤æ´ããã®ã§ã`run.js` ãæ´æ°ãããã¹ããè¡ãã¾ãã

ä¸è¨ã®ããã« `run.js` ãæ´æ°ãã¦ãã ããã

```javascript
// run.js
const main = async () => {
  const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
  const waveContract = await waveContractFactory.deploy();
  await waveContract.deployed();
  console.log("Contract addy:", waveContract.address);
  let waveCount;
  waveCount = await waveContract.getTotalWaves();
  console.log(waveCount.toNumber());
  /**
   * ãðï¼waveï¼ããéã
   */
  let waveTxn = await waveContract.wave("A message!");
  await waveTxn.wait(); // ãã©ã³ã¶ã¯ã·ã§ã³ãæ¿èªãããã®ãå¾ã¤ï¼ãã¹ã:1åç®ï¼
  const [_, randomPerson] = await hre.ethers.getSigners();
  waveTxn = await waveContract.connect(randomPerson).wave("Another message!");
  await waveTxn.wait(); // ãã©ã³ã¶ã¯ã·ã§ã³ãæ¿èªãããã®ãå¾ã¤ï¼ãã¹ã:2åç®ï¼
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

`run.js` ãæ´æ°ããããã¿ã¼ããã«ä¸ã§ `my-wave-portal` ã«ç§»åããä¸è¨ãå®è¡ãã¾ãã

```
npx hardhat run scripts/run.js
```

ä¸è¨ã®ãããªçµæãã¿ã¼ããã«ã«è¡¨ç¤ºããã¦ããã°ãã¹ãã¯æåã§ãã

```bash
Compiling 1 file with 0.8.4
Solidity compilation finished successfully
WavePortal - Smart Contract!
Contract addy: 0x5FbDB2315678afecb367f032d93F642f64180aa3
We have 0 total waves!
0
0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 waved w/ message A message!
0x70997970c51812dc3a010c7d01b50e0d17dc79c8 waved w/ message Another message!
[
  [
    '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266',
    'A message!',
    BigNumber { value: "1643724588" },
    waver: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266',
    message: 'A message!',
    timestamp: BigNumber { value: "1643724588" }
  ],
  [
    '0x70997970C51812dc3A010C7d01b50e0d17dc79C8',
    'Another message!',
    BigNumber { value: "1643724589" },
    waver: '0x70997970C51812dc3A010C7d01b50e0d17dc79C8',
    message: 'Another message!',
    timestamp: BigNumber { value: "1643724589" }
  ]
]
```

æ³¨ï¼ãã¿ã¤ã ã¹ã¿ã³ããã¯ããBigNumberãã¨ãã¦åºåããã¦ãã¾ãããBigNumberãã«ã¤ãã¦ã¯ã[ãã¡ã](https://qiita.com/niharu/items/52ee466c37c701f9109b)
ãåç§ãã¦ãã ããã

ð© ããä¸åº¦ããã­ã¤ãã
------------

ã³ã³ãã©ã¯ããæ´æ°ããã®ã§ãä¸è¨ãå®è¡ããå¿è¦ãããã¾ãã

1. ååº¦ã³ã³ãã©ã¯ããããã­ã¤ãã

2. ãã­ã³ãã¨ã³ãã®å¥ç´ã¢ãã¬ã¹ãæ´æ°ããï¼æ´æ°ãããã¡ã¤ã«: `App.js` ï¼

3. ãã­ã³ãã¨ã³ãã®ABIãã¡ã¤ã«ãæ´æ°ããï¼æ´æ°ãããã¡ã¤ã«: `your-first-dApp/src/utils/WavePortal.json` ï¼

**ã³ã³ãã©ã¯ããæ´æ°ãããã³ããããã®3ã¤ã®ã¹ããããå®è¡ããå¿è¦ãããã¾ãã**

**âï¸: ä¸è¨3ã¤ã®ã¹ããããå¿è¦ãªçç±**
> ãã°ããã¹ãã¼ãã³ã³ãã©ã¯ãã¯ä¸åº¦ããã­ã¤ãããã¨**å¤æ´ãããã¨ãã§ããªã**ããã§ãã
>
> ã³ã³ãã©ã¯ããæ´æ°ããããã«ã¯ãåã³ããã­ã¤ããå¿è¦ãããã¾ãã
>
> åã³ããã­ã¤ãããã³ã³ãã©ã¯ãã¯ãå®å¨ã«æ°ããã³ã³ãã©ã¯ãã¨ãã¦æ±ãããããããã¹ã¦ã®å¤æ°ã¯**ãªã»ãã**ããã¾ãã
>
> **ã¤ã¾ããã³ã³ãã©ã¯ããä¸åº¦æ´æ°ãã¦ãã¾ãã¨ããã¹ã¦ã®æ¢å­ã®ãðï¼waveï¼ããã¼ã¿ãå¤±ããã¾ãã**

ããã§ã¯ãå¾©ç¿ãå¼ã­ã¦ãä¸è¨ãå®è¡ãã¦ããã¾ãããã

**1 \. ã¿ã¼ããã«ä¸ã§ `my-wave-portal` ã«ç§»åããä¸è¨ãå®è¡ããã³ã³ãã©ã¯ããååº¦ããã­ã¤ããã**
```
npx hardhat run scripts/deploy.js --network rinkeby
```

ã¿ã¼ããã«ã«ä¸è¨ã®ãããªåºåçµæãè¡¨ç¤ºããã¦ããã°ãããã­ã¤ã¯æåã§ãã
```
Deploying contracts with account:  0x821d451FB0D9c5de6F818d700B801a29587C3dCa
Account balance:  333733007254181125
WavePortal address:  0x8B1D31bFBf34dBF12c73034215752261e55b443c
```

**2 \. `App.js` ã® `contractAddress` ããã¿ã¼ããã«ã§åå¾ããæ°ããã³ã³ãã©ã¯ãã¢ãã¬ã¹ã«å¤æ´ãã¾ãã**

ä¸è¨ã®ããã«ãã¿ã¼ããã«ã«åºåãããã³ã³ãã©ã¯ãã¢ãã¬ã¹ï¼ `0x..` ï¼ãã³ãã¼ãã¾ãããã

```
WavePortal address: 0x... â ããªãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãã³ãã¼
```

ã³ãã¼ããã¢ãã¬ã¹ã `App.js` ã® `const contractAddress = "ãã¡ã"` ã«è²¼ãä»ãã¾ãããã

**3 \. ä»¥åã¨åãããã« `artifacts` ããABIãã¡ã¤ã«ãåå¾ãã¾ããä¸è¨ã®ã¹ããããå®è¡ãã¦ãã ããã**

1. ã¿ã¼ããã«ä¸ã§ `my-wave-portal` ã«ãããã¨ãç¢ºèªããï¼ãããã¯ç§»åããï¼ã
2. ã¿ã¼ããã«ä¸ã§ä¸è¨ãå®è¡ããã
> ```
> code artifacts/contracts/WavePortal.sol/WavePortal.json
> ```
3. VS Codeã§ `WavePortal.json` ãã¡ã¤ã«ãéãããã®ã§ãä¸­èº«ãå¨ã¦ã³ãã¼ãã¾ãããã

	â» VS Codeã®ãã¡ã¤ã³ãã¼ãä½¿ã£ã¦ãç´æ¥ `WavePortal.json` ãéããã¨ãå¯è½ã§ãã

4. ã³ãã¼ãã `my-wave-portal/artifacts/contracts/WavePortal.sol/WavePortal.json` ã®ä¸­èº«ãæ°ããä½æãã `your-first-dApp/src/utils/WavePortal.json` ã®ä¸­ã«è²¼ãä»ãã¦ãã ããã

**ç¹°ãè¿ãã¾ãããã³ã³ãã©ã¯ããæ´æ°ãããã³ã«ãã®ä½æ¥­ãè¡ãå¿è¦ãããã¾ãã**

ð WEBã¢ããªã«ã³ã³ãã©ã¯ãã®å¤æ´ãåæ ããã
----------------------------------

ä¸è¨ã®ããã« `App.js` ãæ´æ°ãã¾ãããã

æ°ããå®è£ããæ©è½ã¯ä»¥ä¸ã®ã¤ã§ãã
1. ã¦ã¼ã¶ã¼ã¯ãðï¼waveï¼ãã¨ä¸ç·ã«ã¡ãã»ã¼ã¸ãéä¿¡ããã

2. ãã®ãã¼ã¿ããã­ãã¯ãã§ã¼ã³ã«ä¿å­ããã

3. WEBã¤ãã«ãã®ãã¼ã¿ãè¡¨ç¤ºããã

```javascript
// App.js
import React, { useEffect, useState } from "react";
import "./App.css";
/* ethers å¤æ°ãä½¿ããããã«ãã*/
import { ethers } from "ethers";
/* ABIãã¡ã¤ã«ãå«ãWavePortal.jsonãã¡ã¤ã«ãã¤ã³ãã¼ããã*/
import abi from "./utils/WavePortal.json";

const App = () => {
  /* ã¦ã¼ã¶ã¼ã®ãããªãã¯ã¦ã©ã¬ãããä¿å­ããããã«ä½¿ç¨ããç¶æå¤æ°ãå®ç¾© */
  const [currentAccount, setCurrentAccount] = useState("");
  /* ã¦ã¼ã¶ã¼ã®ã¡ãã»ã¼ã¸ãä¿å­ããããã«ä½¿ç¨ããç¶æå¤æ°ãå®ç¾© */
  const [messageValue, setMessageValue] = useState("")
  /* ãã¹ã¦ã®wavesãä¿å­ããç¶æå¤æ°ãå®ç¾© */
  const [allWaves, setAllWaves] = useState([]);
  console.log("currentAccount: ", currentAccount);
  /* ããã­ã¤ãããã³ã³ãã©ã¯ãã®ã¢ãã¬ã¹ãä¿æããå¤æ°ãä½æ */
  const contractAddress = "0x8B1D31bFBf34dBF12c73034215752261e55b443c";
  /* ã³ã³ãã©ã¯ããããã¹ã¦ã®wavesãåå¾ããã¡ã½ãããä½æ */
  /* ABIã®åå®¹ãåç§ããå¤æ°ãä½æ */
  const contractABI = abi.abi;

  const getAllWaves = async () => {
    const { ethereum } = window;

    try {
      if (ethereum) {
      const provider = new ethers.providers.Web3Provider(ethereum);
      const signer = provider.getSigner();
      const wavePortalContract = new ethers.Contract(contractAddress, contractABI, signer);
        /* ã³ã³ãã©ã¯ãããgetAllWavesã¡ã½ãããå¼ã³åºã */
      const waves = await wavePortalContract.getAllWaves();
          /* UIã«å¿è¦ãªã®ã¯ãã¢ãã¬ã¹ãã¿ã¤ã ã¹ã¿ã³ããã¡ãã»ã¼ã¸ã ããªã®ã§ãä»¥ä¸ã®ããã«è¨­å® */
      const wavesCleaned = waves.map(wave => {
        return {
        address: wave.waver,
        timestamp: new Date(wave.timestamp * 1000),
        message: wave.message,
        };
      });
          /* React Stateã«ãã¼ã¿ãæ ¼ç´ãã */
      setAllWaves(wavesCleaned);
      } else {
      console.log("Ethereum object doesn't exist!");
      }
    } catch (error) {
      console.log(error);
    }
    };

    /**
     * `emit`ãããã¤ãã³ãããã­ã³ãã¨ã³ãã«åæ ããã
     */
    useEffect(() => {
    let wavePortalContract;

    const onNewWave = (from, timestamp, message) => {
      console.log("NewWave", from, timestamp, message);
      setAllWaves(prevState => [
      ...prevState,
      {
        address: from,
        timestamp: new Date(timestamp * 1000),
        message: message,
      },
      ]);
    };
    /* NewWaveã¤ãã³ããã³ã³ãã©ã¯ãããçºä¿¡ãããã¨ãã«ãæå ±ããåãåãã¾ã */
    if (window.ethereum) {
      const provider = new ethers.providers.Web3Provider(window.ethereum);
      const signer = provider.getSigner();

      wavePortalContract = new ethers.Contract(contractAddress, contractABI, signer);
      wavePortalContract.on("NewWave", onNewWave);
    }
    /*ã¡ã¢ãªãªã¼ã¯ãé²ãããã«ãNewWaveã®ã¤ãã³ããè§£é¤ãã¾ã*/
    return () => {
      if (wavePortalContract) {
      wavePortalContract.off("NewWave", onNewWave);
      }
    };
    }, []);

  /* window.ethereumã«ã¢ã¯ã»ã¹ã§ãããã¨ãç¢ºèª */
  const checkIfWalletIsConnected = async () => {
    try {
      const { ethereum } = window;
      if (!ethereum) {
        console.log("Make sure you have metamask!");
        return;
      } else {
        console.log("We have the ethereum object", ethereum);
      }
      /* ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¸ã®ã¢ã¯ã»ã¹ãè¨±å¯ããã¦ãããã©ãããç¢ºèª */
      const accounts = await ethereum.request({ method: "eth_accounts" });
      if (accounts.length !== 0) {
        const account = accounts[0];
        console.log("Found an authorized account:", account);
        setCurrentAccount(account)
        getAllWaves();
      } else {
        console.log("No authorized account found")
      }
    } catch (error) {
      console.log(error);
    }
  }
  /* connectWalletã¡ã½ãããå®è£ */
  const connectWallet = async () => {
    try {
      const { ethereum } = window;
      if (!ethereum) {
        alert("Get MetaMask!");
        return;
      }
      const accounts = await ethereum.request({ method: "eth_requestAccounts" });
      console.log("Connected: ", accounts[0]);
      setCurrentAccount(accounts[0]);
    } catch (error) {
      console.log(error)
    }
  }
  /* waveã®åæ°ãã«ã¦ã³ãããé¢æ°ãå®è£ */
  const wave = async () => {
    try {
      const { ethereum } = window;
      if (ethereum) {
        const provider = new ethers.providers.Web3Provider(ethereum);
        const signer = provider.getSigner();
        /* ABIãåç§ */
        const wavePortalContract = new ethers.Contract(contractAddress, contractABI, signer);
        let count = await wavePortalContract.getTotalWaves();
        console.log("Retrieved total wave count...", count.toNumber());
        /* ã³ã³ãã©ã¯ãã«ðï¼waveï¼ãæ¸ãè¾¼ã */
        const waveTxn = await wavePortalContract.wave(messageValue,{gasLimit:300000})
        console.log("Mining...", waveTxn.hash);
        await waveTxn.wait();
        console.log("Mined -- ", waveTxn.hash);
        count = await wavePortalContract.getTotalWaves();
        console.log("Retrieved total wave count...", count.toNumber());
      } else {
        console.log("Ethereum object doesn't exist!");
      }
    } catch (error) {
      console.log(error)
    }
  }

  /* WEBãã¼ã¸ãã­ã¼ããããã¨ãã«ä¸è¨ã®é¢æ°ãå®è¡ */
  useEffect(() => {
    checkIfWalletIsConnected();
  }, [])

  return (
    <div className="mainContainer">
      <div className="dataContainer">
        <div className="header">
        <span role="img" aria-label="hand-wave">ð</span> ããããï¼
        </div>
        <div className="bio">
          ã¤ã¼ãµãªã¢ã ã¦ã©ã¬ãããæ¥ç¶ãã¦ãã¡ãã»ã¼ã¸ãä½æãããã<span role="img" aria-label="hand-wave">ð</span>ãéã£ã¦ãã ãã<span role="img" aria-label="shine">â¨</span>
        </div>
        <br></br>
        {/* ã¦ã©ã¬ããã³ãã¯ãã®ãã¿ã³ãå®è£ */}
        {!currentAccount && (
        <button className="waveButton" onClick={connectWallet} >
            Connect Wallet
        </button>
        )}
        {currentAccount && (
        <button className="waveButton">
            Wallet Connected
        </button>
        )}
        {/* waveãã¿ã³ã«waveé¢æ°ãé£å */}
        {currentAccount && (
        <button className="waveButton" onClick={wave}>
          Wave at Me
        </button>)
        }
        {/* ã¡ãã»ã¼ã¸ããã¯ã¹ãå®è£*/}
        {currentAccount && (<textarea name="messageArea"
            placeholder="ã¡ãã»ã¼ã¸ã¯ãã¡ã"
            type="text"
            id="message"
            value={messageValue}
            onChange={e => setMessageValue(e.target.value)} />)
        }
        {/* å±¥æ­´ãè¡¨ç¤ºãã */}
        {currentAccount && (
        allWaves.slice(0).reverse().map((wave, index) => {
          return (
            <div key={index} style={{ backgroundColor: "#F8F8FF", marginTop: "16px", padding: "8px" }}>
              <div>Address: {wave.address}</div>
              <div>Time: {wave.timestamp.toString()}</div>
              <div>Message: {wave.message}</div>
            </div>)
        })
        )}
      </div>
    </div>
  );
  }
export default App
```

ä¸è¨ã§å®è£ããæ©è½ãè©³ããè¦ã¦ããã¾ãããã

**1 \. WEBã¢ããªããã¡ãã»ã¼ã¸ãåãåã**

ä¸è¨ãReactNodeãè¿ãé¢æ°å `App` ã®ä¸­ã«å®è£ãã¾ããã

```javascript
// App.js
const [messageValue, setMessageValue] = useState("")
```
ããã§ã¯ãã¦ã¼ã¶ã¼ã®ã¡ãã»ã¼ã¸ãä¿å­ããããã«ä½¿ç¨ããç¶æå¤æ°ãå®ç¾©ãã¦ãã¾ãã

`useState` ã¯åæç¶æãåãåãã2ã¤ã®å¤ãè¿ãã¾ãã
- ç¾å¨ã®ç¶æï¼ï¼ `messageValue` ï¼
- ç¾å¨ã®ç¶æãæ´æ°ããé¢æ°ï¼ï¼ `setMessageValue` ï¼

ãããã `getAllWaves` é¢æ°ã®ä¸­ã«ä¸è¨ãå®è£ãã¦ãWEBã¢ããªããã¢ãã¬ã¹ãã¿ã¤ã ã¹ã¿ã³ããã¡ãã»ã¼ã¸ãåå¾ã§ããããã«ãã¦ãã¾ãã

è©³ããè¦ã¦ããã¾ãããã
>```javascript
> // App.js
>const wavesCleaned = waves.map(wave => {
>   return {
>   address: wave.waver,
>   timestamp: new Date(wave.timestamp * 1000),
>   message: wave.message,
>   };
>});
>setAllWaves(wavesCleaned);
>```

>ããã§ã¯ç¶æå¤æ°ï¼ï¼ `waveCleaned` ï¼ãå®£è¨ãããã®å¤ãåæåãã¦ãã¾ãã
>
> ããããã[mapã¡ã½ãã](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/map) ãä½¿ã£ã¦ã`wavesCleaned` å¤æ°ã«ãã¼ã¿ãè¿½å ãã¦ãã¾ãã
>
> `map` ã¡ã½ããã¯ãåã¨ãªãéåããæ°ããéåãä½ãããã®ã¡ã½ããã§ããéåã®ãã¹ã¦ã®è¦ç´ ã«å¯¾ãã¦ãä¸ããããé¢æ°ãå®è¡ããé¢æ°ã§è¿ãããå¤ã§æ°ããéåãçæãã¾ãã
>
> `map` ã¡ã½ããã«ãã£ã¦ä¸è¨ã®ãã¼ã¿ãã`wavesCleaned` ã«æ ¼ç´ããã¾ãã
> - `wave`ããã¦ã¼ã¶ã¼ã®ã¢ãã¬ã¹ï¼ï¼ `address` ï¼
> - éä¿¡ããæéï¼ï¼ `timestamp` ï¼
> - ä»éããã¡ãã»ã¼ã¸ï¼ï¼ `message` ï¼
>
> æå¾ã«ã`AllWaves` ã®ç¶æãæ´æ°ãã¦ãã¾ãã
> ```javascript
> // App.js
>setAllWaves(wavesCleaned);
> ```
> ããã§ãæ°ãã `wave` ã®æå ±ã `waves` å¤æ°ã«æ°ããªéåã¨ãã¦è¿½å ããã¾ãã
>

**â½ï¸: ã¬ã¹ãªãããï¼`gasLimit`ï¼ã®è¨­å®**

> ä¸è¨ãå®è£ãã¦ããã©ã³ã¶ã¯ã·ã§ã³ã«ä½¿ç¨ã§ããã¬ã¹ä»£ï¼ï¼`gasLimit`ï¼ã«å¶éãè¨­ãã¦ãã¾ãã
>
>```javascript
> // App.js
>wavePortalContract.wave(message, { gasLimit: 300000 })
>```
> `gasLimit` ã¯ããã¬ã¹éãã®æå¤§å¤ï¼ä¸éï¼ãè¨­å®ããããã®ãã©ã¡ã¼ã¿ã§ãã
>
> ããã¯ãééåã®ãã­ã°ã©ã ã®åé¡ãªã©ã§ããã£ã¨å¦çãå®è¡ããç¶ãã¦ãééææ°æã®æ¯æããç¡éã«çºçããï¼ãã¬ã¹éããç¡éã«å¤§ãããªãï¼ãã¨ãé²ãããã®ãã®ã§ãã
>
> ã¬ã¹éãã¬ã¹ãªãããã§è¨­å®ãããæ°å¤ä»¥ä¸ã«ãªã£ãå ´åã¯å¦çãä¸­æ­ãã¦ãããä»¥ä¸ã®ééææ°æãçºçããªããããªä»çµã¿ã«ãªã£ã¦ãã¾ãã
>
> ã¤ã¾ããééææ°æã¨ãã¦æ¯æãæå¤§å¤ï¼ä¸éï¼ã¯ãä¸è¨ã®ããã«ãªãã¾ãã
> ```
> æå¤§ééææ°æï¼ETHï¼ = ã¬ã¹ä¾¡æ ¼ Ã ã¬ã¹ãªããã
>```
>
> ä»åã¯ã`gasLimit` ã `300000` Gasã«è¨­å®ãã¦ãã¾ãã
>
>
**ð¸: ã¬ã¹ä¾¡æ ¼ã¨ã¯**
> ééææ°æãæ±ºããããã1ã¤ã®ãã©ã¡ã¼ã¿ãã**ã¬ã¹ä¾¡æ ¼**ãã§ãã
>
> **ã¬ã¹ä¾¡æ ¼**ã¯ã**1Gas å½ããã®ä¾¡æ ¼**ãæå³ãã¾ãã
> åºæ¬çãª**1Gaså½ããã®ä¾¡æ ¼**ã¯ ã**21 `Gwei`**ã ã§ééããã¾ãã
>
> ã¬ã¹ä¾¡æ ¼ã®åä½ã¨ãã¦ä½¿ããã¦ããã **`wei`** ãã¯ãã¤ã¼ãµãªã¢ã ã®åä½ã§ 1ETH ã¨ã®ã¬ã¼ãã¯ä¸å³ã®ããã«ãªã£ã¦ãã¾ãã
> ![](https://i.imgur.com/IGdCKQV.png)
>
>**`G`** ã¯ã®ã¬ã®ãã¨ã§ã`1Gwei = 0.000000001ETH` ã§ãã
>
> ã¬ã¹ä¾¡æ ¼ã¯ãééèãèªç±ã«è¨­å®ãããã¨ãã§ãã¾ãã
>
> ãã¤ãã¼ã¯ãã¬ã¹ä¾¡æ ¼ãé«ãï¼ï¼ãã¤ãã³ã°å ±é¬ãå¤ãï¼ãã©ã³ã¶ã¯ã·ã§ã³ãåªåçã«æ¿èªããã®ã§ãã¬ã¹ä¾¡æ ¼ãé«ãè¨­å®ãã¦ããã¨ãééãæ©ããªãå¾åãããã¾ãã

**2 \. ãã­ã³ãã¨ã³ãã«ã¡ãã»ã¼ã¸ããã¯ã¹ãè¨­ç½®ãã**

ä¸è¨ããã­ã³ãã¨ã³ãã«å®è£ãã¾ããã
```javascript
// App.js
{currentAccount && (<textarea name="messageArea"
    placeholder="ã¡ãã»ã¼ã¸ã¯ãã¡ã"
    type="text"
    id="message"
    value={messageValue}
    onChange={e => setMessageValue(e.target.value)} />)
}
```
ããã¯ãèªè¨¼æ¸ã¿ã®ã¢ãã¬ã¹ï¼ï¼ `currentAccount` ï¼ãå­å¨ããå ´åã«ããã­ã¹ãããã¯ã¹ã UI ã«è¡¨ç¤ºããä»æ§ã«ãªã£ã¦ãã¾ããããã§ãã¦ã¼ã¶ã¼ã¯ UI ããç´æ¥ã¡ãã»ã¼ã¸ãæ¸ãè¾¼ããããã«ãªãã¾ãã

**3 \. éããã¦ããã¡ãã»ã¼ã¸ããã­ã³ãã¨ã³ãã«è¡¨ç¤ºãã**

```javascript
// App.js
{allWaves.slice(0).reverse().map((wave, index) => {
  return (
    <div key={index} style={{ backgroundColor: "#F8F8FF", marginTop: "16px", padding: "8px" }}>
      <div>Address: {wave.address}</div>
      <div>Time: {wave.timestamp.toString()}</div>
      <div>Message: {wave.message}</div>
    </div>)
})}
```

ã­ã¼ã«ã«ãµã¼ãã¼ã§WEBã¢ããªããã¹ããã¦ããã­ã³ãã¨ã³ããç¢ºèªããªãããä¸è¨ã®ã³ã¼ããã©ã®ããã«ãã­ã³ãã¨ã³ãã«åæ ããã¦ããã®ããèå¯ãã¦ã¿ã¦ãã ããã

**â­ï¸: ã­ã¼ã«ã«ãµã¼ãã¼ã®ç«ã¡ä¸ã**
  - ã¿ã¼ããã«ä¸ã§` your-first-dApp` ã«ç§»å
  - `npm run start` ãå®è¡
  - `localhost` ã§WEBã¢ããªãåç§

ãã¡ããããã­ã³ãã¨ã³ãã®å®è£çµæã®ä¾ã«ãªãã¾ãã

![](https://i.imgur.com/L61kUQY.pngs)


ðââï¸ è³ªåãã
-------------------------------------------
ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-3-help` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã®3ç¹ãè¨è¼ãã¦ãã ããâ¨
```
1. ä½ããããã¨ãã¦ããã
2. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
3. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```
--------------
WEBã¢ããªã®å¤§æ ãå®æããããæ¬¡ã®ã¬ãã¹ã³ã«é²ã¿ã¾ãããð
