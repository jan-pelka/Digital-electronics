CODE VELOCITY:

```vhdl
library ieee;
use IEEE.math_real.all;                 -- Needed for power
use ieee.std_logic_1164.all;            -- Basic library
use ieee.numeric_std.all;               -- Needed for shifts



entity velocity is
    Port (
        clk1hz_i           : in std_logic;
        velocity_o         : out STD_logic_vector(10-1 downto 0)  := "0000000000";
        sensor_i           : in std_logic
    );
end velocity;
 
architecture behave of velocity is

begin
 
p_velocity : process(clk1hz_i)

  variable counter          : integer    := 0; 
  variable var1             : integer    := 0; 
  variable var2             : STD_logic_vector(10-1 downto 0);
                                                
    begin
    
    if rising_edge(sensor_i) then
        counter := counter + 1; 					-- if sensor detect magnet couter count it


    end if;

    if rising_edge(clk1hz_i) then 
        var1 := (counter*36)/5; 					-- calculating speed
        var2 := std_logic_vector(to_unsigned(var1, var2'length)); 	-- geting right data type
        velocity_o <= var2; 						-- instert data to output variable
        counter := 0; 							-- reseting counter
    end if;
  end process p_velocity;
end architecture behave;


```


TB:

```vhdl
library ieee;
use ieee.std_logic_1164.all;

entity tb_distance is
end entity tb_distance;

architecture testbench of tb_distance is

    signal s_sensor     :  std_logic;
    signal s_clk1hz     :  std_logic;
    signal s_velocity   :  std_logic_vector(10-1 downto 0);
    signal s_var5       : integer;
    signal s_counter    : integer;
    
    
begin
    uut_velocity: entity work.velocity
        port map (
            
        clk1hz_i => s_clk1hz,  
        velocity_o => s_velocity,
        sensor_i => s_sensor,
        var5_o => s_var5,
        counter_o => s_counter
        );
        
    gen_clock : process
    begin
        s_clk1hz <= '1';
        wait for 500ms;
        s_clk1hz <= '0';
        wait for 500ms;
        s_clk1hz <= '1';
        wait for 500ms;
        s_clk1hz <= '0';
        wait for 500ms;
        s_clk1hz <= '1';
        wait for 500ms;
        s_clk1hz <= '0';
        wait for 500ms;
        s_clk1hz <= '1';
        wait for 500ms;
        s_clk1hz <= '0';
        wait for 500ms;
        wait;
    end process gen_clock;

    p_stimulus : process
    begin
        s_sensor <= '1';
        wait for 500ms;
        s_sensor <= '0';
        wait for 500ms;
        
        s_sensor <= '1';
        wait for 250ms;
        s_sensor <= '0';
        wait for 250ms;
        s_sensor <= '1';
        wait for 250ms;
        s_sensor <= '0';
        wait for 250ms;
        s_sensor <= '1';
        wait for 250ms;
        s_sensor <= '0';
        wait for 250ms;
        s_sensor <= '1';
        wait for 250ms;
        s_sensor <= '0';
        wait for 250ms;

        s_sensor <= '1';
        wait for 100ms;
        s_sensor <= '0';
        wait for 100ms;
        s_sensor <= '1';
        wait for 100ms;
        s_sensor <= '0';
        wait for 100ms;
        s_sensor <= '1';
        wait for 100ms;
        s_sensor <= '0';
        wait for 100ms;
        s_sensor <= '1';
        wait for 100ms;
        s_sensor <= '0';
        wait for 100ms;
        s_sensor <= '1';
        wait for 100ms;
        s_sensor <= '0';
        wait for 100ms;
        
        wait;
    end process p_stimulus;
end architecture testbench;
```

===> sim.jpg
