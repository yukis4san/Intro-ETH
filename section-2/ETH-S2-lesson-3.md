ð `window.ethereum`ãè¨­å®ãã
--------------------------

WEBã¢ããªä¸ã§ãã¦ã¼ã¶ã¼ãã¤ã¼ãµãªã¢ã ãããã¯ã¼ã¯ã¨éä¿¡ããããã«ã¯ãWEBã¢ããªã¯ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããæå ±ãåå¾ããå¿è¦ãããã¾ãã

ãããããããªãã®WEBã¢ããªã«ã¦ã©ã¬ãããæ¥ç¶ããã¦ã¼ã¶ã¼ã«ãã¹ãã¼ãã³ã³ãã©ã¯ããå¼ã³åºãæ¨©éãä»ä¸ããæ©è½ãå®è£ãã¦ããã¾ãã

- ããã¯ãWEBãµã¤ãã¸ã®èªè¨¼æ©è½ã§ãã

ã¿ã¼ããã«ä¸ã§ã`your-first-dApp/src`ã«ç§»åãããã®ä¸­ã«ãã `App.js` ã VS Code ã§éãã¾ãããã

ä¸è¨ã®ããã«ã`App.js`ã®ä¸­èº«ãæ´æ°ãã¾ãã
- `App.js` ã¯ããªãã®WEBã¢ããªã®ãã­ã³ãã¨ã³ãæ©è½ãæããã¾ãã

```javascript
// App.js
import React, { useEffect } from "react";
import "./App.css";
const App = () => {
  const checkIfWalletIsConnected = () => {
    /*
    * window.ethereumã«ã¢ã¯ã»ã¹ã§ãããã¨ãç¢ºèªãã¾ãã
    */
    const { ethereum } = window;
    if (!ethereum) {
      console.log("Make sure you have metamask!");
    } else {
      console.log("We have the ethereum object", ethereum);
    }
  }
  /*
  * WEBãã¼ã¸ãã­ã¼ããããã¨ãã«ä¸è¨ã®é¢æ°ãå®è¡ãã¾ãã
  */
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
          ã¤ã¼ãµãªã¢ã ã¦ã©ã¬ãããæ¥ç¶ãã¦ãã<span role="img" aria-label="hand-wave">ð</span>(wave)ããéã£ã¦ãã ãã<span role="img" aria-label="shine">â¨</span>
        </div>
        <button className="waveButton" onClick={null}>
          Wave at Me
        </button>
      </div>
    </div>
  );
}
export default App
```
ð¦ ã¦ã¼ã¶ã¼ã¢ã«ã¦ã³ãã«ã¢ã¯ã»ã¹ã§ãããç¢ºèªãã
-----------------------------------------

`window.ethereum` ã¯ãããªãã®WEBãµã¤ããè¨ªåããã¦ã¼ã¶ã¼ã Metamask ãæã£ã¦ãããç¢ºèªããçµæã `Console log` ã«åºåãã¾ãã

ã¿ã¼ããã«ã§ `your-first-dApp` ã«ç§»åããä¸è¨ãå®è¡ãã¦ã¿ã¾ãããã

```bash
npm run start
```

ã­ã¼ã«ã«ãµã¼ãã¼ã§WEBãµã¤ããç«ã¡ä¸ãããããµã¤ãã®ä¸ã§å³ã¯ãªãã¯ãè¡ãã`Inspect`ãé¸æãã¾ãã
![](https://i.imgur.com/ce43rnr.png)
æ¬¡ã«ã`Console`ãé¸æããåºåçµæãç¢ºèªãã¦ã¿ã¾ãããã
![](https://i.imgur.com/M9836LA.png)
`Console` ã« `We have the ethereum object` ã¨è¡¨ç¤ºããã¦ããã§ããããï¼
- ããã¯ã`window.ethereum` ãããã®WEBãµã¤ããè¨ªåããã¦ã¼ã¶ã¼ï¼ããã§ããããªãï¼ã Metamask ãæã£ã¦ãããã¨ãç¢ºèªãããã¨ãç¤ºãã¦ãã¾ãã

æ¬¡ã«ãWEBãµã¤ããã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã«ã¢ã¯ã»ã¹ããæ¨©éããããç¢ºèªãã¾ãã

- ã¢ã¯ã»ã¹ã§ããããã¹ãã¼ãã³ã³ãã©ã¯ããå¼ã³åºããã¨ãã§ãã¾ãã

ãããããã¦ã¼ã¶ã¼èªèº«ãæ¿èªããWEBãµã¤ãã«ã¦ã©ã¬ããã®ã¢ã¯ã»ã¹æ¨©éãä¸ããã³ã¼ããæ¸ãã¦ããã¾ãã
- ããã¯ãã¦ã¼ã¶ã¼ã®ã­ã°ã¤ã³æ©è½ã§ãã

ä¸è¨ã®ããã«ã`App.js` ã®ä¸­èº«ãæ´æ°ãã¾ãã
```javascript
// App.js
import React, { useEffect, useState } from "react";
import "./App.css";
const App = () => {
  /* ã¦ã¼ã¶ã¼ã®ãããªãã¯ã¦ã©ã¬ãããä¿å­ããããã«ä½¿ç¨ããç¶æå¤æ°ãå®ç¾©ãã¾ã */
  const [currentAccount, setCurrentAccount] = useState("");
  console.log("currentAccount: ", currentAccount);
  /* window.ethereumã«ã¢ã¯ã»ã¹ã§ãããã¨ãç¢ºèªãã¾ã */
  const checkIfWalletIsConnected = async () => {
    try {
      const { ethereum } = window;
      if (!ethereum) {
        console.log("Make sure you have metamask!");
        return;
      } else {
        console.log("We have the ethereum object", ethereum);
      }
      /* ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¸ã®ã¢ã¯ã»ã¹ãè¨±å¯ããã¦ãããã©ãããç¢ºèªãã¾ã */
      const accounts = await ethereum.request({ method: "eth_accounts" });
      if (accounts.length !== 0) {
        const account = accounts[0];
        console.log("Found an authorized account:", account);
        setCurrentAccount(account)
      } else {
        console.log("No authorized account found")
      }
    } catch (error) {
      console.log(error);
    }
  }
  /* WEBãã¼ã¸ãã­ã¼ããããã¨ãã«ä¸è¨ã®é¢æ°ãå®è¡ãã¾ã */
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
          ã¤ã¼ãµãªã¢ã ã¦ã©ã¬ãããæ¥ç¶ãã¦ãã<span role="img" aria-label="hand-wave">ð</span>(wave)ããéã£ã¦ãã ãã<span role="img" aria-label="shine">â¨</span>
        </div>
        <button className="waveButton" onClick={null}>
          Wave at Me
        </button>
      </div>
    </div>
  );
  }
export default App
```

æ°ããè¿½å ããã³ã¼ããè¦ã¦ããã¾ãã

```javascript
// App.js
/* ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¸ã®ã¢ã¯ã»ã¹ãè¨±å¯ããã¦ãããã©ãããç¢ºèªãã¾ã */
const accounts = await ethereum.request({ method: "eth_accounts" });
if (accounts.length !== 0) {
	const account = accounts[0];
	console.log("Found an authorized account:", account);
	setCurrentAccount(account)
} else {
	console.log("No authorized account found")
}
```
`eth_accounts` ã¯ãç©ºã®éåã¾ãã¯åä¸ã®ã¢ã«ã¦ã³ãã¢ãã¬ã¹ãå«ãéåãè¿ãå½å¥ãªã¡ã½ããã§ãã

ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ã«ã¦ã³ãã¸ã®ã¢ã¯ã»ã¹ãè¨±å¯ããã¦ããå ´åã¯ã `Found an authorized account` ã¨ `Console` ã«åºåããã¾ãã

ã¿ã¼ããã«ã§ååº¦ `your-first-dApp` ã«ç§»åããä¸è¨ãå®è¡ãã¦ã¿ã¾ãããã

```bash
npm run start
```

ã­ã¼ã«ã«ãµã¼ãã¼ã§WEBãµã¤ããç«ã¡ä¸ãããããµã¤ãã®ä¸ã§å³ã¯ãªãã¯ãè¡ãã`Inspect` ãé¸æãã¾ãã
![](https://i.imgur.com/ce43rnr.png)
æ¬¡ã«ã`Console` ãé¸æããåºåçµæãç¢ºèªãã¦ã¿ã¾ãããã
![](https://i.imgur.com/U1F66KG.png)

âï¸: `Console` ã®çµæãè¦ã¦ããããã¨
> `App.js` ã«è¨è¼ããã¦ããã³ã¼ãã¯ä¸ããé ãè¿½ã£ã¦èµ°ã£ã¦ããã®ã§ãæåã« `currentAccount` ã®ç¶æå¤æ°ãå®ç¾©ããã¨ãã«ã¯ãä¸­èº«ãç©ºã§ãããã¨ããããã¾ãã
> ```javascript
> // App.js
> const [currentAccount, setCurrentAccount] = useState("");
> /*ãã®æ®µéã§currentAccountã®ä¸­èº«ã¯ç©º*/
> console.log("currentAccount: ", currentAccount);
> ```
> ã¢ã¯ã»ã¹å¯è½ãªã¢ã«ã¦ã³ããæ¤åºããå¾ã`currentAccount` ã«ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ã«ã¦ã³ãï¼`0x...`ï¼ã®å¤ãå¥ãã¾ãã
>

ä»¥ä¸ã§ `currentAccount` ãæ´æ°ãã¦ãã¾ãã
> ```javascript
> // App.js
> // accountsã«WEBãµã¤ããè¨ªããã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ã«ã¦ã³ããæ ¼ç´ããï¼è¤æ°æã£ã¦ããå ´åãå å³ããã£ã¦ account's' ã¨å¤æ°ãå®ç¾©ãã¦ããï¼
> const accounts = await ethereum.request({ method: "eth_accounts" });
> // ããã¢ã«ã¦ã³ããä¸ã¤ã§ãå­å¨ããããä»¥ä¸ãå®è¡ã
> if (accounts.length !== 0) {
> 	// accountã¨ããå¤æ°ã«ã¦ã¼ã¶ã¼ã®1ã¤ç®ï¼=Javascriptã§ãã0çªç®ï¼ã®ã¢ãã¬ã¹ãæ ¼ç´
> 	const account = accounts[0];
>	console.log("Found an authorized account:", account);
> 	// currentAccountã«ã¦ã¼ã¶ã¼ã®ã¢ã«ã¦ã³ãã¢ãã¬ã¹ãæ ¼ç´
>	setCurrentAccount(account)
>} else {
>	console.log("No authorized account found")
>}
> ```
> ãã®å¦çã®ãããã§ãã¦ã¼ã¶ã¼ãã¦ã©ã¬ããã«è¤æ°ã®ã¢ã«ã¦ã³ããæã£ã¦ããå ´åã§ãããã­ã°ã©ã ã¯ã¦ã¼ã¶ã¼ã®1çªç®ã®ã¢ã«ã¦ã³ãã¢ãã¬ã¹ãåå¾ãããã¨ãã§ãã¾ãã

ð ã¦ã©ã¬ããæ¥ç¶ãã¿ã³ãä½æãã
--------------------------------

`connectWallet` ãã¿ã³ãä½æãã¦ããã¾ãã

```javascript
// App.js
import React, { useEffect, useState } from "react";
import "./App.css";
const App = () => {
  // ã¦ã¼ã¶ã¼ã®ãããªãã¯ã¦ã©ã¬ãããä¿å­ããããã«ä½¿ç¨ããç¶æå¤æ°ãå®ç¾©ãã¾ãã
  const [currentAccount, setCurrentAccount] = useState("");
  console.log("currentAccount: ", currentAccount);
  // window.ethereumã«ã¢ã¯ã»ã¹ã§ãããã¨ãç¢ºèªãã¾ãã
  const checkIfWalletIsConnected = async () => {
    try {
      const { ethereum } = window;
      if (!ethereum) {
        console.log("Make sure you have metamask!");
        return;
      } else {
        console.log("We have the ethereum object", ethereum);
      }
      // ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¸ã®ã¢ã¯ã»ã¹ãè¨±å¯ããã¦ãããã©ãããç¢ºèªãã¾ãã
      const accounts = await ethereum.request({ method: "eth_accounts" });
      if (accounts.length !== 0) {
        const account = accounts[0];
        console.log("Found an authorized account:", account);
        setCurrentAccount(account)
      } else {
        console.log("No authorized account found")
      }
    } catch (error) {
      console.log(error);
    }
  }
  // connectWalletã¡ã½ãããå®è£
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
  // WEBãã¼ã¸ãã­ã¼ããããã¨ãã«ä¸è¨ã®é¢æ°ãå®è¡ãã¾ãã
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
          ã¤ã¼ãµãªã¢ã ã¦ã©ã¬ãããæ¥ç¶ãã¦ãã<span role="img" aria-label="hand-wave">ð</span>(wave)ããéã£ã¦ãã ãã<span role="img" aria-label="shine">â¨</span>
        </div>
        <button className="waveButton" onClick={null}>
          Wave at Me
        </button>
        {/* ã¦ã©ã¬ããã³ãã¯ãã®ãã¿ã³ãå®è£ */}
        {!currentAccount && (
        <button className="waveButton" onClick={connectWallet}>
            Connect Wallet
        </button>
        )}
        {currentAccount && (
        <button className="waveButton" onClick={connectWallet}>
            Wallet Connected
        </button>
        )}
      </div>
    </div>
  );
  }
export default App
```
ããã§å®è£ããæ©è½ã¯ä»¥ä¸ã®äºã¤ã§ãã

**1 \. `connectWallet` ã¡ã½ãããå®è£**
```javascript
// App.js
const connectWallet = async () => {
	try {
		// ã¦ã¼ã¶ã¼ãèªè¨¼å¯è½ãªã¦ã©ã¬ããã¢ãã¬ã¹ãæã£ã¦ãããç¢ºèª
		const { ethereum } = window;
		if (!ethereum) {
			alert("Get MetaMask!");
			return;
		}
		// æã£ã¦ããå ´åã¯ãã¦ã¼ã¶ã¼ã«å¯¾ãã¦ã¦ã©ã¬ããã¸ã®ã¢ã¯ã»ã¹è¨±å¯ãæ±ãããè¨±å¯ãããã°ãã¦ã¼ã¶ã¼ã®æåã®ã¦ã©ã¬ããã¢ãã¬ã¹ã currentAccount ã«æ ¼ç´ããã
		const accounts = await ethereum.request({ method: "eth_requestAccounts" });
		console.log("Connected: ", accounts[0]);
		setCurrentAccount(accounts[0]);
    } catch (error) {
		console.log(error)
    }
  }
```
`eth_requestAccounts` é¢æ°ãä½¿ç¨ãããã¨ã§ãMetamask ããã¦ã¼ã¶ã¼ã«ã¦ã©ã¬ããã¸ã®ã¢ã¯ã»ã¹ãè¨±å¯ããããå¼ã³ããããã¨ãã§ãã¾ãã

**2 \. ã¦ã©ã¬ããã³ãã¯ãã®ãã¿ã³ãå®è£**
```javascript
// App.js
// currentAccountãå­å¨ããªãå ´åã¯ããConnect Walletããã¿ã³ãå®è£
{!currentAccount && (
<button className="waveButton" onClick={connectWallet}>
	Connect Wallet
</button>
)}
/// currentAccountãå­å¨ããå ´åã¯ããWallet Connectedããã¿ã³ãå®è£
{currentAccount && (
<button className="waveButton" onClick={connectWallet}>
	Wallet Connected
</button>
)}
```
ð ã¦ã©ã¬ããã³ãã¯ãã®ãã¹ããå®è¡ãã
--------------------------------

ä¸è¨ã®ã³ã¼ããå¨ã¦ `App.js` ã«åæ ãããããã¿ã¼ããã«ã§ `your-first-dApp` ã«ç§»åããä¸è¨ãå®è¡ãã¾ãããã

```bash
npm run start
```

ã­ã¼ã«ã«ãµã¼ãã¼ã§WEBãµã¤ããç«ã¡ä¸ããããMetamask ã®ãã©ã°ã¤ã³ãã¯ãªãã¯ããããªãã®ã¦ã©ã¬ããã¢ãã¬ã¹ã®æ¥ç¶ç¶æ³ãç¢ºèªãã¾ãããã
ãããä¸å³ã®ããã« `Connected` ã¨è¡¨ç¤ºããã¦ããå ´åã¯ã`Connected` ã®æå­ãã¯ãªãã¯ãã¾ãã
![](https://i.imgur.com/hzXLzQZ.png)

ããã§ãWEBãµã¤ãã¨ããªãã®ã¦ã©ã¬ããã¢ãã¬ã¹ã®æ¥ç¶ãä¸åº¦è§£é¤ãã¾ãã
- `Disconnect this account` ãé¸æãã¦ãã ããã
![](https://i.imgur.com/UoOhJDd.png)

æ¬¡ã«ã­ã¼ã«ã«ãµã¼ãã¼ã«ãã¹ãããã¦ããããªãã®WEBãµã¤ãããªãã¬ãã·ã¥ãã¦ãã¿ã³ã®è¡¨ç¤ºãç¢ºèªãã¦ãã ããã
- ã¦ã©ã¬ããæ¥ç¶ç¨ã®ãã¿ã³ãã`Connect Wallet` ã¨è¡¨ç¤ºããã¦ããã°æåã§ãã
![](https://i.imgur.com/KEI6jwd.png)

æ¬¡ã«ãå³ã¯ãªãã¯ â `Inspect` ãé¸æãã`Console` ãç«ã¡ä¸ãã¾ããããä¸å³ã®ããã«ã`No authorized account found` ã¨åºåããã¦ããã°æåã§ãã
![](https://i.imgur.com/q6uEOFF.png)

ã§ã¯ã`Connect Wallet` ãã¿ã³ãæ¼ãã¦ã¿ã¾ãããã
ä¸å³ã®ããã« Metamask ããã¦ã©ã¬ããæ¥ç¶ãæ±ãããã¾ãã®ã§ãæ¿èªãã¦ãã ããã
![](https://i.imgur.com/IwyFnQj.png)

Metamask ã®æ¿èªãçµããã¨ãã¦ã©ã¬ããæ¥ç¶ãã¿ã³ã®è¡¨ç¤ºã `Wallet Connected` ã«å¤æ´ããã¦ããã¯ãã§ãã `Console` ã«ããæ¥ç¶ãããã¦ã©ã¬ããã¢ãã¬ã¹ãã`currentAccount` ã¨ãã¦åºåããã¦ãããã¨ãç¢ºèªãã¦ãã ããã
![](https://i.imgur.com/zQsSsmT.png)

ðââï¸ è³ªåãã
-------------------------------------------
ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscordã®`#section-2-help`ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã®3ç¹ãè¨è¼ãã¦ãã ããâ¨
```
1. ä½ããããã¨ãã¦ããã
2. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
3. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```
-------------------------------------------
ã¦ã©ã¬ããæ¥ç¶æ©è½ãå®æããããæ¬¡ã®ã¬ãã¹ã³ã«é²ã¿ã¾ãããð

<!--
ðæ¥ç¶!ãã®åç»ã§ã¢ããªã®åä½ãå®æ¼ãã¦ã¾ããæ°ããåç»ãä½ããã¯è¦æ¤è¨
-----------
ãããé­æ³ã®æéã§ã!ä»¥ä¸ã®ãããªããã§ãã¯ãã¦ãã ããï¼
[ç¹æ©](https ï¼// www.loom.com/share/1d30b147047141ce8fde590c7673128d?t=0)
-->
