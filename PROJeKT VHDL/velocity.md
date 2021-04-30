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
        sensor_i           : in std_logic;
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

