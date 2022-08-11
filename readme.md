## Dump Marscoin addresses with positive balance

Simple utility to list all bitcoin addresses with positive balance. It works by analysing the current unspent transaction output set (UTXO), aggregating outputs to same addresses together and write them to csv file.

#### Prequisities:
python 2.7  
pip

#### To install:  
run pip install -r requirements.txt

or install following packages with pip manualy

for linux：
* plyvel
* base58
* sqlite3

for windows：
* plyvel-win32
* base58
* pysqlite3

#### Usage
To use this script, you will need copy of chainstate database as created by marscoind node. 

To get current addresses with positive balance, let the full node client sync with the network. 
**Stop** the bitcoin-core client before running this utility. If you not stop the client, the database might get corrupted.  
Then run this program with path to chainstate directory (usualy $HOME/.marscoin/chainstate).

Show help
```
python2 marsposbal2csv.py -h
```
#### Example:  
The following will read from `/home/USER/.marscoin/chainstate`, and write result to `/home/USER/addresses_with_balance.csv`.
```
python2 marsposbal2csv.py --marscoin_version=0.14 /home/USER/.marscoin/chainstate /home/USER/addresses_with_balance.csv
```

##### Notice
* The output may not be complete as there are some transactions which are not understood by the decoding lib, or that which do not have "address" at all. Such transactions are not processed. Number of them and the total ammount in such transactions is displayed after the analysis.  
* The output csv file only reflects the chainstate leveldb at your disk. So it will always be few blocks behind the network as you need to stop the marscoind client.

#### Converting to RIPEMD160
Per request, I'm adding script which is able to convert MARS address to RIPEMD160 representation.
MARS address must be in fist column, RIPEMD160 is added to csv. Output goes to stdout.

Example:
```
python2 convert2ripemd160.py /home/USER/addresses_with_balance.csv
```

#### Acknowledgement
This utility builds on very nice [bitcoin_tools](https://github.com/sr-gi/bitcoin_tools/) lib,
 which does the UTXO parsing.
 
#### Support
If you like this utility, please consider supporting the bitcoin_tools library which does all the heavy lifting.

If this particular functionality made your life easier you can support coffee consumption in BTC 
1FxC1mgJkad63beJcECfZMRaFSf4PBLr2f.

## FAQ
- Python 3 does not work. Yes, the the code is for python 2 - as stated in the requirements.
- Derived from its original Bitoin implementation
