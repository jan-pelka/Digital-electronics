# ![alt text](https://github.com/jan-pelka/Digital-electronics "Logo Title Text 1")

## 03-Vivado

### Task 01


| | **Name of pin for** | |
| :-: | :-: | :-: |
| **Num** | **Switch** |  **LED**  |
| 0 | J15 | H17 |
| 1 | L16 | K15 |
| 2 | M13 | J13 |
| 3 | R15 | N14 |
| 4 | R17 | R18 |
| 5 | T18 | V17 |
| 6 | U18 | U17 |
| 7 | R13 | U16 |
| 8 | T8 | V16 |
| 9 | U8 | T15 |
| 10 | R16 | U14 |
| 11 | T13 | T16 |
| 12 | H6 | V15 |
| 13 | U12 | V14 |
| 14 | U11 | V12 |
| 15 | V10 | V11 |

### Task 02

Architecture:
```VHDL

    architecture Behavioral of mux_2bit_4to1 is
    begin
        f_o     <=  a_i when (sel_i = "00") else
                b_i when (sel_i = "01") else
                c_i when (sel_i = "10") else
                d_i;
    end Behavioral;

```


stimulus proces:

```VHDL
    p_stimulus : process
    begin
        report "stimulus proces started" severity note;
        
        s_a <= "00"; s_b <= "00"; s_c <= "00"; s_d <= "00";
        s_sel <= "00"; 
        wait for 100 ns;
        
        s_a <= "00"; s_b <= "01"; s_c <= "01"; s_d <= "10";
        s_sel <= "00"; 
        wait for 100 ns;
        
        s_a <= "11"; s_b <= "01"; s_c <= "01"; s_d <= "10";
        s_sel <= "00"; 
        wait for 100 ns;
        
        s_a <= "00"; s_b <= "01"; s_c <= "01"; s_d <= "10";
        s_sel <= "01"; 
        wait for 100 ns;
        
        s_a <= "00"; s_b <= "11"; s_c <= "01"; s_d <= "10";
        s_sel <= "01"; 
        wait for 100 ns;
        
        s_sel <= "10"; wait for 100 ns;
        
        s_sel <= "11"; wait for 100 ns;
        
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
```
Ukazka:

![alt text](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/03-vivado/TASK2.png "Logo Title Text 1")



### Task 03
TUTORIAL:
![naleznete ZDE](https://github.com/jan-pelka/Digital-electronics/blob/main/Labs/03-vivado/TUTORIAL/DE1%20CV3%20TUTORIAL.pdf "Logo Title Text 1")
