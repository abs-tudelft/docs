# Writing interfaces

Tydi, as the spec explains, is language-agnostic. However, there are integrations available for various HDLs.

Below you can see an example of a streamlet with simple interface that only has a single output stream. The data-type is an RGB pixel value nested in a group that gives it an index. The meaning of this datatype does not matter, it is just to showcase the different syntaxes for different languages. Note that the VHDL example contains a compiled, non-rich output.

=== "Tydi-lang"

    ``` c
    type byte = Bit(8);

    Group RGB {
        r: byte;
        g: byte;
        b: byte;
    };

    Group MyGroup {
        index: Bit(64);
        value: RGB;
    };

    type RootStream = Stream(MyGroup, c=8, d=1, n=1, r=false, u=Null);

    streamlet SimpleStreamlet {
        output: RootStream out;
    };
    ```

=== "Chisel"

    ``` scala
    import nl.tudelft.tydi_chisel._
    import chisel3._

    class RGB extends Group {
        private val byte = Uint(8.W)

        val r = byte
        val g = byte
        val b = byte
    }

    class MyGroup extends Group {
        val index = BitsEl(64.W)
        val value = new RGB
    }

    class RootStream extends PhysicalStreamDetailed(e=new MyGroup, c=8, d=1, n=1, r=false, u=Null())

    class SimpleStreamlet extends TydiModule {
        private val outputStream = new RootStream
        val output: PhysicalStream = outputStream.toPhysical
    }
    ```

=== "Clash"

    ``` haskell
    type Byte = Unsigned 8

    type MyGroup = Group (
        r >:: Byte :&:
        g >:: Byte :&:
        b >:: Byte
    )

    type MyGroup = Group (
        index >:: Unsigned 64 :&:
        value >:: RGB
    )

    type RootStream = TydiSynth New (C 8) 1 1 () MyGroup

    SimpleStreamlet :: () -> RootStream
    ```

=== "VHDL"

    ``` vhdl
    library ieee;
    use ieee.std_logic_1164.all;

    package proj is

      component simple_interface_0_simple_streamlet_com is
        port (
          clk : in std_logic;
          rst : in std_logic;
          root_stream_out_valid : out std_logic;
          root_stream_out_ready : in std_logic;
          root_stream_out_data : out std_logic_vector(87 downto 0);
          root_stream_out_last : out std_logic_vector(0 downto 0);
          root_stream_out_strb : out std_logic_vector(0 downto 0)
        );
      end component simple_interface_0_simple_streamlet_com;

    end proj;
    ```