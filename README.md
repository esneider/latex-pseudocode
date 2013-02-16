latex-pseudocode
================

Based on package `clrscode3e`, written by Thomas H. Cormen:

Package for producing pseudocode in the style of Cormen, Leiserson,
Rivest, and Stein, Introduction to Algorithms, Third edition.

[See more](http://www.cs.dartmouth.edu/~thc/clrscode/)

LIMITATION
----------

This package works only if each procedure has at most 99
numbered lines of code.

DOCUMENTATION
-------------

Each pseudocode function is typeset within a codebox environment,
```tex
  \begin{codebox}...\end{codebox}.
```

Normally, the first line within the codebox environment is a
`\Function` command. The first argument is the function name, and the
optional second argument is a comma separated list of parameters, each
optionally with a description of the parameter (after an equal sign).
Example:
```tex
  \Function{Dijkstra}{G = graph, s = vertex}
```
The `\Function` command is optional.

To typeset the name of a function in small caps, use the \proc command:
  \proc{Matrix-Multiply}

To typeset the name of a constant (e.g., nil) in small caps, use the
\const command:
  \const{nil}

To typeset the name of an identifier (e.g., rank) in regular italics,
use the \id command:
  \id{rank}

To typeset the name of a fixed function (e.g., sin) in roman, use the
\func command:
  \func{sin}
(Note that several fixed functions, like sin, are already built into
LaTeX.)

The \proc, \const, \id, and \func commands not only use the correct
font, they also perform the important service of interpreting a dash
as a hyphen, rather than as a minus sign.  These commands may be used
either in or out of math mode.

For attributes, use the various forms of the \attrib commands.

Other than the \Procname line, all lines begin with either \li (for a
numbered line) or \zi (for an unnumbered line).  The following
commands are provided for typesetting keywords and handling automatic
indentation:

Loops: \For, \To, \By, \Downto, \Do, \While, \Repeat, \Until
Selection: \If, \Then, \Else, \ElseIf, \ElseNoIf
Jumps: \Return, \Error, \Goto
Multithreading: \Spawn, \Sync, \Parfor
Comments: \Comment, \RComment, \CommentSymbol
Indentation: \Indentmore, \Startalign, \Stopalign

\label commands appearing in or after the first numbered line in a
codebox resolve to the number of the most recent numbered line.

\twodots produces the ".." notation used for subarrays.

EXAMPLE
-------

```tex
\begin{codebox}
    \Function{Dijkstra}{G = graph, s = vertex}

    \li \For each vertex $v \in \id{V_G}$
    \li \Do
            $\id{dist}[v] \gets \infty$
    \li     $\id{parent}[v] \gets \const{NIL}$
        \End
    \li $\id{dist}[s] \gets 0$

    \liempty

        $Q \gets \id{V_G}$

    \li \While $Q \neq \emptyset$
    \li \Do
            $u \gets \proc{Extract-Min}(Q)$

    \li     \For each edge $e = (u,v)$
    \li     \Do
                \If $\id{dist}[v] > \id{dist}[u] + \id{weight}[e]$
    \li         \Then
                    $\id{dist}[v] \gets \id{dist}[u] + \id{weight}[e]$
    \li             $\id{parent}[v] \gets u$
                \End
            \End
        \End

    \liempty

        $H \gets (\id{V_G, \emptyset})$
    \li \For each vertex $v \in \id{V_G},\ v \neq s$
    \li \Do
            $\id{E_H} \gets \id{E_H} \cup \{(\id{parent}[v], v)\}$
        \End

    \liempty

        \Return $H, \id{dist}$
\end{codebox}
```

Will produce:

![Latex render](https://github.com/esneider/latex-pseudocode/raw/master/images/Dijkstra.png "Pseudocode for Dijkstra's algorithm")

