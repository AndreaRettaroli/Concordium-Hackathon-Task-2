# setup

### 1. Install and init project

````
cargo install --locked cargo-generate
cargo concordium init
````

### 2. Build, Test's smartcontract

````
cd counter-template
cargo concordium build -e --out ./my_concordium_project.wasm.v1
cargo concordium test
````


### 3. Build dist and Deploy

````
mkdir dist
cargo concordium build --out dist/module.wasm.v1 --schema-out dist/schema.bin
````

# deploy

````
concordium-client module deploy dist/module.wasm.v1 --sender andrea1  --name andrea-greeter --grpc-port 10000 --grpc-ip node.testnet.concordium.com
````

![deploy](https://github.com/AndreaRettaroli/Concordium-Hackathon-Task-2/blob/master/img/deploy.PNG)

TX:
````
  dd1999db2a61c88558ac409a6f713888a2010c448cb485e77bb8d85605a297fc
````


# init 

````
concordium-client contract init andrea-greeter --sender andrea1 --energy 10000 --contract hackathon_task2 --parameter-json init-param.json --schema .\dist\schema.bin --grpc-port 10000 --grpc-ip node.testnet.concordium.com 
````

![init](https://github.com/AndreaRettaroli/Concordium-Hackathon-Task-2/blob/master/img/init.PNG)
TX:
````
aebffc646a996d6a787ca1cb88f6abcf8e0c56820aa998778002d878cac5be02
````
Params:
````
{
  "description": "Set New Greeting Here"
}
````



# update 
````
concordium-client contract update 2792 --entrypoint set_greeting --energy 10000 --sender andrea1   --parameter-json update-param.json --schema .\dist\schema.bin --grpc-port 10000 --grpc-ip node.testnet.concordium.com 
````

![update](https://github.com/AndreaRettaroli/Concordium-Hackathon-Task-2/blob/master/img/update.PNG)

TX:
````
e8cfe71e91008b9b54ba9038e98e75f259eba6c059a21c8c0aef29e3caa1e563
````
Params:
````
"Hello World!"
````

# Invoke
````
concordium-client contract invoke 2792 --entrypoint view --grpc-port 10000 --grpc-ip node.testnet.concordium.com 
````
![invoke](https://github.com/AndreaRettaroli/Concordium-Hackathon-Task-2/blob/master/img/invoke.PNG)

Mainnet Wallet address
Concordium address:  3mbLgjjYf6YKPiNt7jyyrAKv4xTF46kKMceEmuC8BLjJDGPMsS