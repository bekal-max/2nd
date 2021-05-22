--ALU VHDL Code
Library ieee;
use ieee.std_logic_vector_1164.all;
use ieee.std_logic_unsigned.all;
Entity my_ALU is
Port (a,b : in std_logic_vector(7 downto 0);
      Sel : in std_logic_vector(3 downto 0);
      Cin : in std_logic
         y: out std_logic_vector(7 downto 0))
End my_ALU;
Architecture Dataflow of my_ALU is
  signal Arith,Logic:std_logic_vector(7 downto 0);
Begin
--Arithmetic Unit
With sel (2 downto 0) select
Arith <=a    when "000",
        a +1 when "001",
        a -1 when "010",
        b    when "011",
        b +1 when "100",
        b -1 when "101",
        a +b when "110",
        a +b + Cin when others ;
--Logical Unit 
With sel (2 downto 0) select
Logic<=not a when "000",
       not b when "001",
       a and b when "010",
       a or b when "011",
       a nand b when "100",
       a nor b when "101",
       a xor b when "110",
       not(a xor b) when others  ;
With sel (3) select
y<= Arith when "0",
    Logic when others;
End Dataflow;
