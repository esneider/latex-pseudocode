latex-pseudocode
================

Based on package _clrscode3e_, written by Thomas H. Cormen:

> Package for producing pseudocode in the style of Cormen, Leiserson,
> Rivest, and Stein, Introduction to Algorithms, Third edition.

[See more](http://www.cs.dartmouth.edu/~thc/clrscode/)


Example
-------

![Latex render](https://github.com/esneider/latex-pseudocode/raw/master/images/Dijkstra.png "Pseudocode for Dijkstra's algorithm")


Limitation
----------

This package works only if each procedure has at most 99
numbered lines of code.


Documentation
-------------


Each pseudocode process is typeset within a codebox environment,
```tex
    \begin{codebox}...\end{codebox}.
```

### Process name


Normally, the first line within the codebox environment is a
`\Process` command (optional). The first argument is the process name, and the
optional second argument is a comma separated list of parameters, each
optionally with a description of the parameter (after an equal sign).
Example:
```tex
    \Process{Dijkstra}{G = graph, s = vertex}
```

### Format commands


To typeset the name of a function in small caps, use:
```tex
    \proc{Insertion-Sort}
```


To typeset the name of a constant in small caps, use:
```tex
    \const{true}, \const{nil}
```


To typeset the name of an identifier in regular italics, use:
```tex
    \id{key}, \id{left-sum}
```


To typeset the name of a fixed function in roman, use:
```tex
    \func{sin}, \func{out-degree}
```


To typeset an object attribute, use:
```tex
    \member{user}{name}
```


To typeset array elements, use:
```tex
    \at{names}{pos}
```


All these commands not only use the correct font, they also perform the
important service of interpreting a dash as a hyphen, rather than as a
minus sign. These commands may be used either in or out of math mode.


To typeset subarray ranges, use:
```tex
    $[1 \twodots n]$
```


### Line numbering


Other than the `\Function` line, all lines begin with either `\li` (for
a numbered line) or `\zi` (for an unnumbered line).

The following commands are provided for typesetting keywords and
handling automatic indentation:

+ Loops: `\For`, `\To`, `\By`, `\Downto`, `\Do`, `\While`, `\Repeat`, `\Until`
+ Selection: `\If`, `\Then`, `\Else`, `\ElseIf`, `\ElseNoIf`
+ Jumps: `\Return`, `\Error`, `\Goto`
+ Multithreading: `\Spawn`, `\Sync`, `\Parfor`
+ Comments: `\Comment`, `\RComment`, `\CommentSymbol`
+ Indentation: `\Indentmore`, `\Startalign`, `\Stopalign`


`\label` commands appearing in or after the first numbered line in a
codebox resolve to the number of the most recent numbered line.


Code for the example
--------------------

```tex
\begin{codebox}
    \Process{Dijkstra}{G = graph, s = vertex}

    \li \For each vertex $v \in \id{V_G}$
    \li \Do
            $\at{dist}{v} \gets \infty$
    \li     $\at{parent}{v} \gets \const{NIL}$
        \End
    \li $\at{dist}{s} \gets 0$

    \liempty

        $Q \gets \id{V_G}$

    \li \While $Q \neq \emptyset$
    \li \Do
            $u \gets \proc{Extract-Min}(Q)$

    \li     \For each edge $e = (u,v)$
    \li     \Do
                \If $\at{dist}{v} > \at{dist}{u} + \at{weight}{e}$
    \li         \Then
                    $\at{dist}{v} \gets \at{dist}{u} + \at{weight}{e}$
    \li             $\at{parent}{v} \gets u$
                \End
            \End
        \End

    \liempty

        $H \gets (\id{V_G, \emptyset})$
    \li \For each vertex $v \in \id{V_G},\ v \neq s$
    \li \Do
            $\id{E_H} \gets \id{E_H} \cup \{(\at{parent}{v}, v)\}$
        \End

    \liempty

        \Return $H, \id{dist}$
\end{codebox}
```

