# CS690UnderstandingEthereum
## Developer: Charles Ge, Jinyue Song

## Transaction fee and processing time
### dataset structure
```markdown
records
+-- ali_txs
+-- aws_txs
+-- blocks
    +-- ali
    +-- aws
    +-- canonical 
+-- matched
+-- one_week 
    +-- ali_blocks
    +-- ali_matched
    +-- ali_tx_non_canonical_log
    +-- ali_txs
    +-- aws_blocks
    +-- aws_matched
    +-- aws_tx_non_canonical_log
    +-- aws_txs
```
### Reproduce

#### Run load_txt_j.py:
EthereumData object is defined in this file. 
1. Run this run() function, the object loads aws transactions from records/aws_txs/ 
and matches transactions in the canonical chain /blocks/canonical/. 
Then, the aws matched transactions are saved in the /records/matched/.
After matching, I copy the matched result to /records/one_week/aws_matched. 
And delete files in /records/matched/. 

2. Comment out the line with /aws_txs/ and comment back the line with /ali_txs/.
And run run() function again. 
Then, copy the matched ali transactions from records/matched/ to /records/one_week/ali_matched.

#### Run compare_tx_peer_time.py:
Add the time intervals to check which transactions have the experience in the uncle blocks.
The first and second arguments are the range for the time interval. 
(0, 100) means the transactions with processing time between 0 and 100 seconds will be checked.  
For example:
```python
     ed = EthereumData() 
     ed.count_txs_in_uncle(0, 100)
```


#### Run get_txs_peers.py:
1. In the output file /records/one_week/ali_tx_non_canonical_log, 
copy the transaction with large processing time and small fee.

2. Paste the transaction information into the json.loads(). 

3. Create the object, set this_tx as the first argument and run.
\
3.1 After the first time running, the data will be serialized. 
Comment out the lines in the run function before pickle.load() 
and comment back the line pickle.load().

4. Adjust the analysis functions.  
 

