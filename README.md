# CS690UnderstandingEthereum

## Developer: Charles Ge, Jinyue Song

## Overall process of comparing TX fee and Processing time
1. Collect live data at AWS and Ali Cloud. 
2. Clean the duplicate TXs, download to local machine, and do the matching. 
3. Serialize un-matched TXs and blocks on disk for the next matching. 

## Do the routine matching:

1. Log in to AWS, or Ali Cloud
2. Go to cs690/go-ethereum/analysis-tool-python
3. Run python3 clean_records.py to "set" all TXs with the earliest recieved time. 
4. If cleaning said date format is wrong, go to go-ethereum/records/txs, open the file, change the wrong format(usually just use the previous line's timestamp). You can vi the file, click '/', paste the hash value, hit the button, then VI would locate that line. 
5. clean_records.py would clean the duplicate txs of all txs.txt until yesterday, move all cleaned files to backup folder, and leave the cleaned ones in records/txs/cleaned.
6. Download all cleaned files to local. Here's the command: 
scp -i "~/.ssh/cs690ethereum.pem" ubuntu@ec2-18-144-14-139.us-west-1.compute.amazonaws.com:/home/ubuntu/cs690/go-ethereum/records/txs/cleaned/* ~/charles/university/Master\ Project/go-ethereum/records/txs/cleaned/
7. On local machine, first change the path of last saved object to load the latest saved state, then run load_txt.py to match all TXs. It would first load serialized object, then load latest TXs and blocks, then do the match, then save the matched TXs, then serialize the remaining object. 
8. On AWS, move all txs.txt at records/txs/cleaned/ to records/txs/cleaned/backup.


