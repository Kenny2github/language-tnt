
# language-tnt

Typographic Number Theory support in Atom.

## Summary of TNT
### Rules of Well-Formedness
**Numerals**
> 0 is a numeral.
> A numeral preceded by S is also a numeral.
> *Examples*: `0` `S0` `SS0` `SSS0` `SSSS0` `SSSSS0`

**Variables**
> `a` is a variable. If we're not being austere, so are `b`, `c`, `d`, and `e`.
> A variable followed by a prime is also a variable.
> *Examples*: `a` `b′` `c′′` `d′′′` `e′′′′`
> *Other symbols permitted instead of `′`*: `'`

**Terms**
> All numerals and variables are terms.
> A term preceded by `S` is also a term.
> If `s` and `t` are terms, then so are `(s+t)` and `(s⋅t)`.
> *Examples*: `0` `b` `(S0⋅(SS0+c))` `S(Sa⋅(Sb⋅Sc))`
> *Other symbols permitted instead of `⋅`*: `*`, `.`

The above rules tell how to make *parts* of well-formed formulas; the remaining rules tell how to make *complete* well-formed formulas.

**Atoms**
> If `s` and `t` are terms, then `s=t` is an atom.
> *Examples*: `S0=0` `(SS0+SS0)=SSSS0` `S(b+c)=((c⋅d)⋅e)`
> If an atom contains a variable `u`, then `u` is *free* in it. Thus there are four free variables in the last example.

**Negations**
> A well-formed formula preceded by a tilde is well-formed.
> *Examples*: `~S0=0` `~∃b:(b+b)=S0` `~<0=0⊃S0=0>` `~b=S0`
> *Other symbols permitted instead of `~`*: `!`

**Compounds**
> If `x` and `y` are well-formed formulas, and provided that no variable which is free in one is quantified in the other, then the following are all well-formed formulas:
> `<x∧y>`, `<x∨y>`, `<x⊃y>`
> *Examples*: `<0=0∧~0=0>` `<b=b∨~∃c:c=b>` `<S0=0⊃∀c:~∃b:(b+b)=c>`
> *Other symbols permitted instead of `∧`*: `&`, `^`
> *Other symbols permitted instead of `∨`*: `|`, `V`, `v`
> *Other symbols permitted instead of `⊃`*: `→` (Alt+26 on Windows), `]` (less obvious as "implies")

**Quantifications**
> If `u` is a variable, and `x` is a well-formed formula in which `u` is free, then the following strings are well-formed formulas:
> `∃u:x` and `∀u:x`
> *Examples*: `∀b:<b=b∨~∃c:c=b>` `∀c:~∃b:(b+b)=c` `~∃c:Sc=d`
> *Other symbols permitted instead of `∀`*: `A`
> *Other symbols permitted instead of `∃`*: `E`

### Rules of Propositional Calculus
**Joining Rule**: `joining`
> If `x` and `y` are theorems, then `<x∧y>` is a theorem.

**Separation Rule**: `separation`
> If `<x∧y>` is a theorem, then both `x` and `y` are theorems.

**Double-Tilde Rule**: `double-tilde`
> The string `~~` can be deleted from any theorem. It can also be inserted into any theorem, provided that the resulting string is itself well-formed

**Fantasy Rule**: `fantasy rule`
> If `y` can be derived when `x` is assumed to be a theorem, then `<x⊃y>` is a theorem.

**Carry-Over Rule**: `carry over line`*`n`*
> Inside a fantasy, any theorem from the "reality" one level higher can be brought in and used.

**Rule of Detachment**: `detachment`
> If `x` and `<x⊃y>` are both theorems, then `y` is a theorem.

**Contrapositive Rule**: `contrapositive`
> `<x⊃y>` and `<~y⊃~x>` are interchangeable.

**De Morgan's Rule**: `De Morgan`
> `<~x∧~y>` and `~<x∨y>` are interchangeable.

**Switcheroo Rule**: `switcheroo`
> `<x∨y>` and `<~x⊃y>` are interchangeable.

### Rules of TNT
**Rule of Specification**: `specification`
> Suppose `u` is a variable which occurs inside the string `x`. If the string `∀u:x` is a theorem, then so is `x`, and so are any strings made from `x` by replacing `u`, wherever it occurs, by one and the same term.
> (*Restriction*: The term which replaces `u` must not contain any variable that is quantified in `x`.)

**Rule of Generalization**: `generalization`
> Suppose `x` is a theorem in which `u`, a variable, occurs free. Then `∀u:x` is a theorem.
> (*Restriction*: No generalization is allowed in a fantasy on any variable which appeared free in the fantasy's premise.)

**Rule of Interchange**: `interchange`
> Suppose `u` is a variable. Then the strings `∀u:~` and `~∃u:` are interchangeable anywhere inside any theorem.

**Rule of Existence**: `existence`
> Suppose a term (which may contain variables as long as they are free) appears once, or multiply, in a theorem. Then any (or several, or all) of the appearances of the term may be replaced by a variable which otherwise does not occur in the theorem, and the corresponding existential quantifier must be placed in front.

**Rule of Symmetry** (in Equality); `symmetry`
> If `r=s` is a theorem, then so is `s=r`

**Rule of Transitivity** (in Equality): `transitivity`
> If `r=s` and `s=t` are theorems, then so is `r=t`

**Add S** (a Rule of Successorship): `add S`
> If `r=t` is a theorem, then `Sr=St` is a theorem.

**Drop S** (a Rule of Successorship): `drop S`
> If `Sr=St` is theorem, then `r=t` is a theorem.

**Rule of Induction**: `induction`
> Let `X{u}` represent a well-formed formula in which the variable `u` is free, and `X{x/u}` represent the same string, with each appearance of `u` replaced by `x`.
> If both `∀u:<X{u}⊃X{Su/u}>` and `X{0/u}` are theorems, then `∀u:X{u}` is also a theorem.

### Examples
Check the [examples folder](tree/master/examples) - `ascii` contains examples using only ASCII-compatible symbols, `unicode` contains the same examples using the proper (intended) symbols.
