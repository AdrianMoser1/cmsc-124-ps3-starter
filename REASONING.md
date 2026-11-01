# Reasoning for the Predictions Table

Write one entry under every heading below, then commit this file together with
`predictions.tsv`, before you run a case or open `tests/expected.tsv`.

Each entry names the rule that produces the four predicted fields for that
case. One to three sentences is enough. The grader checks structure only. It
does not judge quality, and it sets no word minimum.

After you run the cases, add a short correction under each case you predicted
wrongly. Say what you predicted, what CLISP printed, and which rule you
misread. Those entries belong in the correction commits.

## P01

`` `(+ 1 (* 2 3))` `` starts with the function `+`. The inner form `(* 2 3)` evaluates first, returning `6`, after which `+` adds `1` to it, resulting to `7`. Which is an integer, so the length is `none` and the head is a `function`.

## P02

`` `''(+ 1 2)` `` breaks down to `(quote (quote (+ 1 2)))`. Evaluating the outer quote returns the argument within unevaluated as the list `(quote (+ 1 2))`, which is the value. The list contains two top-level elements and starts with the special operator `quote`, making its kind `cons`, its length `4`, and its operator `special-operator`.

## P03

`` `'nil` `` evaluates to the empty list and symbol `nil`. Because `nil` can act as the null value and an empty sequence, its kind is `null`, its sequence length is `0`, and since it is an atomic form, its operator is `none`.

## P04

`` `'t` `` evaluates to the boolean truth symbol `t`. Which is a symbol, so its kind is `symbol`, its length is `none`, and its operator is `none` because it is an atom.

## P05

`` `(symbolp nil)` `` heads with the function `symbolp`. It evaluates its argument `nil` checking if it is a symbol, returning `t`. Since it is a `symbol`, so the length is `none` and the head is a `function`.

## P06

`` `(car '())` `` heads with the function `car`. The quote hands `car` the empty list, and `car` returns `nil` for its value since there is no element being given to it. Having the `null` kind with a sequence length of `0`, and the head is a `function`.

## P07

`` `(cons 1 '(2 3))` `` heads with the function `cons`. It evaluates both arguments, prepending `1` to the list `(2 3)` to produce `(1 2 3)`. A list with three elements, so the kind is `cons`, the length is `3`, and the head is a `function`.

## P08

`` `(if (null '()) 'empty 'full)` `` heads with the special operator `if`. The condition (null '()) evaluates to nil because an empty list represents falsy, causing the if statement to fail its test and evaluate to nil by default. That is the null value, so the kind is `null`, the length is `0`, and the head is a `special operator`.

## P09

`` `(and 1 nil 3)` `` heads with the special operator `and`. Under CLISP's implementation rules, `and` acts as a special operator, evaluating arguments from left to right and short-circuiting upon encountering `nil`, returning `nil`. That is the null value with length `0` and a `special-operator` head.

## P10

`` `(progn (defvar *ps3-rate* 2) ...)` `` heads with the special operator `progn`. The dynamic variable `*ps3-rate*` is rebound to `10` via `let` inside the sequence, causing `ps3-scale` to compute `3 * 10`, resulting to `30`. An `integer`, so the length is `none` and the operator is a `special operator`.

## P11

`` `(defun ps3-twice (n) (* n 2))` `` heads with the macro `defun`. Evaluating a function definition globally binds the code to the name and returns the symbol naming the function, `ps3-twice`. That is a symbol, so the length is `none` and the operator is a `macro`.

## P12

`` `(labels ((down (n) ...)) (down 3))` `` heads with the special operator `labels`. It recursively constructs a countdown list from `3` down to `1`, producing `(3 2 1)`. That is a list of three elements, so the kind is `cons`, the length is `3`, and the operator is a `special operator`.

## P13

`` `(mapcar #'length '((1 2) () (3)))` `` heads with the function `mapcar`. It applies the `length` function to each sublist in turn, yielding `(2 0 1)`. That is a list of three elements, so the kind is `cons`, the length is `3`, and the operator is a `function`.

## P14

`` `(mapcar (lambda (n) (* n n)) '(1 2 3))` `` heads with the function `mapcar`. It applies the anonymous squaring function to each element of the list, producing `(1 4 9)`. That is a list of three elements, so the kind is `cons`, the length is `3`, and the operator is a `function`.

## P15

`` `(lambda (n) (* n 2))` `` heads with the macro `lambda`. Evaluating an uncalled lambda expression creates and returns an anonymous function object represented as `#<function>`. That is a function kind with length `none` and a `macro` operator.

## P16

`` `(let ((factor 2)) ...)` `` heads with the special operator `let`. The inner lambda expression captures the lexical variable `factor` bound to `2` at its definition site. When `(funcall f 3)` runs later, the inner `factor` bound to `10` is ignored because closures look up variables in the environment where they were born, yielding `6`. That is an integer, so the length is `none` and the operator is a `special operator`.