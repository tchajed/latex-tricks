# Assorted LaTeX quirks and workarounds

`\inferH` (an Iris wrapper around lkproof's `infer`) needs some tricks to
support newlines. You can either use `\\\\` for a plain line break
(center-aligned), or use `\begin{aligned} ...` by wrapping the entire body in
an extra pair of curly braces.

If you have a binary operator at the end of a line (say in a big equation in an
`aligned` environment), you need to write something like `x + {} \\` so
that LaTeX inserts binary operator spacing between the `x` and the `+`.
The same goes for operators next to `&` alignment specifiers, e.g.
`x ={}& 5`.

(iris.sty-specific) References to `\inferH` will be broken if the `\inferH` is
in a `\[ \]`. Switch to `\begin{mathpar}` to fix this.

In an `align*` environment, a final newline will actually add extra whitespace
after the equation.

In a math environment, `name` will be interpreted as `n a m e`, i.e., 4
variables "multiplied" with each other. If you want this to render as a single
word, use `\mathit{name}`. You can also use `\operatorname{name}` or
`\DeclareMathOperator` (and wrap them in a command to make this more convenient
to write and read).

When writing a paper (not sure exactly which style sets this up), there's an
`\author` macro where names are separated by `\and`. If you want an explicit
line break in that list, use the following macro:

```tex
\def\andnewline{\end{tabular} \\ \begin{tabular}[t]{c}}
```

(this works because each author is actually its own `\tabular` environment;
`\and` just ends the previous environment and starts a new one)

When a macro expands to a word, LaTeX swallows the space afterward (eg, `\sys`
expands to "Linux" and `\sys is cool` renders as "Linuxis cool"). You can fix
this by writing `\sys{}`, or with `\usepackage{xspace}` and then
`\newcommand{\sys}{Linux\xspace}`.

The following macro will take arguments with LaTeX special characters, and
renders them in a monospace font:
`\newcommand{\cc}[1]{\mbox{\smaller[0.5]\texttt{\detokenize{#1}}}}`. Useful for
small code snippets or referencing identifiers.

You can customize the hyphenation options LaTeX considers for a word with
`\hyphenation`.
