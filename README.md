# PYTHAGOREAN TRIPLES


## Basic Implementation

```D
import std.stdio;
import std.range;
import std.algorithm;

void main()
{
    const N = 20;

    alias Triples = int[][];
    Triples triples;

    foreach (a; 1..N+1)
        foreach (b; a..N+1)
            foreach (c; b..N+1)
                if (a^^2 + b^^2 == c^^2) triples ~= [a, b, c];

    triples.each!(triple => triple.writeln);
}
```

## Basic Implementation but using Tuple

```D
import std.stdio;
import std.array;
import std.range;
import std.typecons;
import std.algorithm;

void main()
{
    const N = 20;
    
    alias Triples = Tuple!(int, int, int)[]; 
    Triples triples;

    foreach (a; 1..N+1)
        foreach (b; a..N+1)
            foreach (c; b..N+1)
                if (a^^2 + b^^2 == c^^2) triples ~= tuple(a, b, c);
    
    triples.each!(triple => triple.array.writeln);
}
```

## Cartesian Product Implementation

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
        .filter!(t => t[0]^^2 + t[1]^^2 == t[2]^^2)
        .map!(t => tuple(t[0], t[1], t[2]));

    ts.map!array.each!(triple => triple.writeln);
}
```
