# keepass_profile
Profile for generating easy to type password in keepass.
# Principle
## 1. Strong enough.
You can select and calculate in Google.

- For general use:  
1. [10^16](https://math.stackexchange.com/questions/739874/how-many-possible-combinations-in-8-character-password) `=(26+26+10+33)^8`  
All possible combinations for 8 characters password (A-z 0-9 and special characters).

- For top secret:  
1. 10^22 `=10*10^12*60*60*24*365*100`
> Assume your adversary is capable of one trillion guesses per second. -- Snowden, 2015.

2. [10^24](https://www.wired.com/2015/04/snowden-sexy-margaret-thatcher-password-isnt-so-sexy/) `=2^80`
> Bonneau estimates that a passphrase needs at least 70 or 80 bits of entropy to be considered secure.

3. [10^39](https://en.wikipedia.org/wiki/Password_strength) `=2^128`
> Their answers vary between 29 bits of entropy needed if only online attacks are expected, and up to 128 bits of entropy needed for important cryptographic keys...

4. [10^26](https://www.quora.com/How-fast-could-the-worlds-fastest-supercomputer-brute-force-crack-a-password) `=38360000000000000*60*60*24*365*100`
> I believe the fastest supercomputer can do 38,360,000,000,000,000 keys per second right now. (2013)

5. [10^26](https://en.wikipedia.org/wiki/TOP500) `=93*10^15*60*60*24*365*100`  
FLOPS of supercomputer Sunway (world top 1, 2016) in 100 years. 93 petaflops. Note: KB MB GB TB PB  

6. [10^21](https://gist.github.com/epixoip/a83d38f412b4737e99bbef804a270c40) `=414.4*10^9*60*60*24*365*100`  
Hashes done by Brutalis (8x Nvidia GTX 1080) in 100 years.

7. 10^30 `=18036.65*10^9/21169*414.4*10^9*60*60*24*365*100`  
Hashes done in 100 years by Brutalis, purchased by a whole year GDP of US. GDP in the United States was worth [18036.65 billion](http://www.tradingeconomics.com/united-states/gdp) US dollars in 2015. Brutalis base configuration price: [21,169.00 USD](https://sagitta.pw/hardware/gpu-compute-nodes/brutalis/).

8. 10^31 `=18036.65*10^9/500*8*31642*10^6*60*60*24*365*100`  
MIPS in 100 years by AMD 1800x, purchased by a whole year GDP of US. 1800x MIPS: [31642](https://arstechnica.com/gadgets/2017/03/amd-ryzen-review/3/); core: 8; price: $500.

## 2. Easy to type.  
You can't paste passwords on some websites, neither on linux terminal. So password shoud be pronounceable and easy to type.  
Yes: `fo`  
No: `ff` `oo` `&(*&%$` `AaAaAa`  


# Solution
Use custom password generator `zvcv cvcv cvcv cvcv cvcv cvcv cvcv cvcv.` in keepass.  
`z`: `BCDFGHJKLMNPQRSTVWXYZ` Upper-Case Consonant. See [keepass.info](http://keepass.info/help/base/pwgenerator.html#charset).  
Typing an uppercase should be avoid. Yet some sites force our password to contain uppercase. So use uppercase at beginning of a password, like a sentance.  
`v`: `aeiou` Lower-Case Vowel.  
`c`: `bcdfghjklmnpqrstvwxyz` Lower-Case Consonant.  
```python
# python3
for i in range(8,1,-1):
    print('zvcv', end="")
    for j in range(i-1):
        print(' cvcv', end="")
    print('.')
```
Output:
```
zvcv cvcv cvcv cvcv cvcv cvcv cvcv cvcv.
zvcv cvcv cvcv cvcv cvcv cvcv cvcv.
zvcv cvcv cvcv cvcv cvcv cvcv.
zvcv cvcv cvcv cvcv cvcv.
zvcv cvcv cvcv cvcv.
zvcv cvcv cvcv.
zvcv cvcv.
```
# Example
```
# type: 8x
Nixi tiyo cote vuvi sani jabi leto juzu.
Letu yine yufu kiyi sula rixi xuge vuxi.
Xagi cira mefa kipu wiqa jodo vihu zipu.
Gewi feti coxo ceqe tida bedi wofa pixe.
Xeno lisi topo niqo buge koge xoja yada.
Yimi xoku debi besi beco nato reci suza.
Felu qabu biwa muru voni zijo cave mozu.
Bisu tegi yuye cowi dide hoxo buya pipe.
Wapi dofo boje qadu wele puvi zuza bune.
Levu voma coma varo nuti laxi putu zure.
Dova piwi nodi bubu jawa gumu mahu dewi.
```

# Strength
For type 8x: `=((26-5)*5*(26-5)*5)^8/2` Why `/2`? Brute-force a halfway and find out the password at average.
```python
# python3
from math import log
for i in range(8,1,-1):
    cvcv = (26 - 5) * 5 * (26 - 5) * 5
    print('%d %dx 10^%-2d 2^%-3d'%(9-i, i, int(log(cvcv ** i / 2, 10)), int(log(cvcv ** i / 2, 2))))
```
Output:
```
1 8x 10^32 2^106
2 7x 10^27 2^92 
3 6x 10^23 2^79 
4 5x 10^19 2^66 
5 4x 10^15 2^52 
6 3x 10^11 2^39 
7 2x 10^7  2^25 
```
For general use (10^16):  
`>=` `5 4x 10^15 2^52 ` i.e. `zvcv cvcv cvcv cvcv.`  
For top secret (10^31):  
`>=` `1 8x 10^32 2^106` i.e. `zvcv cvcv cvcv cvcv cvcv cvcv cvcv cvcv.`  
`1 8x 10^32 2^106` can also be the title of your keepass password generation profile.  
