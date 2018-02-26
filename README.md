# keepass_profile
Profile for generating easy to type password in keepass.

# Solution
Use custom password generator e.g. `zvcv cvcv cvcv cvcv cvcv cvcv cvcv cvcv.` in keepass.  
```python
# python3
import math

print('len strength(10) strength(2) pattern')
for i in range(1,11):
    pattern = ''
    pattern += 'zvcv'
    for j in range(i-1):
        pattern += ' cvcv'
    pattern += '.'
    cvcv = (26 - 5) * 5 * (26 - 5) * 5
    print('%dx%s 10^%5.2f 2^%6.2f  %s'%(
        i,
        ' ' if i < 10 else '',
        # / 2 for brute-force success probablity.
        math.floor(math.log(cvcv ** i / 2, 10)*100)/100,
        math.floor(math.log(cvcv ** i / 2, 2)*100)/100,
        pattern
        )
    )
```
Output:
```
len strength(10) strength(2) pattern
1x  10^ 3.74 2^ 12.42  zvcv.
2x  10^ 7.78 2^ 25.85  zvcv cvcv.
3x  10^11.82 2^ 39.28  zvcv cvcv cvcv.
4x  10^15.86 2^ 52.71  zvcv cvcv cvcv cvcv.
5x  10^19.91 2^ 66.14  zvcv cvcv cvcv cvcv cvcv.
6x  10^23.95 2^ 79.57  zvcv cvcv cvcv cvcv cvcv cvcv.
7x  10^27.99 2^ 92.99  zvcv cvcv cvcv cvcv cvcv cvcv cvcv.
8x  10^32.03 2^106.42  zvcv cvcv cvcv cvcv cvcv cvcv cvcv cvcv.
9x  10^36.08 2^119.85  zvcv cvcv cvcv cvcv cvcv cvcv cvcv cvcv cvcv.
10x 10^40.12 2^133.28  zvcv cvcv cvcv cvcv cvcv cvcv cvcv cvcv cvcv cvcv.
```
`z`: `BCDFGHJKLMNPQRSTVWXYZ` Upper-Case Consonant. See [keepass.info](http://keepass.info/help/base/pwgenerator.html#charset).  
Typing an uppercase should be avoid. Yet some sites force our password to contain uppercase. So use uppercase at beginning of a password, like a sentance.  
`v`: `aeiou` Lower-Case Vowel.  
`c`: `bcdfghjklmnpqrstvwxyz` Lower-Case Consonant.  
  
- For general use (10^23.18): 6 words     
`>=` `6x  10^23.95 2^ 79.57`  
- For top secret (10^31.46):  8 words   
`>=` `8x  10^32.03 2^106.42`  
   

`8x  10^ 32.04 2^106.43` can be the title of your keepass password generation profile also.  
[How to set new profile as default?](https://superuser.com/questions/379823/can-i-change-the-default-password-profile-in-keepass)

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

# Principle
## 1. Strong enough.
- Minimal strength (not recommanded):
A usual 8 characters password, not benifit from keepass password generator.  
    * [10^15.83](https://math.stackexchange.com/questions/739874/how-many-possible-combinations-in-8-character-password) `=log((26+26+10+33)^8)` You can select and calculate in Google.  
All possible combinations for 8 characters password (A-z 0-9 and special characters).

- For general use:  
    * [10^19.27](https://en.wikipedia.org/wiki/S/KEY) `=log(2^64)`
        > Internally, S/KEY uses 64-bit numbers. For human usability purposes.

    * [10^23.18](https://en.wikipedia.org/wiki/Diceware) `=log(2^77)`
        > Originally, in 1995, Diceware creator Arnold Reinhold considered five words (64 bits) the minimal length needed by average users. However, starting in 2014, Reinhold recommends that at least six words (77 bits) should be used.

- For top secret:  

    - [10^21.12](https://gist.github.com/epixoip/a83d38f412b4737e99bbef804a270c40) `=log(414.4*10^9*60*60*24*365*100)`  
Hashes done by one Brutalis (8x Nvidia GTX 1080) in 100 years.

    - 10^22.50 `=log(10*10^12*60*60*24*365*100)`
        > Assume your adversary is capable of one trillion guesses per second.  
    -- Snowden, 2015.


    - [10^24.09](https://www.wired.com/2015/04/snowden-sexy-margaret-thatcher-password-isnt-so-sexy/) `=log(2^80)`
        > Bonneau estimates that a passphrase needs at least 70 or 80 bits of entropy to be considered secure.

    - [10^26.09](https://www.quora.com/How-fast-could-the-worlds-fastest-supercomputer-brute-force-crack-a-password) `=log(38360000000000000*60*60*24*365*100)`
        > I believe the fastest supercomputer can do 38,360,000,000,000,000 keys per second right now. (2013)

    - [10^26.47](https://en.wikipedia.org/wiki/TOP500) `=log(93*10^15*60*60*24*365*100)`  
FLOPS of supercomputer Sunway (world top 1, 2016) in 100 years. 93 petaflops. Note: KB MB GB TB PB  

    - 10^30.05 `=log(18036.65*10^9/21169*414.4*10^9*60*60*24*365*100)`  
Hashes done in 100 years by Brutalis, purchased by a whole year GDP of US. GDP in the United States was worth [18036.65 billion](http://www.tradingeconomics.com/united-states/gdp) US dollars in 2015. Brutalis base configuration price: [21,169.00 USD](https://sagitta.pw/hardware/gpu-compute-nodes/brutalis/).

    - 10^31.46 `=log(18036.65*10^9/500*8*31642*10^6*60*60*24*365*100)`  
MIPS in 100 years by AMD 1800x, purchased by a whole year GDP of US. 1800x MIPS: [31642](https://arstechnica.com/gadgets/2017/03/amd-ryzen-review/3/); core: 8; price: $500.

    - [10^38.54](https://en.wikipedia.org/wiki/Password_strength) `=log(2^128)`
        > Their answers vary between 29 bits of entropy needed if only online attacks are expected, and up to 128 bits of entropy needed for important cryptographic keys...

    - [10^38.54](https://en.wikipedia.org/wiki/Key_size) `=log(2^128)`
        > The large number of operations (2128) required to try all possible 128-bit keys is widely considered out of reach for conventional digital computing techniques for the foreseeable future.  
-- How secure is AES against brute force attacks?

## 2. Easy to type.  
You can't paste passwords on some websites, neither on linux terminal. So password shoud be pronounceable and easy to type.  
Yes: `fo`  
No: `ff` `oo` `&(*&%$` `AaAaAa`  

# Credit
[Diceware](https://en.wikipedia.org/wiki/Diceware) and [MasterPassword](https://github.com/Lyndir/MasterPassword/).
