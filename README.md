# CoRF


## Demo Video
[![CoRF](https://res.cloudinary.com/marcomontalbano/image/upload/v1721658637/video_to_markdown/images/youtube--na0dStb2gfE-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/na0dStb2gfE "CoRF")

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

### Analyze Your Own Smart Contracts

#### Initializing File Structure with `truffle`

- Create a new folder named `test` in the path `rlf/example`. Open a terminal in this folder and execute:

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

- Copy the files from rlf/example/crowdsale/migrations to the migrations folder.

- Copy Migrations.sol and the contract files you want to test from rlf/example/crowdsale/contracts to the contracts folder.

- Modify the compiler's version in truffle-config.js if you're working with older contracts.
