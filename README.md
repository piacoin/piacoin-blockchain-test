# PiaCoin Blockchain Test

[Join the chat at Gitter](https://gitter.im/fork-ethereum/Lobby)

## Installation

### Docker

1. **Install Docker**

    ```bash
    docker pull forkblockchain/fork-ethereum:latest
    ```

2. **Docker Compose**

    ```bash
    docker-compose up -d
    ```

    then

    ```bash
    ./enter-docker.sh
    cd /ethereum
    ```

### Vagrant

1. **Install VirtualBox**
2. **Install Vagrant**

    ```bash
    vagrant up --provision
    cd /home/ethereum/
    ```

## Initialization of Chain

### Geth Commands

1. **Initialize Genesis**

    ```bash
    ./init-genesis.sh
    ```

2. **Start Geth**

    ```bash
    ./start-geth.sh
    ```

3. **Connect to Geth**

    ```bash
    ./connect-geth.sh
    ```

## Account Setup Commands

1. **Create New Account**

    ```javascript
    personal.newAccount();
    ```

    or (need to specify passphrase as argument in container)

    ```javascript
    personal.newAccount("YOUR PASSPHRASE");
    ```

2. **Show Balance**

    ```javascript
    eth.getBalance(eth.accounts[0]);
    ```

3. **Generate DAG and Mine Coins**

    ```javascript
    miner.start();
    ```

    ```javascript
    miner.stop();
    ```

## Smart Contract Example

### Contract Commands

1. **Load Script**

    ```javascript
    loadScript("simple.js");
    ```

2. **Parse Simple Contract**

    ```javascript
    var parsedSimpleContract = web3.eth.contract(JSON.parse(simpleContract.contracts["simple.sol:Simple"].abi));
    ```

3. **Unlock Account**

    ```javascript
    personal.unlockAccount(eth.accounts[0], "YOUR PASSPHRASE");
    ```

4. **Log Mined Contract**

    ```javascript
    var simpleContract = parsedSimpleContract.new({ 
        from: eth.accounts[0], 
        data: "0x" + simpleContract.contracts["simple.sol:Simple"].bin, 
        gas: 4700000
    }, function (e, contract) {
        console.log(e, contract);
        if (typeof contract.address !== 'undefined') {
            console.log('Contract mined! address: ' + contract.address + ' transactionHash: ' + contract.transactionHash);
        }
    });
    ```

5. **Mine Contract**

    ```javascript
    miner.start();
    ```

    ```javascript
    miner.stop();
    ```

6. **Execute Locally**

    ```javascript
    simpleContract.multiply.call(9,2);
    ```

7. **Execute on EVM**

    ```javascript
    simpleContract.multiply.sendTransaction(2,2,{from:eth.accounts[0]})
    ```

8. **Process Smart Contract Transaction**

    ```javascript
    miner.start();
    ```

    ```javascript
    miner.stop();
    ```

9. **View Logged Events**

    ```javascript
    var simpleContractEvents = simpleContract.allEvents({fromBlock: 0, toBlock: 'latest'});
    simpleContractEvents.get(function(error, logs) {
        logs.forEach( function(log,error) {
            console.log(JSON.stringify(log.args));
        })
    });
    ```

## References

- [Puppeth](https://modalduality.org/posts/puppeth/)
- [Private Network](https://github.com/ethereum/go-ethereum/wiki/Private-network)
- [Default Bootnodes](https://github.com/ethereum/go-ethereum/blob/master/params/bootnodes.go)
- [First Steps with Ethereum Private Networks and Smart Contracts](https://alanbuxton.wordpress.com/2017/07/19/first-steps-with-ethereum-private-networks-and-smart-contracts-on-ubuntu-16-04/)
- [How to Compile Solidity Contracts with Geth v1.6](https://ethereum.stackexchange.com/questions/15435/how-to-compile-solidity-contracts-with-geth-v1-6)
