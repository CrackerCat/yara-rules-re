# YARA assembly language examples

## `tests.putchar` patch

YARA has no useful output routine that can be called from condition
bytecode. (At least I have not found any.) This
[patch](yara4-putchar.patch) adds a simple `tests.putchar` function
that wraps _putchar(3)_ to YARA 4.0.

All examples below require this patch.

## "Hello world"-like program

The program contained in [abcd.yac](abcd.yac) outputs the string
`ABCD` and a newline character. It is a more concise version of the
program generated by the following rule:
``` YARA
import "tests"
rule abcd {
  condition:
    tests.putchar(0x41) and tests.putchar(0x42) and
    tests.putchar(0x43) and tests.putchar(0x44) and
    tests.putchar(0x0a) and false
}
```

## Mandelbrot set renderer

[mandelbrot.yac](mandelbrot.yac) is a port of the Mandelbrot ASCII
rendering program written in obfuscated C that can be found at the top
of [Professor Ken Perlin's](https://mrl.nyu.edu/~perlin) homepage. (I
found it via [Rosetta
Code](http://rosettacode.org/wiki/Mandelbrot_set#ASCII).)

``` C
main(k){float i,j,r,x,y=-16;while(puts(""),y++<15)for(x
=0;x++<84;putchar(" .:-;!/>)|&IH%*#"[k&15]))for(i=k=r=0;
j=r*r-i*i-2+x/25,i=2*r*i+y/10,j*j+i*i<11&&k++<111;r=j);}
```
