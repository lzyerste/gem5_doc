**MC**: memory cell, the basic 1-bit store unit

**WL**: wordline, horizontal as a row

> **DWL**: divided wordline
>
> **GWL**: global wordline
>
> **LWL**: local wordline
>
> **HWD**: hierarchical word decoding
>
> **PWD**: pulsed wordline

**BL**: bitline, vertical as a column

**SA**: sense amplifier

------

**Predecoding**: to decrease the fan-in of gates. For example, a 8-256 decoder could be designed in one level, using 256 AND gates, each gate has 8 inputs. Predecoding could first partition decoder into two parts, each is a 4-16 decoder, and then use 256 2-input AND gates to generate the result. Predecoding could be used for selecting the wordline (or row decoder).

**Non-Partitioned** decode hierarchy: the selected entire row (WL) is activated, but one wordline has many memory cells (columns), only a small fraction of these columns are actually need and much power is squandered. This kind of decoding is suitable for small SRAM caches such as L1.

**Divided Wordline (DWL)** mechanism divides the memory array into Nb blocks (vertically, so each wordline is also divided into multiple parts). The top level wordline is so called global wordline (GWL), and the divided small part of the line is called local wordline (LWL). The global row decoder keeps unchanged, nonetheless, we need a way to select the LWL (local row decoder). These bits of course come from the original column bits. After two-level row decoding, only one LWL is activated instead of the entire wordline (GWL). One LWL has (Nc / Nb) columns (Nc is the number of total columns). The LWL could contain multiple cache blocks. The left column bits are used to select the cache block.

**Hierarchical Word Decoding (HWD)** is an extension to DWL, adding another level of decoding hierarchy (Global WL -> Block Group -> Local WL), which is efficient for large size cache.