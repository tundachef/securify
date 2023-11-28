![securify](/img/securify-v2-0.png)

Securify v2.0
===

Securify 2.0 is a security scanner for Ethereum smart contracts supported by the
[Ethereum
Foundation](https://ethereum.github.io/blog/2018/08/17/ethereum-foundation-grants-update-wave-3/)
and [ChainSecurity](https://chainsecurity.com). The core
[research](https://files.sri.inf.ethz.ch/website/papers/ccs18-securify.pdf)
behind Securify was conducted at the [Secure, Reliable, and Intelligent Systems Lab](https://www.sri.inf.ethz.ch/) at ETH
Zurich.

It is the successor of the popular Securify security scanner (you can find the old version [here](https://github.com/eth-sri/securify)).

https://github.com/eth-sri/securify2


Features
===
- Supports 37 vulnerabilities (see [table](#supported-vulnerabilities) below)
- Implements novel context-sensitive static analysis written in Datalog
- Analyzes contracts written in Solidity >= 0.5.8


Docker
===
To build the container:
```angular2
sudo docker build -t securify .
```
To run the container:
````angular2
sudo docker run -it -v <contract-dir-full-path>:/share securify /share/<contract>.sol
````
## What actually Works(Any Environment):
These tests were performed on a windows environment.
```
docker run -it -v C:/Users/sentl/Documents/securify2-master/gold:/app securify /app/gold.sol
```
In this command:

`-v C:/Users/sentl/Documents/securify2-master/gold:/app` maps the `C:\Users\sentl\Documents\securify2-master\gold` directory on your local machine to the `/app` directory inside the Docker container.

securify is the Docker image you're running.

`/app/gold.sol` is the path to the `gold.sol` file inside the Docker container.

Another solidity version causes the program to crash thus, the code was sent to Chatgpt on file at a time and made compatible with solidity compiler version 0.5.12 thus getting rid of this problem altogether. 

But Note: gold.sol consists of all the contracts put in one file with the one that depends on all of them last, that is:
IERC20.sol, Context.sol, Ownable.sol, GoldGrinder.sol, were all put together in one file (gold.sol). Then the code was tested with remix IDE with compiler 0.5.12. Lastly fed to securify. 

Only build once with 0.5.12 and follow these steps.

[To compare the live contract with Chatgpt code this tool was used](https://www.w3docs.com/tools/code-diff/)

### Example Response:

```
Severity:    INFO
Pattern:     Constable State Variables
Description: State variables that do not change should be declared as
             constants.
Type:        Violation
Contract:    GoldGrinderV2
Line:        89
Source:
>
>     uint256 public COMPOUND_BONUS = 30;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public COMPOUND_BONUS_MAX_TIMES = 20;


Severity:    INFO
Pattern:     Constable State Variables
Description: State variables that do not change should be declared as
             constants.
Type:        Violation
Contract:    GoldGrinderV2
Line:        90
Source:
>     uint256 public COMPOUND_BONUS = 30;
>     uint256 public COMPOUND_BONUS_MAX_TIMES = 20;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public COMPOUND_STEP = 1 days;


Severity:    INFO
Pattern:     Constable State Variables
Description: State variables that do not change should be declared as
             constants.
Type:        Violation
Contract:    GoldGrinderV2
Line:        91
Source:
>     uint256 public COMPOUND_BONUS_MAX_TIMES = 20;
>     uint256 public COMPOUND_STEP = 1 days;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    INFO
Pattern:     Constable State Variables
Description: State variables that do not change should be declared as
             constants.
Type:        Violation
Contract:    GoldGrinderV2
Line:        93
Source:
>
>     uint256 public WITHDRAWAL_TAX = 800;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public COMPOUND_FOR_NO_TAX_WITHDRAWAL = 10;


Severity:    INFO
Pattern:     Constable State Variables
Description: State variables that do not change should be declared as
             constants.
Type:        Violation
Contract:    GoldGrinderV2
Line:        94
Source:
>     uint256 public WITHDRAWAL_TAX = 800;
>     uint256 public COMPOUND_FOR_NO_TAX_WITHDRAWAL = 10;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    INFO
Pattern:     Constable State Variables
Description: State variables that do not change should be declared as
             constants.
Type:        Violation
Contract:    GoldGrinderV2
Line:        103
Source:
>     uint256 private marketGolds = 100_000 * GOLDS_TO_HIRE_1MINER;
>     uint256 PSN = 10000;
>     ^^^^^^^^^^^^^^^^^^^
>     uint256 PSNH = 5000;


Severity:    INFO
Pattern:     Constable State Variables
Description: State variables that do not change should be declared as
             constants.
Type:        Violation
Contract:    GoldGrinderV2
Line:        104
Source:
>     uint256 PSN = 10000;
>     uint256 PSNH = 5000;
>     ^^^^^^^^^^^^^^^^^^^
>


Severity:    INFO
Pattern:     Constable State Variables
Description: State variables that do not change should be declared as
             constants.
Type:        Violation
Contract:    GoldGrinderV2
Line:        108
Source:
>
>     uint256 public CUTOFF_STEP = 2 days;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public WITHDRAW_COOLDOWN = 1 days;


Severity:    INFO
Pattern:     Constable State Variables
Description: State variables that do not change should be declared as
             constants.
Type:        Violation
Contract:    GoldGrinderV2
Line:        109
Source:
>     uint256 public CUTOFF_STEP = 2 days;
>     uint256 public WITHDRAW_COOLDOWN = 1 days;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    Ownable
Line:        35
Source:
>
>     function renounceOwnership() public onlyOwner {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         _transferOwnership(address(0));


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    Ownable
Line:        39
Source:
>
>     function transferOwnership(address newOwner) public onlyOwner {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         require(


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    Ownable
Line:        35
Source:
>
>     function renounceOwnership() public onlyOwner {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         _transferOwnership(address(0));


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    Ownable
Line:        39
Source:
>
>     function transferOwnership(address newOwner) public onlyOwner {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         require(


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    GoldGrinderV2
Line:        145
Source:
>
>     function startFarm(address addr, uint256 amount) public payable onlyOwner {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         require(!_initialized, "Already initialized");


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    GoldGrinderV2
Line:        189
Source:
>
>     function sellGolds() public initialized {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         User storage user = users[msg.sender];


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    GoldGrinderV2
Line:        272
Source:
>
>     function getUserInfo(
>     ^^^^^^^^^^^^^^^^^^^^^
>         address _adr


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    GoldGrinderV2
Line:        306
Source:
>
>     function getAvailableEarnings(address _adr) public view returns (uint256) {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         return calculateGoldSell(getMyGolds(_adr));


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    GoldGrinderV2
Line:        330
Source:
>
>     function calculateGoldBuySimple(uint256 eth) public view returns (uint256) {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         return calculateGoldBuy(eth, token.balanceOf(address(this)));


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    GoldGrinderV2
Line:        334
Source:
>
>     function getGoldsYieldPerDay(
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         uint256 amount


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    GoldGrinderV2
Line:        360
Source:
>
>     function getSiteInfo()
>     ^^^^^^^^^^^^^^^^^^^^^^
>         public


Severity:    LOW
Pattern:     External Calls of Functions
Description: A public function that is never called within the
             contract should be marked as external
Type:        Violation
Contract:    GoldGrinderV2
Line:        373
Source:
>
>     function getMyMiners() public view returns (uint256) {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         return users[msg.sender].miners;


Severity:    MEDIUM
Pattern:     Locked Ether
Description: Contracts that may receive ether must also allow users to
             extract the deposited ether from the contract.
Type:        Violation
Contract:    GoldGrinderV2
Line:        82
Source:
>
> contract GoldGrinderV2 is Ownable {
> ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public constant GOLDS_TO_HIRE_1MINER = 10 days; // 10% daily apr


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Warning
Contract:    GoldGrinderV2
Line:        145
Source:
>
>     function startFarm(address addr, uint256 amount) public payable onlyOwner {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         require(!_initialized, "Already initialized");


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Warning
Contract:    GoldGrinderV2
Line:        225
Source:
>
>     function buyGold(address ref, uint256 amount) public payable initialized {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         User storage user = users[msg.sender];


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Warning
Contract:    GoldGrinderV2
Line:        306
Source:
>
>     function getAvailableEarnings(address _adr) public view returns (uint256) {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         return calculateGoldSell(getMyGolds(_adr));


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Warning
Contract:    GoldGrinderV2
Line:        377
Source:
>
>     function getMyGolds(address adr) public view returns (uint256) {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         return users[adr].claimedGolds + getGoldsSinceLastHireTime(adr);


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Warning
Contract:    GoldGrinderV2
Line:        381
Source:
>
>     function getGoldsSinceLastHireTime(
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         address adr


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Violation
Contract:    GoldGrinderV2
Line:        263
Source:
>
>     function getDailyCompoundBonus(
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         address _adr,


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Violation
Contract:    GoldGrinderV2
Line:        272
Source:
>
>     function getUserInfo(
>     ^^^^^^^^^^^^^^^^^^^^^
>         address _adr


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Violation
Contract:    GoldGrinderV2
Line:        318
Source:
>
>     function calculateGoldSell(uint256 golds) public view returns (uint256) {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         return


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Violation
Contract:    GoldGrinderV2
Line:        323
Source:
>
>     function calculateGoldBuy(
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^
>         uint256 eth,


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Violation
Contract:    GoldGrinderV2
Line:        330
Source:
>
>     function calculateGoldBuySimple(uint256 eth) public view returns (uint256) {
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         return calculateGoldBuy(eth, token.balanceOf(address(this)));


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Violation
Contract:    GoldGrinderV2
Line:        334
Source:
>
>     function getGoldsYieldPerDay(
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         uint256 amount


Severity:    MEDIUM
Pattern:     Missing Input Validation
Description: Method arguments must be sanitized before they are used
             in computations.
Type:        Violation
Contract:    GoldGrinderV2
Line:        348
Source:
>
>     function calculateGoldSellForYield(
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         uint256 golds,


Severity:    MEDIUM
Pattern:     Multiplication after division
Description: Information might be lost due to division before
             multiplication
Type:        Violation
Contract:    GoldGrinderV2
Line:        245
Source:
>             address upline = user.referrer;
>             uint256 refRewards = (amount * REFERRAL) / PERCENTS_DIVIDER;
>                                   ^^^^^^^^^^^^^^^^^
>             token.transfer(upline, refRewards);


Severity:    MEDIUM
Pattern:     Multiplication after division
Description: Information might be lost due to division before
             multiplication
Type:        Violation
Contract:    GoldGrinderV2
Line:        315
Source:
>     ) private view returns (uint256) {
>         return (PSN * bs) / (PSNH + (PSN * rs + PSNH * rt) / rt);
>                 ^^^^^^^^
>     }


Severity:    MEDIUM
Pattern:     Multiplication after division
Description: Information might be lost due to division before
             multiplication
Type:        Violation
Contract:    GoldGrinderV2
Line:        315
Source:
>     ) private view returns (uint256) {
>         return (PSN * bs) / (PSNH + (PSN * rs + PSNH * rt) / rt);
>                                      ^^^^^^^^
>     }


Severity:    MEDIUM
Pattern:     Multiplication after division
Description: Information might be lost due to division before
             multiplication
Type:        Violation
Contract:    GoldGrinderV2
Line:        315
Source:
>     ) private view returns (uint256) {
>         return (PSN * bs) / (PSNH + (PSN * rs + PSNH * rt) / rt);
>                                                 ^^^^^^^^^
>     }


Severity:    MEDIUM
Pattern:     Multiplication after division
Description: Information might be lost due to division before
             multiplication
Type:        Violation
Contract:    GoldGrinderV2
Line:        268
Source:
>         uint256 totalBonus = users[_adr].dailyCompoundBonus * COMPOUND_BONUS;
>         uint256 result = (amount * totalBonus) / PERCENTS_DIVIDER;
>                           ^^^^^^^^^^^^^^^^^^^
>         return result;


Severity:    MEDIUM
Pattern:     Multiplication after division
Description: Information might be lost due to division before
             multiplication
Type:        Violation
Contract:    GoldGrinderV2
Line:        258
Source:
>     function payFees(uint256 goldValue) private returns (uint256) {
>         uint256 tax = (goldValue * devTax) / PERCENTS_DIVIDER;
>                        ^^^^^^^^^^^^^^^^^^
>         token.transfer(dev1, tax);


Severity:    MEDIUM
Pattern:     Multiplication after division
Description: Information might be lost due to division before
             multiplication
Type:        Violation
Contract:    GoldGrinderV2
Line:        200
Source:
>         if (user.dailyCompoundBonus < COMPOUND_FOR_NO_TAX_WITHDRAWAL) {
>             goldValue -= ((goldValue * WITHDRAWAL_TAX) / PERCENTS_DIVIDER);
>                            ^^^^^^^^^^^^^^^^^^^^^^^^^^
>         } else {


Severity:    MEDIUM
Pattern:     Multiplication after division
Description: Information might be lost due to division before
             multiplication
Type:        Violation
Contract:    GoldGrinderV2
Line:        343
Source:
>         uint256 day = 1 days;
>         uint256 goldsPerDay = day * miners;
>                               ^^^^^^^^^^^^
>         uint256 earningsPerDay = calculateGoldSellForYield(goldsPerDay, amount);


Severity:    MEDIUM
Pattern:     No-Ether-Involved Reentrancy
Description: Reentrancy that involves no ether
Type:        Warning
Contract:    GoldGrinderV2
Line:        211
Source:
>
>         if (token.balanceOf(address(this)) < goldValue) {
>             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>             goldValue = token.balanceOf(address(this));


Severity:    MEDIUM
Pattern:     No-Ether-Involved Reentrancy
Description: Reentrancy that involves no ether
Type:        Warning
Contract:    GoldGrinderV2
Line:        212
Source:
>         if (token.balanceOf(address(this)) < goldValue) {
>             goldValue = token.balanceOf(address(this));
>                         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         }


Severity:    MEDIUM
Pattern:     No-Ether-Involved Reentrancy
Description: Reentrancy that involves no ether
Type:        Warning
Contract:    GoldGrinderV2
Line:        216
Source:
>         uint256 goldsPayout = goldValue - payFees(goldValue);
>         token.transfer(msg.sender, goldsPayout);
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         user.totalWithdrawn = user.totalWithdrawn + goldsPayout;


Severity:    INFO
Pattern:     Solidity Naming Convention
Description: Reports declarations that do not adhere to Solidity's
             naming convention.
Type:        Violation
Contract:    GoldGrinderV2
Line:        89
Source:
>
>     uint256 public COMPOUND_BONUS = 30;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public COMPOUND_BONUS_MAX_TIMES = 20;


Severity:    INFO
Pattern:     Solidity Naming Convention
Description: Reports declarations that do not adhere to Solidity's
             naming convention.
Type:        Violation
Contract:    GoldGrinderV2
Line:        90
Source:
>     uint256 public COMPOUND_BONUS = 30;
>     uint256 public COMPOUND_BONUS_MAX_TIMES = 20;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public COMPOUND_STEP = 1 days;


Severity:    INFO
Pattern:     Solidity Naming Convention
Description: Reports declarations that do not adhere to Solidity's
             naming convention.
Type:        Violation
Contract:    GoldGrinderV2
Line:        91
Source:
>     uint256 public COMPOUND_BONUS_MAX_TIMES = 20;
>     uint256 public COMPOUND_STEP = 1 days;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    INFO
Pattern:     Solidity Naming Convention
Description: Reports declarations that do not adhere to Solidity's
             naming convention.
Type:        Violation
Contract:    GoldGrinderV2
Line:        93
Source:
>
>     uint256 public WITHDRAWAL_TAX = 800;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public COMPOUND_FOR_NO_TAX_WITHDRAWAL = 10;


Severity:    INFO
Pattern:     Solidity Naming Convention
Description: Reports declarations that do not adhere to Solidity's
             naming convention.
Type:        Violation
Contract:    GoldGrinderV2
Line:        94
Source:
>     uint256 public WITHDRAWAL_TAX = 800;
>     uint256 public COMPOUND_FOR_NO_TAX_WITHDRAWAL = 10;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    INFO
Pattern:     Solidity Naming Convention
Description: Reports declarations that do not adhere to Solidity's
             naming convention.
Type:        Violation
Contract:    GoldGrinderV2
Line:        103
Source:
>     uint256 private marketGolds = 100_000 * GOLDS_TO_HIRE_1MINER;
>     uint256 PSN = 10000;
>     ^^^^^^^^^^^^^^^^^^^
>     uint256 PSNH = 5000;


Severity:    INFO
Pattern:     Solidity Naming Convention
Description: Reports declarations that do not adhere to Solidity's
             naming convention.
Type:        Violation
Contract:    GoldGrinderV2
Line:        104
Source:
>     uint256 PSN = 10000;
>     uint256 PSNH = 5000;
>     ^^^^^^^^^^^^^^^^^^^
>


Severity:    INFO
Pattern:     Solidity Naming Convention
Description: Reports declarations that do not adhere to Solidity's
             naming convention.
Type:        Violation
Contract:    GoldGrinderV2
Line:        108
Source:
>
>     uint256 public CUTOFF_STEP = 2 days;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public WITHDRAW_COOLDOWN = 1 days;


Severity:    INFO
Pattern:     Solidity Naming Convention
Description: Reports declarations that do not adhere to Solidity's
             naming convention.
Type:        Violation
Contract:    GoldGrinderV2
Line:        109
Source:
>     uint256 public CUTOFF_STEP = 2 days;
>     uint256 public WITHDRAW_COOLDOWN = 1 days;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    INFO
Pattern:     State variables default visibility
Description: Visibility of state variables should be stated explicitly
Type:        Violation
Contract:    GoldGrinderV2
Line:        103
Source:
>     uint256 private marketGolds = 100_000 * GOLDS_TO_HIRE_1MINER;
>     uint256 PSN = 10000;
>     ^^^^^^^^^^^^^^^^^^^
>     uint256 PSNH = 5000;


Severity:    INFO
Pattern:     State variables default visibility
Description: Visibility of state variables should be stated explicitly
Type:        Violation
Contract:    GoldGrinderV2
Line:        104
Source:
>     uint256 PSN = 10000;
>     uint256 PSNH = 5000;
>     ^^^^^^^^^^^^^^^^^^^
>


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Warning
Contract:    GoldGrinderV2
Line:        211
Source:
>
>         if (token.balanceOf(address(this)) < goldValue) {
>             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>             goldValue = token.balanceOf(address(this));


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Warning
Contract:    GoldGrinderV2
Line:        212
Source:
>         if (token.balanceOf(address(this)) < goldValue) {
>             goldValue = token.balanceOf(address(this));
>                         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         }


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Violation
Contract:    GoldGrinderV2
Line:        227
Source:
>         User storage user = users[msg.sender];
>         token.transferFrom(msg.sender, address(this), amount);
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         uint256 goldsBought = calculateGoldBuy(


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Violation
Contract:    GoldGrinderV2
Line:        230
Source:
>             amount,
>             token.balanceOf(address(this)) - amount
>             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         );


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Violation
Contract:    GoldGrinderV2
Line:        246
Source:
>             uint256 refRewards = (amount * REFERRAL) / PERCENTS_DIVIDER;
>             token.transfer(upline, refRewards);
>             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Violation
Contract:    GoldGrinderV2
Line:        320
Source:
>         return
>             calculateTrade(golds, marketGolds, token.balanceOf(address(this)));
>                                                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     }


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Violation
Contract:    GoldGrinderV2
Line:        259
Source:
>         uint256 tax = (goldValue * devTax) / PERCENTS_DIVIDER;
>         token.transfer(dev1, tax);
>         ^^^^^^^^^^^^^^^^^^^^^^^^^
>         return tax;


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Violation
Contract:    GoldGrinderV2
Line:        216
Source:
>         uint256 goldsPayout = goldValue - payFees(goldValue);
>         token.transfer(msg.sender, goldsPayout);
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         user.totalWithdrawn = user.totalWithdrawn + goldsPayout;


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Violation
Contract:    GoldGrinderV2
Line:        331
Source:
>     function calculateGoldBuySimple(uint256 eth) public view returns (uint256) {
>         return calculateGoldBuy(eth, token.balanceOf(address(this)));
>                                      ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     }


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Violation
Contract:    GoldGrinderV2
Line:        339
Source:
>             amount,
>             token.balanceOf(address(this))
>             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         );


Severity:    HIGH
Pattern:     Unhandled Exception
Description: The return value of statements that may return error
             values must be explicitly checked.
Type:        Violation
Contract:    GoldGrinderV2
Line:        356
Source:
>                 marketGolds,
>                 token.balanceOf(address(this)) + amount
>                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>             );


Severity:    HIGH
Pattern:     Uninitialized State Variable
Description: State variables should be explicitly initialized.
Type:        Warning
Contract:    GoldGrinderV2
Line:        96
Source:
>
>     uint256 public totalStaked;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public totalUsers;


Severity:    HIGH
Pattern:     Uninitialized State Variable
Description: State variables should be explicitly initialized.
Type:        Warning
Contract:    GoldGrinderV2
Line:        97
Source:
>     uint256 public totalStaked;
>     uint256 public totalUsers;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public totalCompound;


Severity:    HIGH
Pattern:     Uninitialized State Variable
Description: State variables should be explicitly initialized.
Type:        Warning
Contract:    GoldGrinderV2
Line:        98
Source:
>     uint256 public totalUsers;
>     uint256 public totalCompound;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public totalRefBonus;


Severity:    HIGH
Pattern:     Uninitialized State Variable
Description: State variables should be explicitly initialized.
Type:        Warning
Contract:    GoldGrinderV2
Line:        99
Source:
>     uint256 public totalCompound;
>     uint256 public totalRefBonus;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>     uint256 public totalWithdrawn;


Severity:    HIGH
Pattern:     Uninitialized State Variable
Description: State variables should be explicitly initialized.
Type:        Warning
Contract:    GoldGrinderV2
Line:        100
Source:
>     uint256 public totalRefBonus;
>     uint256 public totalWithdrawn;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    HIGH
Pattern:     Uninitialized State Variable
Description: State variables should be explicitly initialized.
Type:        Warning
Contract:    GoldGrinderV2
Line:        106
Source:
>
>     bool private _initialized;
>     ^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    Ownable
Line:        49
Source:
>         address oldOwner = _owner;
>         _owner = newOwner;
>         ^^^^^^^^^^^^^^^^^
>         emit OwnershipTransferred(oldOwner, newOwner);


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    GoldGrinderV2
Line:        232
Source:
>         );
>         user.userDeposit += amount;
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^
>         user.initialDeposit += amount;


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    GoldGrinderV2
Line:        233
Source:
>         user.userDeposit += amount;
>         user.initialDeposit += amount;
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         user.claimedGolds += goldsBought;


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    GoldGrinderV2
Line:        234
Source:
>         user.initialDeposit += amount;
>         user.claimedGolds += goldsBought;
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    GoldGrinderV2
Line:        253
Source:
>         uint256 goldsPayout = payFees(amount);
>         totalStaked += amount - goldsPayout;
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         hireMiners(false);


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    GoldGrinderV2
Line:        163
Source:
>             uint256 goldsUsedValue = calculateGoldSell(goldsForCompound);
>             user.userDeposit += goldsUsedValue;
>             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>             totalCompound += goldsUsedValue;


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    GoldGrinderV2
Line:        164
Source:
>             user.userDeposit += goldsUsedValue;
>             totalCompound += goldsUsedValue;
>             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         }


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    GoldGrinderV2
Line:        173
Source:
>         }
>         user.claimedGolds = goldsForCompound % GOLDS_TO_HIRE_1MINER;
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         user.miners += goldsForCompound / GOLDS_TO_HIRE_1MINER;


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    GoldGrinderV2
Line:        174
Source:
>         user.claimedGolds = goldsForCompound % GOLDS_TO_HIRE_1MINER;
>         user.miners += goldsForCompound / GOLDS_TO_HIRE_1MINER;
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         user.lastHireTime = block.timestamp;


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    GoldGrinderV2
Line:        175
Source:
>         user.miners += goldsForCompound / GOLDS_TO_HIRE_1MINER;
>         user.lastHireTime = block.timestamp;
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    CRITICAL
Pattern:     Unrestricted write to storage
Description: Contract fields that can be modified by any user must be
             inspected.
Type:        Warning
Contract:    GoldGrinderV2
Line:        177
Source:
>
>         marketGolds += dampenGold(goldsUsed);
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    MEDIUM
Pattern:     Unused Return Pattern
Description: The value returned by an external function call is never
             used
Type:        Violation
Contract:    GoldGrinderV2
Line:        227
Source:
>         User storage user = users[msg.sender];
>         token.transferFrom(msg.sender, address(this), amount);
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         uint256 goldsBought = calculateGoldBuy(


Severity:    MEDIUM
Pattern:     Unused Return Pattern
Description: The value returned by an external function call is never
             used
Type:        Violation
Contract:    GoldGrinderV2
Line:        246
Source:
>             uint256 refRewards = (amount * REFERRAL) / PERCENTS_DIVIDER;
>             token.transfer(upline, refRewards);
>             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>


Severity:    MEDIUM
Pattern:     Unused Return Pattern
Description: The value returned by an external function call is never
             used
Type:        Violation
Contract:    GoldGrinderV2
Line:        259
Source:
>         uint256 tax = (goldValue * devTax) / PERCENTS_DIVIDER;
>         token.transfer(dev1, tax);
>         ^^^^^^^^^^^^^^^^^^^^^^^^^
>         return tax;


Severity:    MEDIUM
Pattern:     Unused Return Pattern
Description: The value returned by an external function call is never
             used
Type:        Violation
Contract:    GoldGrinderV2
Line:        216
Source:
>         uint256 goldsPayout = goldValue - payFees(goldValue);
>         token.transfer(msg.sender, goldsPayout);
>         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
>         user.totalWithdrawn = user.totalWithdrawn + goldsPayout;


Severity:    LOW
Pattern:     Usage of block timestamp
Description: Returned value relies on block timestamp.
Type:        Violation
Contract:    GoldGrinderV2
Line:        384
Source:
>     ) public view returns (uint256) {
>         uint256 secondsSinceLastHireTime = block.timestamp -
>                                            ^^^^^^^^^^^^^^^
>             users[adr].lastHireTime;


Severity:    LOW
Pattern:     Usage of block timestamp
Description: Returned value relies on block timestamp.
Type:        Conflict
Contract:    GoldGrinderV2
Line:        192
Source:
>         require(
>             block.timestamp - user.lastHireTime >= WITHDRAW_COOLDOWN,
>             ^^^^^^^^^^^^^^^
>             "must wait 24 hours before sell"

```
Note: to run the code via Docker with a Solidity version that is different than `0.5.12`, you will need to modify the variable `ARG SOLC=0.5.12` at the top of the `Dockerfile` to point to your version. After building with the correct version, you should not run into errors.



Install
===

## Prerequisites
The following instructions assume that a Python is already installed. In addition to that, Securify requires `solc`, `souffle` and `graphviz` to be installed on the system:

### [Solc](https://solidity.readthedocs.io/en/v0.5.10/installing-solidity.html) 
```
sudo add-apt-repository ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install solc
```

### [Souffle](https://souffle-lang.github.io/install) 

Follow the instructions here: https://souffle-lang.github.io/download.html

*Please do not opt for the unstable version since it might break at any point.*

### [Graphviz / Dot](https://www.graphviz.org/download/)
```
sudo apt install graphviz
```

## Setting up the virtual environment

After the prerequisites have been installed, we can set up the python virtual environment from which we will run the scripts in this project. 

In the project's root folder, execute the following commands to set up and activate the virtual environment:

```
virtualenv --python=/usr/bin/python3.7 venv
source venv/bin/activate
```

Verify that the `python` version is actually `3.7`:

```
python --version
```

Set `LD_LIBRARY_PATH`:
```
cd <securify_root>/securify/staticanalysis/libfunctors
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:`pwd`
```

Finally, install the project's dependencies by running the following commands from the `<securify_root>` folder:
```
pip install --upgrade pip
pip install -r requirements.txt
pip install -e .
```

Now you're ready to start using the securify framework.

Remember: Before executing the framework's scripts, you'll need to activate the virtual environment with the following command:
```
source venv/bin/activate
```

Usage
===

## Analyzing a contract
Currently Securify2 supports only flat contracts, i.e., contracts that do not contain import statements.

To analyze a local contract simply run:
```
securify <contract_source>.sol [--use-patterns Pattern1 Pattern2 ...]
```
Or download it from the Blockchain using the Etherscan.io API:
```
securify <contract_address> --from-blockchain [--key <key-file>]
```
*Notice that you need an API-key from Etherscan.io to use this functionality.*

To analyze a contract against specific severity levels run:
```
securify <contract_source>.sol [--include-severity Severity1 Severity2]
securify <contract_source>.sol [--exclude-severity Severity1 Severity2]
```
To get all the available patterns run:
```
securify --list
```

Supported vulnerabilities
===


| ID | Pattern name | Severity | Slither ID | SWC ID | Comments |
|----|-------------| ---------|------------|--------|----------|
| 1 | TODAmount | Critical | - | [SWC-114](https://swcregistry.io/docs/SWC-114) |
| 2 | TODReceiver| Critical | - | [SWC-114](https://swcregistry.io/docs/SWC-114)|
| 3 | TODTransfer | Critical | - | [SWC-114](https://swcregistry.io/docs/SWC-114) |
| 4 | UnrestrictedWrite | Critical | - | [SWC-124](https://swcregistry.io/docs/SWC-124) | 
| 5 | RightToLeftOverride | High | `rtlo`| [SWC-130](https://swcregistry.io/docs/SWC-130) |
| 6 | ShadowedStateVariable | High | `shadowing-state`, `shadowing-abstract` | [SWC-119](https://swcregistry.io/docs/SWC-119) | 
| 7 | UnrestrictedSelfdestruct | High | `suicidal` | [SWC-106](https://swcregistry.io/docs/SWC-106) |
| 8 | UninitializedStateVariable | High | `uninitialized-state`| [SWC-109](https://swcregistry.io/docs/SWC-109) |
| 9 | UninitializedStorage | High | `uninitialized-storage`| [SWC-109](https://swcregistry.io/docs/SWC-109) |
| 10 | UnrestrictedDelegateCall | High | `controlled-delegatecall`| [SWC-112](https://swcregistry.io/docs/SWC-112) |
| 11 | DAO | High | `reentrancy-eth` | [SWC-107](https://swcregistry.io/docs/SWC-107) |
| 12 | ERC20Interface | Medium | `erc20-interface` | - |
| 13 | ERC721Interface | Medium | `erc721-interface` | - |
| 14 | IncorrectEquality | Medium | `incorrect-equality`| [SWC-132](https://swcregistry.io/docs/SWC-132) |
| 15 | LockedEther | Medium | `locked-ether` | - |
| 16 | ReentrancyNoETH | Medium | `reentrancy-no-eth` | [SWC-107](https://swcregistry.io/docs/SWC-107) |
| 17 | TxOrigin | Medium |`tx-origin` | [SWC-115](https://swcregistry.io/docs/SWC-115) |
| 18 | UnhandledException | Medium | `unchecked-lowlevel` | - |
| 19 | UnrestrictedEtherFlow | Medium | `unchecked-send` |[SWC-105](https://swcregistry.io/docs/SWC-105) |
| 20 | UninitializedLocal | Medium | `uninitialized-local` | [SWC-109](https://swcregistry.io/docs/SWC-109) |
| 21 | UnusedReturn | Medium | `unused-return` | [SWC-104](https://swcregistry.io/docs/SWC-104) |
| 22 | ShadowedBuiltin | Low | `shadowing-builtin` | - |
| 23 | ShadowedLocalVariable | Low | `shadowing-local` | - |
| 24 | CallToDefaultConstructor?| Low | `void-cst` | - |
| 25 | CallInLoop | Low | `calls-loop` | [SWC-104](https://swcregistry.io/docs/SWC-104) |
| 26 | ReentrancyBenign | Low | `reentrancy-benign` | [SWC-107](https://swcregistry.io/docs/SWC-107) |
| 27 | Timestamp | Low | `timestamp` | [SWC-116](https://swcregistry.io/docs/SWC-116) |
| 28 | AssemblyUsage | Info | `assembly` | - |
| 29 | ERC20Indexed | Info | `erc20-indexed` | - |
| 30 | LowLevelCalls | Info | `low-level-calls` | - |
| 31 | NamingConvention | Info | `naming-convention` | - |
| 32 | SolcVersion | Info | `solc-version` | [SWC-103](https://swcregistry.io/docs/SWC-103) |
| 33 | UnusedStateVariable | Info | `unused-state` | - |
| 34 | TooManyDigits | Info | `too-many-digits` | - |
| 35 | ConstableStates | Info | `constable-states` | - |
| 36 | ExternalFunctions | Info | `external-function` | - | 
| 37 | StateVariablesDefaultVisibility | Info | - | [SWC-108](https://swcregistry.io/docs/SWC-108) |

The following Slither patterns are not checked by Securify since they are checked by the Solidity compiler (ver. 0.5.8):
- `constant-function`
- `deprecated-standards`
- `pragma`

The following SWC vulnerabilities do not apply to Solidity contracts with pragma >=5.8 and are therefore not checked by Securify:

- SWC-118 (Incorrect Constructor Name)
- SWC-129 (Usage of +=)
