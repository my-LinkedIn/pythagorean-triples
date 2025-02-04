# PYTHAGOREAN TRIPLES


## Basic Implementation

```D
import std.stdio;
import std.range;
import std.algorithm;

alias Triples = int[][];

void main()
{
    const N = 20;

    Triples triples;

    foreach (a; 1..N+1)
        foreach (b; a+1..N+1)
            foreach (c; b+1..N+1)
                if (a^^2 + b^^2 == c^^2) triples ~= [a, b, c];

    triples.each!writeln;
}
```

## Basic Implementation but using Tuple

```D
import std.stdio;
import std.array;
import std.range;
import std.typecons;
import std.algorithm;

alias Triples = Tuple!(int, int, int)[]; 

void main()
{
    const N = 20;
    
    Triples triples;

    foreach (a; 1..N+1)
        foreach (b; a+1..N+1)
            foreach (c; b+1..N+1)
                if (a^^2 + b^^2 == c^^2) triples ~= tuple(a, b, c);
    
    triples.each!(triple => triple.array.writeln);
}
```

## Phobos (Standard library) Cartesian Product Implementation

```D
import std.stdio;
import std.array;
import std.range;
import std.algorithm;
import std.algorithm.iteration;
import std.typecons;

void main()
{
    const N = 20;
    
    auto ts = cartesianProduct(iota(1,N+1), iota(1,N+1), iota(1,N+1))
        .filter!(t => (t[0] < t[1]) && (t[0]^^2 + t[1]^^2 == t[2]^^2))
        .map!(t => tuple(t[0], t[1], t[2]));

    ts.map!array.each!writeln;
}
```
## More advanced Functional Programming Implementation


```D
import std.stdio;
import std.range;
import std.algorithm.iteration;

auto pythagoreanTriplet(int n) {
    return  iota(1, n+1).map!(x => 
              iota(x+1, n+1).map!(y => 
                  iota(y+1, n+1).filter!((z) => x * x + y * y == z * z).map!(z => [x, y, z])
              ).join
            ).join;
}

void main() {
    const LIMIT = 20;

    pythagoreanTriplet(LIMIT).each!writeln;
}
```

## BONUS: Special Pythagorean Triplet (Project Euler problem 9 solution)

You can find the Problem statement [here](https://projecteuler.net/problem=9).

```D
import std.stdio;
import std.range;

void main()
{
    foreach (a; iota(0, 333))
        foreach (b; iota(a + 1, 500))
            {
              auto c = 1000-(a+b);
              
              if (a*a + b*b == c*c) {
                  writeln(a, " * ", b, " * ", c, " = ", a * b * c);
                  return;
              }
            }
   
    writeln("No Triple found!");
}
```
