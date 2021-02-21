# Digital-electronics

## 02-Gates

### Pravdivostní tabulka

máme dvoubitový vstup B a dvoubitový vstup A
v následující tabulce porovnáváme operace s těmito vstupy
například kdy je B < A 

| **Dec. equivalent** | **B[1:0]** | **A[1:0]** | **B is greater than A** | **B equals A** | **B is less than A** |
| :-: | :-: | :-: | :-: | :-: | :-: |
|  0  | 0 0 | 0 0 | 0 | 1 | 0 |
|  1  | 0 0 | 0 1 | 0 | 0 | 1 |
|  2  | 0 0 | 1 0 | 0 | 0 | 1 |
|  3  | 0 0 | 1 1 | 0 | 0 | 1 |
|  4  | 0 1 | 0 0 | 1 | 0 | 0 |
|  5  | 0 1 | 0 1 | 0 | 1 | 0 |
|  6  | 0 1 | 1 0 | 0 | 0 | 1 |
|  7  | 0 1 | 1 1 | 0 | 0 | 1 |
|  8  | 1 0 | 0 0 | 1 | 0 | 0 |
|  9  | 1 0 | 0 1 | 1 | 0 | 0 |
| 10  | 1 0 | 1 0 | 0 | 1 | 0 |
| 11  | 1 0 | 1 1 | 0 | 0 | 1 |
| 12  | 1 1 | 0 0 | 1 | 0 | 0 |
| 13  | 1 1 | 0 1 | 1 | 0 | 0 |
| 14  | 1 1 | 1 0 | 1 | 0 | 0 |
| 15  | 1 1 | 1 1 | 0 | 1 | 0 |

### Karnaughova mapa

z přechozího úkolu vytvoříme pro všechny 3 vástupní sloupce
Karnaughovy mapy

pro funkci  B > A

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/02-logic/img/mapa1.jpg "Logo Title Text 1")

pro funkci  B = A

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/02-logic/img/mapa2.jpg "Logo Title Text 1")

pro funkci  B < A

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/02-logic/img/mapa3.jpg "Logo Title Text 1")

u těchto map můžeme napsat jejich logickou funkci a to Buďto
SoP a nebo PoS
- kde SoP značí součet součinů (součin součtů)
- a PoS značí součin součtů (součtový součin)

například můžeme uvést zjednodušený SoP ze sloupce B > A

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/02-logic/img/RCE1.jpg "Logo Title Text 1")

a nebo zjednodušený PoS ze sloupce B < A

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/02-logic/img/RCE21.jpg "Logo Title Text 1")

dále problematiku simulujeme na EDA Playgroud kde můžeme projekt
nalézt na [ZDE](https://edaplayground.com/x/EFDv)


### 4 Bitový Vstup

v předchozí úloze jsme pracovaly s 2 bitovým vstupem ale můžeme
také vstup rozšířit na 4 bity

4 bitové zpracování jsme zpracovaly takto:

toto je výpis z EDAPlayGround Design.sv:

```VHDL
library ieee;
use ieee.std_logic_1164.all;

entity comparator_2bit is
    port(
        a_i           : in  std_logic_vector(4 - 1 downto 0);
        b_i           : in  std_logic_vector(4 - 1 downto 0);
        B_greater_A_o : out std_logic;
        B_equals_A_o  : out std_logic;
        B_less_A_o    : out std_logic       -- B is less than A
    );
end entity comparator_2bit;

architecture Behavioral of comparator_2bit is
begin
    B_greater_A_o <= '1' when (b_i > a_i) else '0';
    B_equals_A_o <= '1' when (b_i = a_i) else '0';
    B_less_A_o   <= '1' when (b_i < a_i) else '0';

end architecture Behavioral;
```

výpis z testbench.vhd:
```VHDL
library ieee;
use ieee.std_logic_1164.all;

entity tb_comparator_2bit is
    -- Entity of testbench is always empty
end entity tb_comparator_2bit;

architecture testbench of tb_comparator_2bit is

    -- Local signals
    signal s_a       : std_logic_vector(4 - 1 downto 0);
    signal s_b       : std_logic_vector(4 - 1 downto 0);
    signal s_B_greater_A : std_logic;
    signal s_B_equals_A  : std_logic;
    signal s_B_less_A    : std_logic;

begin
    -- Connecting testbench signals with comparator_2bit entity (Unit Under Test)
    uut_comparator_2bit : entity work.comparator_2bit
        port map(
            a_i           => s_a,
            b_i           => s_b,
            B_greater_A_o => s_B_greater_A,
            B_equals_A_o  => s_B_equals_A,
            B_less_A_o    => s_B_less_A
        );
  
  
    p_stimulus : process
    begin

-- SEQUENCE IMPUTS

        report "Stimulus process started" severity note;
        s_b <= "0000"; s_a <= "0000"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        report "Test failed for input combination: 0000, 0000" severity error;

        s_b <= "0000"; s_a <= "0001"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 0001" severity error;

        s_b <= "0000"; s_a <= "0010"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 0010" severity error;

        s_b <= "0000"; s_a <= "0011"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 0011" severity error;

        s_b <= "0000"; s_a <= "0100"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 0100" severity error;

        s_b <= "0000"; s_a <= "0101"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 0101" severity error;

        s_b <= "0000"; s_a <= "0110"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 0110" severity error;

        s_b <= "0000"; s_a <= "0111"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 0111" severity error;

        s_b <= "0000"; s_a <= "1000"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 1000" severity error;

        s_b <= "0000"; s_a <= "1001"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 1001" severity error;

        s_b <= "0000"; s_a <= "1010"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 1010" severity error;

        s_b <= "0000"; s_a <= "1011"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 1011" severity error;

        s_b <= "0000"; s_a <= "1100"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 1011" severity error;

        s_b <= "0000"; s_a <= "1101"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 1011" severity error;

        s_b <= "0000"; s_a <= "1110"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 1011" severity error;

        s_b <= "0000"; s_a <= "1111"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 1011" severity error;

-- RANDOM IMPUTS

        s_b <= "0101"; s_a <= "1110"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 1011" severity error;

        s_b <= "1110"; s_a <= "0100"; wait for 100 ns;
        assert ((s_B_greater_A = '1') and (s_B_equals_A = '0') and (s_B_less_A = '0'))
        report "Test failed for input combination: 0000, 1011" severity error;

        s_b <= "0010"; s_a <= "1111"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 0000, 1011" severity error;

        s_b <= "1101"; s_a <= "1101"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        report "Test failed for input combination: 0000, 1011" severity error;

--  ERROR OUTPUTS

        s_b <= "1111"; s_a <= "1111"; wait for 100 ns;
        assert ((s_B_greater_A = '1') and (s_B_equals_A = '1') and (s_B_less_A = '1'))
        report "Test failed for input combination: 1111, 1111" severity error;

        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
end architecture testbench;
```

výpis z logu:

```
[2021-02-21 07:07:17 EST] ghdl -i design.vhd testbench.vhd  && ghdl -m  tb_comparator_2bit && ghdl -r  tb_comparator_2bit   --vcd=dump.vcd && sed -i 's/^U/X/g; s/^-/X/g; s/^H/1/g; s/^L/0/g' dump.vcd 
analyze design.vhd
analyze testbench.vhd
elaborate tb_comparator_2bit
testbench.vhd:34:9:@0ms:(report note): Stimulus process started
testbench.vhd:120:9:@2100ns:(assertion error): Test failed for input combination: 1111, 1111
testbench.vhd:124:9:@2100ns:(report note): Stimulus process finished
Finding VCD file...
./dump.vcd
[2021-02-21 07:07:18 EST] Opening EPWave...
Done
```

odkaz na Playground naleznete [ZDE](https://edaplayground.com/x/JYZ8)
