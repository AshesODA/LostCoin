# LostCoins v4.4
 - This is a modified version [VanitySearch](https://github.com/JeanLucPons/VanitySearch/). 
Huge thanks [kanhavishva](https://github.com/kanhavishva) and to all developers whose codes were used in LostCoins.
## Quick start
- Сonvert addresses into binary hashes RIPEMD160 use [b58dec.exe](https://github.com/phrutis/LostCoins/blob/main/Others/b58dec.exe) Сommand: ```b58dec.exe addresses.txt base160.bin```
- It is important to sort the base160.bin file otherwise the Bloom search filter will not work as expected.
- To sort base160.bin use the program [RMD160-Sort.exe](https://github.com/phrutis/LostCoins/blob/main/Others/RMD160-Sort.exe) Сommand: ```RMD160-Sort.exe base160.bin hex160-Sort.bin``` 
- For Multi 3 GPUs use ```LostCoins.exe -t 0 -g -i 0,1,2 -x 256,256,256,256,256,256 -f test.bin -r 4 -s 252 -z 256 -m 500```  
- **Do not use the GPU+CPU will drop the speed!**
- You can search hashes160 of other coins, if it finds it, it will give an empty legacy address 1.. and positive private key and hex160
## Parametrs:
```
C:\Users\user>LostCoins.exe -h
Usage: LostCoins [options...]
Options:
    -v, --version          Print version. For help visit https://github.com/phrutis/LostCoins
    -c, --check            Check the working of the code LostCoins
    -u, --uncomp           Search only Uncompressed addresses
    -b, --both             Search both (Uncompressed and Compressed addresses)
    -g, --gpu              Enable GPU calculation
    -i, --gpui             GPU ids: 0,1...: List of GPU(s) to use, default is 0
    -x, --gpux             GPU gridsize: g0x,g0y,g1x,g1y, ...: Specify GPU(s) kernel gridsize, default is 8*(MP number),128
    -t, --thread           ThreadNumber: Specify number of CPUs thread, default is number of core
    -o, --out              Outputfile: Output results to the specified file, default: Found.txt
    -m, --max              -m  1-10000 For GPU: Reloads random started hashes every billions in counter. Default: 100 billion
    -s, --seed             PassPhrase   (Start bit range)
    -z, --zez              PassPhrase 2 (End bit range)
    -e, --nosse            Disable SSE hash function. Use for older CPU processor if it fails 
    -r, --rkey             Number of random modes
    -n, --nbit             Number of letters and number bit range 1-256
    -f, --file             RIPEMD160 binary hash file path
    -d, --diz              Display modes -d 0 [info+count], -d 1 SLOW speed [info+hex+count], Default -d 2 [count] HIGH speed
    -k, --color            Text color: -k 1-255 Recommended 3, 10, 11, 14, 15 (default: -k 15)
    -h, --help             Shows this page
 ```
###  Search Passphrases 
- [**Use old databases or Generator to search for passphrases**](https://github.com/phrutis/LostCoins/blob/main/Others/Modes.md) 
## Mode 0 
## Find Passphrases and Privat keys from a text file
### Passphrases from a file
 - To search for passphrases, use mode **-u** or **-b** for old Lost Coins 
 - Each passphrase on a new line. To repeatedly convert each passphrase to sha256-> sha256 use **-t 1 -n 1-256** how many times (slow).
 - For CPU (NORMAL) ```LostCoins.exe -b -t 6 -f test.bin -r 0 -s Passphrases.txt -d 3``` 
 - For CPU (TEST) ```LostCoins.exe -b -t 6 -f test.bin -r 0 -s Passphrases.txt -d 0```
 - For CPU (TEST 2)  ```LostCoins.exe -b -t 6 -f test.bin -r 0 -s Passphrases.txt -d 1```
```
C:\Users\user>LostCoins.exe -b -t 6 -f all.bin -r 0 -s test2021.txt -d 3

 LostCoins v4.4 (03.10.2021)

 SEARCH MODE  : COMPRESSED & UNCOMPRESSED
 DEVICE       : CPU
 CPU THREAD   : 6
 GPU IDS      : 0
 GPU GRIDSIZE : -1x128
 RANDOM MODE  : 0
 ROTOR SPEED  : HIGH (only counter)
 CHARACTERS   : 0
 PASSPHRASE   : test2021.txt
 PASSPHRASE 2 :
 DISPLAY MODE : 3
 TEXT COLOR   : 15
 GPU REKEY    : 100000000000
 HASH160 FILE : all.bin
 OUTPUT FILE  : Found.txt

 Loading      : 100 %
 Loaded       : 32,892,770 address

Bloom at 00000196B597DFA0
  Version     : 2.1
  Entries     : 65785540
  Error       : 0,0000010000
  Bits        : 1891674723
  Bits/Elem   : 28,755175
  Bytes       : 236459341 (225 MB)
  Hash funcs  : 20

  Start Time  : Fri Oct  3 12:41:57 2021

  Random mode : 0
  Rotor       : Loading passphrases from file test2021.txt ...
  Loaded      : 1999999998 passphrases
  Rotor       : Only letters and symbols are supported: А-Яа-яA-Za-z0-9ёЁьЪЬъ `~!@#$&*()-_=+{}|;:'<>,./? others will be skipped!
  Rotor       : For large files use -t 11 max (1 core = ~30.000/s, 1 thread = ~5.000/s) Text file max 2,147,483,647 lines!
  Site        : https://github.com/phrutis/LostCoins
  Donate      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9

  [05:21:11] [CPU: 118,97 Kk/s] [T: 2,037,282,361] [F: 0]
  Search is Finish! (1999378472) passphrases checked from total (1999999998). Found: (0)
  Skipped passphrases with incorrect letters, characters (621526)
  Check the file test2021.txt for incorrect characters, remove the garbage from 621526 passphrases and try again.
  Help by link https://github.com/phrutis/LostCoins/issues/16
```
### Privat keys from a file
 - For CPU (NORMAL) ```LostCoins.exe -b -t 6 -f test.bin -r 0 -s private-keys.txt -z keys -d 3```
 - Private key (HEX) looks like this only numbers 0-9 and letters a,b,c,d,e,f on a new line. 
 - Example: 4A70FE9AA6436E02C2DEA340FBD1E352E4EF2D8CE6CA52AD25D4B95471FC8BF2
```
C:\Users\user>LostCoins.exe -b -t 11 -f test.bin -r 0 -s private-keys.txt -z keys -d 3

  LostCoins v4.4 (03.10.2021)

 SEARCH MODE  : COMPRESSED & UNCOMPRESSED
 DEVICE       : CPU
 CPU THREAD   : 11
 GPU IDS      : 0
 GPU GRIDSIZE : -1x128
 RANDOM MODE  : 0
 CHARACTERS   : 0
 PASSPHRASE   : private-keys.txt
 PASSPHRASE 2 : keys
 DISPLAY MODE : 3
 TEXT COLOR   : 15
 HASH160 FILE : test.bin
 OUTPUT FILE  : Found.txt

 Loading      : 100 %
 Loaded       : 75,471 address

Bloom at 000001AA8719F8D0
  Version     : 2.1
  Entries     : 150942
  Error       : 0,0000010000
  Bits        : 4340363
  Bits/Elem   : 28,755175
  Bytes       : 542546 (0 MB)
  Hash funcs  : 20

  Start Time  : Sun Oct  3 17:26:25 2021

  Random mode : 0
  Rotor       : Loading private keys from file: private-keys.txt ...
  Loaded      : 79437575 private keys
  Rotor       : Only letters and symbols: А-Яа-яA-Za-z0-9ёЁьЪЬъ `~!@#$&*()-_=+{}|;:'<>,./? others will be skipped!
  Rotor       : For large files use -t 11 max (1 core = ~30.000/s, 1 thread = ~5.000/s) Text file max 2,147,483,647 lines!
  Site        : https://github.com/phrutis/LostCoins
  Donate      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9

  [00:04:42] [CPU: 182,36 Kk/s] [T: 42,379,168] [F: 0]
  =================================================================================
  * PubAddress: 162TRPRZvdgLVNksMoMyGJsYBfYtB4Q8tM                                *
  * Priv(WIF) : p2pkh:5JiznUZskJpwodP3SR85vx5JKeopA3QpTK63BuziW8RmGGyJg81        *
  * Priv(HEX) : 77AF778B51ABD4A3C51C5DDD97204A9C3AE614EBCCB75A606C3B6865AED6744E  *
  =================================================================================
  [00:08:46] [CPU: 183,23 Kk/s] [T: 86,849,487] [F: 1]
  Search is Finish! (79437575) passphrases checked from total (79437575). Found: (1)
  Skipped passphrases with incorrect letters, characters (0)
```
## Mode 1 
### GPU fast sequential search from start to end of private keys
 - The range is divided into parts and many streams for quick searching. 
 - Unlike sequential search, you can find a private key in 2 seconds without waiting for a full search of the range. 
 - For GPU ```LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 1 -s ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff0000000000 -z ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ffffffffffff -d 4 -n 5```
 - To continue searching, run the LostCoins-Continue.bat file or add -m 777 (the baht file must exist) 
 - -n 1-1200 (~ after how many minutes to save the search position. default: 60 min.)

 ```
C:\Users\user>LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 1 -s ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff0000000000 -z ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ffffffffffff -d 4 -n 5

 LostCoins v4.4 (03.10.2021)

 SEARCH MODE  : COMPRESSED
 DEVICE       : GPU
 CPU THREAD   : 0
 GPU IDS      : 0
 GPU GRIDSIZE : 256x256
 RANDOM MODE  : 1
 CHARACTERS   : 5
 PASSPHRASE   : ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff0000000000
 PASSPHRASE 2 : ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ffffffffffff
 DISPLAY MODE : 4
 TEXT COLOR   : 15
 HASH160 FILE : test.bin
 OUTPUT FILE  : Found.txt

 Loading      : 100 %
 Loaded       : 75,471 address

Bloom at 00000271BD71C6A0
  Version     : 2.1
  Entries     : 150942
  Error       : 0,0000010000
  Bits        : 4340363
  Bits/Elem   : 28,755175
  Bytes       : 542546 (0 MB)
  Hash funcs  : 20

  Start Time  : Sun Oct  3 17:40:52 2021

  Random mode : 1
  Random      : Finding in a range
  Global start: BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF0000000000 (256 bit)
  Global end  : BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FFFFFFFFFFFF (256 bit)
  Global range: 000000000000000000000000000000000000000000000000000000FFFFFFFFFF (40 bit)
  Rotor       : Save checkpoint every 5 minutes to file LostCoins-Continue.bat
  Site        : https://github.com/phrutis/LostCoins
  Donate      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9

  GPU         : GPU #0 NVIDIA GeForce RTX 2070 (36x64 cores) Grid(256x256)

  Divide the range FFFFFFFFFF into 65536 threads for fast parallel search
  Thread 00000: BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF0000000000 -> BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF0001FFFFFE
  Thread 00001: BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF0001FFFFFE -> BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF0002FFFFFD
  Thread 00002: BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF0002FFFFFD -> BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF0003FFFFFC
  Thread 00003: BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF0003FFFFFC -> BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF0004FFFFFB
          ... :
  Thread 65533: BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FFFFFDFF0002 -> BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FFFFFEFF0001
  Thread 65534: BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FFFFFEFF0001 -> BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FFFFFFFF0000
  Thread 65535: BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FFFFFFFF0000 -> BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB411000000FEFFFF

  [00:00:10] [BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF0288000000] [CPU+GPU: 1083,22 Mk/s] [GPU: 1083,22 Mk/s] [C: 0%] [T: 10,871,635,968 (34 bit)] [F: 0]
  =================================================================================
  * PubAddress: 1PoQRMsXyQFSqCCRek7tt7umfRkJG9TY8x                                *
  * Priv(WIF) : p2pkh:L3UBXym7JYcMX91ssLgZzS2MvxTxjU3VRf9S4jJWXVFdDi4NsLcm        *
  * Priv(HEX) : BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF61F20015AD  *
  =================================================================================
  [00:13:18] [BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FFC048000000] [CPU+GPU: 1037,92 Mk/s] [GPU: 1037,92 Mk/s] [C: 75%] [T: 825,841,680,384 (40 bit)] [F: 1]
 ```
 ### CPU search from start Private key 
  - One core, does not stop )
  - For CPU ```LostCoins.exe -t 1 -f test.bin -r 1 -s ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f0000000 -z ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61ffffffff -d 6```
 ```
C:\Users\user>LostCoins.exe -t 1 -f test.bin -r 1 -s ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f0000000 -z ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61ffffffff -d 6

 LostCoins v4.4 (03.10.2021)

 SEARCH MODE  : COMPRESSED
 DEVICE       : CPU
 CPU THREAD   : 1
 GPU IDS      : 0
 GPU GRIDSIZE : -1x128
 RANDOM MODE  : 1
 CHARACTERS   : 0
 PASSPHRASE   : ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f0000000
 PASSPHRASE 2 : ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61ffffffff
 DISPLAY MODE : 6
 TEXT COLOR   : 15
 HASH160 FILE : test.bin
 OUTPUT FILE  : Found.txt

 Loading      : 100 %
 Loaded       : 75,471 address

Bloom at 000002E594E1DFA0
  Version     : 2.1
  Entries     : 150942
  Error       : 0,0000010000
  Bits        : 4340363
  Bits/Elem   : 28,755175
  Bytes       : 542546 (0 MB)
  Hash funcs  : 20

  Start Time  : Sun Oct  3 17:56:09 2021

  Random mode : 1
  Random      : Finding in a range
  Global start: BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF61F0000000 (256 bit)
  Global end  : BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF61FFFFFFFF (256 bit)
  Global range: 000000000000000000000000000000000000000000000000000000000FFFFFFF (28 bit)
  Site        : https://github.com/phrutis/LostCoins
  Donate      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9

  [00:00:48] [BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF61FBDA5000] [CPU+GPU: 4,03 Mk/s] [GPU: 0,00 Mk/s] [T: 198,856,704] [F: 0]
  =================================================================================
  * PubAddress: 1PoQRMsXyQFSqCCRek7tt7umfRkJG9TY8x                                *
  * Priv(WIF) : p2pkh:L3UBXym7JYcMX91ssLgZzS2MvxTxjU3VRf9S4jJWXVFdDi4NsLcm        *
  * Priv(HEX) : BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF61F20015AD  *
  =================================================================================
  [00:01:02] [BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF61FF05D000] [CPU+GPU: 4,04 Mk/s] [GPU: 0,00 Mk/s] [T: 252,039,168] [F: 1]
 ```
 ## Mode 2
 ### Exact accurate bit by bit search in a range
 - For GPU ```LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 2 -n 64 -m 99```
 ```
C:\Users\user>LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 2 -n 64 -m 99

 LostCoins v4.4 (03.10.2021)

 SEARCH MODE  : COMPRESSED
 DEVICE       : GPU
 CPU THREAD   : 0
 GPU IDS      : 0
 GPU GRIDSIZE : 256x256
 RANDOM MODE  : 2
 CHARACTERS   : 64
 PASSPHRASE   :
 PASSPHRASE 2 :
 DISPLAY MODE : 2
 TEXT COLOR   : 15
 GPU REKEY    : 99000000000
 HASH160 FILE : test.bin
 OUTPUT FILE  : Found.txt

 Loading      : 100 %
 Loaded       : 75,471 address

Bloom at 000001C477BABD20
  Version     : 2.1
  Entries     : 150942
  Error       : 0,0000010000
  Bits        : 4340363
  Bits/Elem   : 28,755175
  Bytes       : 542546 (0 MB)
  Hash funcs  : 20

  Start Time  : Sun Oct  3 17:57:53 2021

  Random mode : 2
  Random      : Finding in a range
  Use range   : 64 (bit)
  Rotor       : Random generate hex in range 64
  Rotor GPU   : Reloading starting hashes in range 64 (bit) every 99.000.000.000 on the counter
  Site        : https://github.com/phrutis/LostCoins
  Donate      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9

  GPU         : GPU #0 NVIDIA GeForce RTX 2070 (36x64 cores) Grid(256x256)

  [00:01:26] [CPU+GPU: 1046,44 Mk/s] [GPU: 1046,44 Mk/s] [T: 91,402,272,768] [F: 0]
 ```
  ### Exact accurate bit by bit search in a range 
 - For CPU ```LostCoins.exe -t 6 -f test.bin -r 2 -n 64 -d 2``` Speed
 - For CPU ```LostCoins.exe -t 6 -f test.bin -r 2 -n 64 -d 0``` Normal
 - For CPU ```LostCoins.exe -t 6 -f test.bin -r 2 -n 64 -d 1``` Slow
  ```
  C:\Users\user>LostCoins.exe -t 6 -f test.bin -r 2 -n 256 -d 2

 LostCoins v4.4 (03.10.2021)

 SEARCH MODE  : COMPRESSED
 DEVICE       : CPU
 CPU THREAD   : 6
 GPU IDS      : 0
 GPU GRIDSIZE : -1x128
 RANDOM MODE  : 2
 CHARACTERS   : 256
 PASSPHRASE   :
 PASSPHRASE 2 :
 DISPLAY MODE : 2
 TEXT COLOR   : 15
 GPU REKEY    : 100000000000
 HASH160 FILE : test.bin
 OUTPUT FILE  : Found.txt

 Loading      : 100 %
 Loaded       : 75,471 address

Bloom at 000001A60AC5D130
  Version     : 2.1
  Entries     : 150942
  Error       : 0,0000010000
  Bits        : 4340363
  Bits/Elem   : 28,755175
  Bytes       : 542546 (0 MB)
  Hash funcs  : 20

  Start Time  : Sun Oct  3 18:00:30 2021

  Random mode : 2
  Random      : Finding in a range
  Use range   : 256 (bit)
  Rotor       : Random generate hex in range 256
  Rotor CPU   : 6 cores constant random generation hashes in 256 (bit) range
  Site        : https://github.com/phrutis/LostCoins
  Donate      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9

  [00:00:48] [CPU+GPU: 24,76 Mk/s] [GPU: 0,00 Mk/s] [T: 1,105,416,192] [F: 0]
  ```
 ## Mode 3
 ### Random search privat key (part+ -n values +par2 + -n value)
 - Run GPU: ```LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 3 -s 0123456789abcdef -n 10 -z fedcba9876543210 -m 5 -d 2```
 - Examples others combinations:
 - Run GPU: ```LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 3 -n 10 -z fedcba9876543210 -m 5 -d 0```
 - Run GPU: ```LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 3 -s 0123456789abcdef -z fedcba9876543210 -m 9 -d 0``` 
 - Run GPU: ```LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 3 -s 0123456789abcdeffedcba9876543210 -m 20 -d 0```
 
 ```
C:\Users\user>LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 3 -s 0123456789abcdef -n 10 -z fedcba9876543210 -m 5 -d 2

 LostCoins v4.4 (03.10.2021)

 SEARCH MODE  : COMPRESSED
 DEVICE       : GPU
 CPU THREAD   : 0
 GPU IDS      : 0
 GPU GRIDSIZE : 256x256
 RANDOM MODE  : 3
 CHARACTERS   : 10
 PASSPHRASE   : 0123456789abcdef
 PASSPHRASE 2 : fedcba9876543210
 DISPLAY MODE : 2
 TEXT COLOR   : 15
 HASH160 FILE : test.bin
 OUTPUT FILE  : Found.txt

 Loading      : 100 %
 Loaded       : 75,471 address

Bloom at 000001796690C240
  Version     : 2.1
  Entries     : 150942
  Error       : 0,0000010000
  Bits        : 4340363
  Bits/Elem   : 28,755175
  Bytes       : 542546 (0 MB)
  Hash funcs  : 20

  Start Time  : Sun Oct  3 18:04:34 2021

  Random mode : 3
  Random      : Part+value+part2+value
  Part        : 0123456789abcdef
  Value       : 10 x (0-f)
  Part 2      : fedcba9876543210
  Value 2     : 5 x (0-f)
  Example     : 0123456789abcdef[<<10>>]fedcba9876543210[<<5>>]
  Site        : https://github.com/phrutis/LostCoins
  Donate      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9

  GPU         : GPU #0 NVIDIA GeForce RTX 2070 (36x64 cores) Grid(256x256)

  [00:00:39] [CPU+GPU: 394,94 Mk/s] [GPU: 394,94 Mk/s] [T: 17,314,086,912] [F: 0]
 ```
 ### Random search privat key (part+ -n values +par2 + -n value)
  - Run CPU: ```LostCoins.exe -t 6 -f test.bin -r 3 -s 0123456789abcdef -n 10 -z fedcba9876543210 -m 5 -d 0```
 ```
C:\Users\user>LostCoins.exe -t 6 -f test.bin -r 3 -s 0123456789abcdef -n 10 -z fedcba9876543210 -m 5 -d 0

 LostCoins v4.4 (03.10.2021)

 SEARCH MODE  : COMPRESSED
 DEVICE       : CPU
 CPU THREAD   : 6
 GPU IDS      : 0
 GPU GRIDSIZE : -1x128
 RANDOM MODE  : 3
 CHARACTERS   : 10
 PASSPHRASE   : 0123456789abcdef
 PASSPHRASE 2 : fedcba9876543210
 DISPLAY MODE : 0
 TEXT COLOR   : 15
 HASH160 FILE : test.bin
 OUTPUT FILE  : Found.txt

 Loading      : 100 %
 Loaded       : 75,471 address

Bloom at 000002395D98B670
  Version     : 2.1
  Entries     : 150942
  Error       : 0,0000010000
  Bits        : 4340363
  Bits/Elem   : 28,755175
  Bytes       : 542546 (0 MB)
  Hash funcs  : 20

  Start Time  : Sun Oct  3 18:06:29 2021

  Random mode : 3
  Random      : Part+value+part2+value
  Part        : 0123456789abcdef
  Value       : 10 x (0-f)
  Part 2      : fedcba9876543210
  Value 2     : 5 x (0-f)
  Example     : 0123456789abcdef[<<10>>]fedcba9876543210[<<5>>]
  Site        : https://github.com/phrutis/LostCoins
  Donate      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9

 [0123456789abcdef5c45388eb5fedcba9876543210509d7]  [00:00:18] [CPU+GPU: 19,30 Mk/s] [GPU: 0,00 Mk/s] [T: 359,233,536] [F: 0]
 ```
  ## Mode 4 (BEST)
  ### Exact random search between specified ranges
 - Run GPU ```LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 4 -s 252 -z 254 -m 200```
 - Run CPU ```LostCoins.exe -t 6 -f test.bin -r 4 -s 252 -z 256```
 - -s 252 -z 256 (252,253,254,255,256)
  ```
  C:\Users\user>LostCoins.exe -t 0 -g -i 0 -x 256,256 -f test.bin -r 4 -s 252 -z 254 -m 200

 LostCoins v4.4 (03.10.2021)

 SEARCH MODE  : COMPRESSED
 DEVICE       : GPU
 CPU THREAD   : 0
 GPU IDS      : 0
 GPU GRIDSIZE : 256x256
 RANDOM MODE  : 4
 
