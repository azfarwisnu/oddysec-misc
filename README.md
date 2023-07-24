Misc
===============

Apollo Apate
---------------
desc:
One always tell the truth, One prevent you to see the truth. 
Address: 0xEaf385874A62AF5863a6db959b09904C8299bc66 
Provider:  
https://eth-sepolia.g.alchemy.com/v2/SMfUKiFXRNaIsjRSccFuYCq8Q3QJgks

Dari desc yang diberikan author mencari smartcontract yang ada yaitu dengan menggunakan testnet sepolia yang berjalan pada eth, lalu didapatkan smartcontract nya
https://sepolia.etherscan.io/address/0xeaf385874a62af5863a6db959b09904c8299bc66

terdapat satu transaksi pada address tersebut https://sepolia.etherscan.io/tx/0x954829a0c1cab01dca36f350ca4a14d5b94cbeb6d6dd05ebb6307f02a94322cd dapat dilihat dari data yang ada pada transaksi.
<img src="https://cdn.discordapp.com/attachments/1101531709670969364/1132852032869515284/image.png" />

Bisa dilihat function firstTruth() -> digunakan untuk mendapatkan flag pertama, lalu terdapat abi nya yang dapat kita pakai, dan pada challanges juga diberikan wordlist yang ada.
lalu pada data transaksi juga terdapat smarcontract baru yang memungkinkan untuk mendapat flag part 2? = 0x011fF1177f13eEeABc358bCee2eEb1a2C520f06b

sebelum itu coba memanggil function pertama, disini saya menggunakan react js (dengan memakai code :u develop web ketika saya menggunakan solidity untuk backend saya). sebelum itu pastikan rpc, abi, chain diset agar terhubung ke jaringan testnet sepolia.
```python
handleFetching = async (signer) => {
    const getMessage = new ethers.Contract(contractAddress, CoreABI, signer);
    this.props.setContract(getMessage);

    
    let message = await getMessage.firstTruth();
    console.log(message)
    let blockedList = await getMessage.GetBlockList();
```
maka akan mereturn hasil flag{7h3_0nly_4nswer

lalu selanjutnya mencoba melihat data pada smartcontract ke dua, pada transksi berikut https://sepolia.etherscan.io/tx/0x3a893233c6fcd7b345ef6c51092be35063a921e0a2c214816fe816dad186c6c5
ada value nilai yang dimasukan pada function seekFlag(string) = kemungkinan menggunakan nilai dari wordlist yang ada, tinggal di brute dengan wordlist yang ada.

<img src="https://media.discordapp.net/attachments/1131976847140335700/1132001320937738300/image.png" />

lalu didaptkan smartcontract berikutnya kemudian author check kembali, pada transaksi berikut
https://sepolia.etherscan.io/tx/0xd9079f0a308a3d312f7ebbfddcf3281b6e821cceff1b1711efae87a9b03df313

dapat dilihat terdapat klue untuk mendapatkan part flag terakhir.
<img src="https://cdn.discordapp.com/attachments/1101531709670969364/1132856427283763310/image.png" />
part1, part2 = sudah didapat tinggal mencari 3 key untuk mendapatkan flag. berdasarkan history transaksi yang ada https://sepolia.etherscan.io/tx/0x8e7747e24111d8a744eacc5c598bfed315f374ae1f0b4a59f2ee7f0db040c681

'history is changing' = mungkin adalah 3 key yang digunakan. lalu saya mencoba menggabungkan part1+part2+part3+part4+part5 namun gagal mendapatkan flagnya. saya berfikir digabungkan karena berdasarkan abi yang didapat pada trasansksi

```
[
    {
        "inputs": [
            {
                "internalType": "string",
                "name": "str1",
                "type": "string"
            }
        ],
        "name": "finalTruth",
        "outputs": [
            {
                "internalType": "string",
                "name": "",
                "type": "string"
            }
        ],
        "stateMutability": "pure",
        "type": "function"
    }
    {
        "inputs": [],
        "name": "help",
        "outputs": [
            {
                "internalType": "string",
                "name": "",
                "type": "string"
            }
        ],
        "stateMutability": "pure",
        "type": "function"
    }
    {
        "inputs": [],
        "name": "mesg",
        "outputs": [
            {
                "internalType": "string",
                "name": "",
                "type": "string"
            }
        ],
        "stateMutability": "view",
        "type": "function"
    }
    {
        "inputs": [],
        "name": "trace",
        "outputs": [
            {
                "internalType": "string",
                "name": "",
                "type": "string"
            }
        ],
        "stateMutability": "pure",
        "type": "function"
    }
]

```

finalTruth hanya menerima satu input pada abi, akhirnya saya mencoba memvalidasi kembali dengan mendecompile program dengan menggunakan ethervm 
https://ethervm.io/decompile/sepolia/0xf29A4420898788C6cF89978CCEA5Cc224fBF575c

pada nilai ini dapat dilihat memasukan 5 nilai function finalTruth
<img src="https://cdn.discordapp.com/attachments/1101531709670969364/1132858520300179587/image.png" />

lalu tinggal call function nya untuk mendapatkan flag terakhir jangan lupa abi nya di custom untuk memasukan 5 nilai pada function.

```python
handleFetching = async (signer) => {
const getMessage = new ethers.Contract(contractAddress, CoreABI, signer);
this.props.setContract(getMessage);

let message = await getMessage.finalTruth("flag{7h3_0nly_4nswer","_1s_g0_b4ck_","history","is","changing");
console.log(message)
let blockedList = await getMessage.GetBlockList();
```

<img src="https://media.discordapp.net/attachments/1131976847140335700/1132019725501730949/image.png?width=943&height=219" />




Mix Match Push!
---------------
Desc:
Welcome Challenger!

The way Gods communicate is unique, so is this challenge, can you break their code? They use an ancient method of communication called “Blockchain”:
Address: 0x97891c560284eAf12175d950bf65Dba071e6a06F
Provider: https://eth-sepolia.g.alchemy.com/v2/SMfUKiFXRNaIsjRSccFuYCq8Q3QJgks8


sama seperti challange berikut nya chalange ini menggunakan jaringan testnet sepolia pada eth pertama author set dulu rpc dan smartcontract nya.
hanya terdapat dua transaksi yang mana bisa dilihat didata nya 
https://sepolia.etherscan.io/tx/0x874929734a74b10cf8b62c3a9e88eefd65dafb6cd9a3ba56413c442ce18bbf14

hanya terdapat dua function, yaitu getflag => untuk dapat flag, lalu getMapping untuk cara mapping atau encrypted flagnya. encrypted flag sendiri juga sudah muncul pada history transaksi yang ada.

```js
handleFetching = async (signer) => {
const getMessage = new ethers.Contract(contractAddress, CoreABI, signer);
this.props.setContract(getMessage);

let message = await getMessage.getMapping();
console.log(message)
let blockedList = await getMessage.GetBlockList();
```

lalu akan keluar mapping atau encrypt pola pada flag
```
Lowercase Mapping:
 a is y
 b is m
 c is q
 d is w
 e is z
 f is p
 g is x
 h is s
 i is r
 j is t
 k is l
 l is e
 m is f
 n is b
 o is c
 p is n
 q is j
 r is k
 s is v
 t is g
 u is i
 v is d
 w is h
 x is u
 y is a
 z is o
Uppercase Mapping:
 A is X
 B is P
 C is Z
 D is Q
 E is R
 F is C
 G is A
 H is M
 I is S
 J is O
 K is L
 L is U
 M is N
 N is T
 O is J
 P is W
 Q is B
 R is V
 S is D
 T is F
 U is Y
 V is K
 W is I
 X is H
 Y is G
 Z is E
Special Character Mapping:
 ! is @
 " is #
 # is $
 $ is %
 % is ^
 & is *
 ' is !
 ( is )
 ) is [
 * is ]
 + is :
 , is ?
 - is !
 . is ,
 / is ;
 : is _
 ; is +
 < is >
 = is (
 > is {
 ? is }
 @ is `
 [ is \
 ] is '
 ^ is ~
 _ is -
 ` is /
 { is .
 | is ~
 } is =
 ~ is ;
Number Mapping:
 0 is 9
 1 is 7
 2 is 4
 3 is 2
 4 is 6
 5 is 0
 6 is 3
 7 is 5
 8 is 1
 9 is 8
```

langsung saja buat solver nya untuk mendapatkan flag.
```python
data = {"a":"y",
"b":"m",
"c":"q",
"d":"w",
"e":"z",
"f":"p",
"g":"x",
"h":"s",
"i":"r",
"j":"t",
"k":"l",
"l":"e",
"m":"f",
"n":"b",
"o":"c",
"p":"n",
"q":"j",
"r":"k",
"s":"v",
"t":"g",
"u":"i",
"v":"d",
"w":"h",
"x":"u",
"y":"a",
"z":"o",
"A":"X",
"B":"P",
"C":"Z",
"D":"Q",
"E":"R",
"F":"C",
"G":"A",
"H":"M",
"I":"S",
"J":"O",
"K":"L",
"L":"U",
"M":"N",
"N":"T",
"O":"J",
"P":"W",
"Q":"B",
"R":"V",
"S":"D",
"T":"F",
"U":"Y",
"V":"K",
"W":"I",
"X":"H",
"Y":"G",
"Z":"E",
"!":"@",
'"':"#",
"#":"$",
"$":"%",
"%":"^",
"&":"*",
"'":"!",
"(":")",
")":"[",
"*":"]",
"+":":",
",":"?",
"-":"!",
".":",",
"/":";",
":":"_",
";":"+",
"<":">",
"=":"(",
">":"{",
"?":"}",
"@":"`",
"[":" ",
"]":"'",
"^":"~",
"_":"-",
"`":"/",
"{":".",
"|":"~",
"}":"=",
"~":";",
"0":"9",
"1":"7",
"2":"4",
"3":"2",
"4":"6",
"5":"0",
"6":"3",
"7":"5",
"8":"1",
"9":"8"
}

enc = "peyx.r5-70-y-D7fne2-ZVan59-6pg2k-6UU-mpw25="
flag = ""

for n in enc:
    for x in data:
        value = data[str(x)]
        if(n==value):
            print(x)
            print(n)
            print("ketemu")
            flag += str(x)

print(flag)
```

flag{i7_15_a_S1mpl3_CRyp70_4ft3r_4LL_bfd37}
