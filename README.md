
# bandit-LEVEL-walkthrough (Redacted)

## Warning
This repo contains step-by-step walkthroughs for Bandit levels with **flags redacted** to avoid spoilers. Commands and reasoning are provided.

---

## Objectives
- Show commands used to locate and extract the flag.
- Explain why each command helps.
- Provide a small practice file that mimics the challenge (no real flags).



🌟 level 0 to 1
    command - cat readme

🌟 level 1 to 2
    command - cat ./-

🌟 level 2 to 3
    command - cat ./--spaces\ in\ this\ filename--

🌟 level 3 to 4
    command i used - cat ./...HIding-From-You

🌟 level 4 to 5
    command i used - first determine the human readable file by
        file ./-*
        then cat ./-file07s

🌟 level 5 to 6 
            Permission	Sum of values	Digit	\
            No permissions	0	---	
            Execute only	1	--x	
            Write only  	2	-w-	
            Write + Execute	3	-wx	
            Read only	    4	r--	
            Read + Execute	5	r-x	
            Read + Write	6	rw-	
            Read + Write + Execute	7	rwx

            found the command by find, first i below the command that i used

                find ./ -type f -size 1033c -exec file {} \; 
                        this is to find a the file and check whether it is human readable or not 

                find ./ -type f -size 1033c -exec cat {} \; 
                        this is to run cat command to see which data contain in that file 
                        

🌟 level 6 to 7
 command i used for that one is 
            find / -type f -size 33c -user bandit7 -group bandit6 
             
        this gives me a error with permission denied so i added a extra thing 
            find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null 


🌟 level 7 to 8
 command i used for this section is - 
            cat data.txt | grep millionth 

            first i see the content in file and pipe it through grep to search millionth

        
🌟 level 8 to 9
 command i used for this section is 
            sort data.txt | uniq -u 

            first sort the data in data.txt and then use uniq -u to remove any duplicates and print the uniq one

🌟 level 9 to 10
   command i used for this level is 
                strings data.txt | grep =

                first get humanreadable and grep = 
                then the password 

🌟 level 10 to 11
                command i used for this level is 
                    base64 -d data.txt 

                    first using base64 -d to decode simmilarly i can use base64 --decode then file name 
                    then the password appear

🌟 level 11 to 12
                        this is rot13 alrorithm 
                        command i used here is 

                        cat data.txt | tr "A-Za-z" "N-ZA-Mn-za-m"   

🌟 level 12 to 13
                first i used command is 
                step 01 
                        *    xxd -r data.txt output
                        this reverse convert the hexdump data back into the binary data so i can analyse the binary data what 
                        it has been compressed 

                            Gzip: the bytes often start with 1F 8B (hex).

                            bzip2: often begins with ASCII BZh.

                            xz: begins with bytes corresponding to the ASCII \xFD7zXZ.

                            Zip / PKZip: begins with ASCII PK.

                            tar: tar itself doesn’t have a single fixed first magic sequence for all tarfiles, but an archive 
                            might be a tar wrapped in a compression format.

                            Plain text: lots of printable ASCII characters; you might see your password directly.
                            Knowing these signatures helps you choose the appropriate decompression step.

                step 02 
                        
                        then i checked file type using 
                            file output 

                            it is gzip file
                                cp output gzip.gz

                        so i decompress it by 
                                gzip -d gzip.gz
                                cp gzip bzip2.bz2
                        
                        then i recheck it again, it is bzip compressed file. so decompress it 
                                bzip2 -d bzip2.bz2
                        
                        then i recheck it again it is a gzip file also 
                                cp bzip2 gzip2.gz 
                                gzip -d gzip2.gz


 ![bandit 12 image](images/bandit%2012%20to%2013.png)       

                            
🌟 level 13 to 14
     command i used for this level is 
        ssh -i ./sshkey.private bandit14@bandit.labs.overthewire.org -p 2220 

        this is reads the private key and authenticate it in overthewire bandit 14 server 


🌟 level 14 to 15
        command i used for this level is 
            telnet localhost 30000
            
            and enter the password for level 14 
