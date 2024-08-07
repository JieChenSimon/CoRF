# CoRF


## Demo Video
[![CoRF](https://res.cloudinary.com/marcomontalbano/image/upload/v1721658637/video_to_markdown/images/youtube--na0dStb2gfE-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/na0dStb2gfE "CoRF")

### Setup

1. Install [solc](https://github.com/ethereum/solidity) 0.4.25:
```
$ wget https://github.com/ethereum/solidity/releases/download/v0.4.25/solc-static-linux
$ chmod +x solc-static-linux
$ sudo mv solc-static-linux /usr/bin/solc
```

2. Install [golang](https://golang.org/), for example:
```
wget https://dl.google.com/go/go1.10.4.linux-amd64.tar.gz
tar -xvf go1.10.4.linux-amd64.tar.gz
sudo mv go /usr/lib/go-1.10

Note: Then you should set `GOPATH` to CoRF folder.
```

3. Install Ollama and pull the base LLMs
```
curl https://ollama.ai/install.sh |sh
ollama pull codegemma
ollama pull llama3.1
ollama pull llama3.1:70b
ollama pull llama3
ollama pull llama2:13b
ollama pull gemma2:27b
ollama pull codellama
ollama pull codegemma
ollama pull qwen:32b
```

4. Install python dependencies:
```
pip3 install -r requirements.txt
```

5. Install execution backend:
```
go build -o execution.so -buildmode=c-shared export/execution.go
```

-----------------------------------------------------------

### Generate Transaction.json
```
python3 script/extract.py --proj example/wallet --port 8545 --fuzz_contract Wallet
```
### Run with Bash Script
```
cd CoRF
./start-safe.sh
```
### Run with Command line 
```
python3 -m llmfuzz --proj example/crowdsale/ --contract Crowdsale --fuzzer llmAgent --limit 2000 --max_rounds 15 --llm codegemma-fuzz

python3 -m llmfuzz --proj example/wallet/ --contract Wallet --fuzzer llmAgent --limit 2000 --max_rounds 15 --llm codegemma-fuzz
```
### Run with Bash script (safe retry)
```
./start-safe.sh
```
or
### Run with overall time limit

```
time 600 python3 -m llmfuzz --proj example/crowdsale/ --contract Crowdsale --fuzzer llmAgent --limit 2000 --max_rounds
```

-----------------------------------------------------------

### Analyze Your Own Smart Contracts (Step-by-Step Guides)

#### 1. Initializing File Structure with `truffle`

- Create a new folder, such as `test`, in the path `CoRF/example`. Open a terminal in this folder and execute:

  ```shell
  truffle init
  ```
 ```shell
  |-- contracts
  |-- migrations
  |-- test
  `-- truffle-config.js
  
  3 directories, 1 file
  ```

- Copy the files from CoRF/example/crowdsale/migrations to the migrations folder.

- Copy Migrations.sol and the contract files you want to test from CoRF/example/crowdsale/contracts to the contracts folder.

- Modify the compiler's version in truffle-config.js if you're working with older contracts.

#### 2. Generating corresponding transitions.json File

```
python3 script/extract.py --proj /example/test
```
Then, a transitions.json file will be generated in the initialized folder path along with the compiled contract files. For example:

  ```shell
  |-- build
  |   `-- contracts
  |       |-- Migrations.json
  |       `-- Rubixi.json
  |-- contracts
  |   |-- Migrations.sol
  |   `-- rubixi.sol
  |-- migrations
  |   |-- 1_initial_migration.js
  |   `-- 2_deploy_contracts.js
  |-- test
  |-- transactions.json
  `-- truffle-config.js
  ```
