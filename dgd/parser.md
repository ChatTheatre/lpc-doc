---
title: Parser Reference Manual
layout: default
---

## 1. Introduction

The parse_string() utility parses strings as follows: first, the string is
broken up into two types of smaller strings, called "tokens" and "whitespace".
Next, the resulting array of tokens (whitespace is ignored) is parsed as a
sentence in the language defined by a formal grammar.  For any valid parsings,
LPC functions are called as appropriate, which may transform the array of
tokens, or indicate that a particular parsing of the string is yet to be
considered invalid.  Finally, the resultant array of tokens, if any, is
returned by the function.

Regular expressions are used to define tokens and whitespace, and the language
of those tokens is defined by a context-free grammar, which can be enhanced
with LPC function calls.  Token/whitespace definitions and language definition
together are called "the grammar".

Internally, two partial automatons are generated for each grammar, one to
match tokens and one to parse a sentence of tokens.  Only those parts of the
automatons are generated that are required to parse the sentences seen so far;
this effect is cumulative for successive calls in each object, ensuring that
the automatons are not needlessly generated more than once.  Each object can
handle only one grammar at a time.  If a grammar differs from the previous
one used by the same object, any existing generated automatons are wiped out
and constructed anew.


## 2. Grammar

A grammar consists of token rules and production rules, which may be given in
any order.  Each grammar must contain at least one token rule and one
production rule.


## 2.1 Token rules

A normal token rule has the following format:

    token = /regexp/

where "token" is an identifier name as in LPC, and "regexp" a regular
expression, with the following syntax:

    c	    a single character except `.', `[', `\', `*', `+', `(', `)', `/'
    .	    any single character
    \c	    a single character c, including `.', `[', `\', `*', `+', `(', `)',
	    `/'
    [set]   a single character in the given set, which is constructed of
	    single characters such as `a' and/or character ranges such as
	    `a-z'.  `\' may be used to escape the characters `]', `^', `-', `\'
    [^set]  a single character not in the given set

and, with regular expressions "a" and "b":

    a*      zero or more occurrences of a	(highest precedence)
    a?      zero or one occurrences of a
    a+      one or more occurrences of a
    ab      the concatenation of a and b
    a|b     a or b
    (a)     a					(lowest precedence)

For any regular expression, the longest possible token will be matched.  The
name "whitespace" is reserved for defining a special token, which is simply
skipped.  More than one rule may be specified for each token, including
whitespace.

If a string matches more than token, the token for which the rule appears first
in the grammar is selected.  If a string does not match any token, it is
rejected and parsing fails.

A special token rule may be defined which matches anything not matched by
other rules:

    token = nomatch

where "nomatch" is literal text.  Nomatch rules can be very inefficient, and
their use should be avoided if possible.


## 2.2 Production rules

A production rule has the following format:

    symbol : rule

where "symbol" is an identifier name as in LPC for the production rule, and
"rule" consists of zero or more token symbols, production rule symbols, or
string constants delimited by single quotes.

A string constant in a production rule matches the given sequence of characters
directly, without reference to a token rule.  Since a token rule is implicitly
generated for such string constants, the string constant is also said to be a
token.  String constants take precedence over regular expressions, and any
token that matches both a string constant and a regular expression will always
match the string constant, only.  \`\\' may be used in a string constant to
escape the single quote.

More than one production rule may be given for the same symbol.  All
production rules taken together form a context-free grammar, for which the
start symbol is defined in the first rule.  Production rules that are
unreachable from the start symbol are ignored.  Any symbol used in a
production rule reachable from the start symbol must itself define a token
rule or a production rule.

Optionally, a rule can be followed by an LPC function name:

    symbol : rule ? function

where "function" is the name of an LPC function to be called in the current
object if the specified rule has been matched.


## 3. Parsing

Normally, parse_string() returns a flat array of token strings (if the input
string could be parsed as a sentence in the language defined by the grammar)
or nil (if the input string could not be parsed).  However, the return value
can be modified to an array containing arbitrary other values, including
sub-arrays, by specifying LPC functions in the grammar that will be called
while parsing.  Moreover, if the grammar is ambiguous, sub-arrays for the
alternative may be automatically included in the result.


## 3.1 LPC functions

An LPC function called for a production rule will have a single argument,
an array with the parse tree that matches the production rule.  LPC functions
are called in bottom-up order, so any function calls for sub-parse trees in
the current parse tree will already have been made.

The LPC function can return its argument unchanged, or modify its argument
before returning it, or return a completely different value.  Whatever the
return value is, it is taken to be an array matching the current rule; if
it is not an array at all, the current parse tree (and all parse trees that
depend on it) is discarded altogether.

LPC functions are typically used to replace tokens in the parse tree by
their semantic value, or to add structure to a parse tree, which otherwise
would be represented as a flat array.


## 3.2 Ambiguous grammars

A grammar that allows more than one parse tree for the same input string is
said to be "ambiguous".  The string parser will sort alternative parse trees
by the order of the topmost different rule in the grammar, and by default
ignore all of them but the first one.

An optional third argument to parse_string() can be used to retain an
additional number of alternative parse trees, which will be merged with the
first one; the argument specifies the number of extra alternatives to keep at
each point where sub-parse trees are handled by different rules in the grammar.
Instead of incorporating the first alternative immediately in the array
returned, a sub-array containing all of the alternatives as separate elements
is included, sorted by the order of their topmost rule in the grammar.

LPC functions called for rules can be used to invalidate alternative parse
trees.  Invalidated alternatives will be removed from the overall result.


## 3.3 Writing grammars

Grammars can be parsed most efficiently if they are not ambiguous.  Generally,
ambiguous grammars can be rewritten to be non-ambiguous.  For example,
consider the following (partial) grammar, which is ambiguous:

    Expr: number
    Expr: Expr '+' Expr

It can be rewritten to be either left-recursive,

    Expr: number
    Expr: Expr '+' number

or right-recursive:

    Expr: number
    Expr: number '+' Expr

Neither rewritten grammar is ambiguous, and both explicitly specify the order
in which expressions are to be evaluated: from left to right, or from right to
left, respectively.  If the order doesn't matter, left recursion should be
preferred, as this is parsed more efficiently.
