# Assorted LaTeX quirks and workarounds

`\inferH` (an Iris wrapper around lkproof's `infer`) needs some tricks to
support newlines. You can either use `\\\\` for a plain line break
(center-aligned), or use `\begin{aligned} ...` by wrapping the entire body in
an extra pair of curly braces.

If you have a binary operator at the end of a line (say in a big equation in an
`aligned` environment), you need to write something like `x + {} \\` so
that LaTeX inserts binary operator spacing between the `x` and the `+`.

(iris.sty-specific) References to `\inferH` will be broken if the `\inferH` is
in a `\[ \]`. Switch to `\begin{mathpar}` to fix this.

In an `align*` environment, a final newline will actually add extra whitespace
after the equation.
