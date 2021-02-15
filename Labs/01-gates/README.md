# Digital-electronics

## 01-Gates

### Git-Hub

Odkaz na můj GitHub je [ZDE](https://github.com/jan-pelka)

a můj repozitář pro předmět BPC-DE1 naleznete [ZDE](https://github.com/jan-pelka/Digital-electronics)




### EDA Playground

#### 1

Máme problém

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/01-gates/img/rce%201.png "Logo Title Text 1")

který má tuto pravdivostní tabulku

| **a** | **b** |**c** | **f(c,b,a)** |
| :-: | :-: | :-: | :-: |
| 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 |

#### 2

a tuto rovnici můžeme řešit i za výhradné pomoci hradla NAND

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/01-gates/img/rce%202.png "Logo Title Text 1")

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/01-gates/img/NAND.jpg "Logo Title Text 1")

#### 3

výhradní hradlo NOR


![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/01-gates/img/rce%203.png "Logo Title Text 1")

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/01-gates/img/NOR.png "Logo Title Text 1")


#### 4

problém je řešen i za pomoci EDA Playground


Kód řešení:
```VHDL
library ieee;               -- Standard library
use ieee.std_logic_1164.all;-- Package for data types and logic operations

------------------------------------------------------------------------
-- Entity declaration for basic gates
------------------------------------------------------------------------
entity gates is
    port(
        a_i    : in  std_logic;         -- Data input
        b_i    : in  std_logic;         -- Data input
        c_i    : in  std_logic;
        fout_o    : out std_logic;         -- OR output function
        fnand_o   : out std_logic;
        fnor_o    : out std_logic
    );
end entity gates;

------------------------------------------------------------------------
-- Architecture body for basic gates
------------------------------------------------------------------------
architecture dataflow of gates is
begin

    fout_o  <=((not b_i)and a_i) or ((not c_i)and(not b_i));
    fnand_o <= ( a_i nand ( b_i nand b_i ) )   nand ( ( b_i nand b_i ) nand (c_i nand c_i) );
	fnor_o <= ((((a_i nor a_i) nor b_i) nor (b_i nor c_i))   nor  (((a_i nor a_i) nor b_i) nor (b_i nor c_i)));   
end architecture dataflow;
```

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/01-gates/img/Prubeh1.png)

řešení na Playground je [ZDE](https://edaplayground.com/x/Ud9_)





### Distribuční zákony

#### 1

máme ověřit zda platí distribuční zákony 
budeme je ověřovat za pomocí prostředí
EDA Playground 

===> kod (vložení)


===> průběhy (foto)

link na EDA Playground
===> link (foto)

