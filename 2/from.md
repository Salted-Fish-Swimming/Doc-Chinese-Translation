# Intuitionistic Logic

> [from](https://plato.stanford.edu/entries/logic-intuitionistic/)
>
> First published Wed Sep 1, 1999; substantive revision Fri Dec 16, 2022

Intuitionistic logic encompasses the general principles of logical reasoning which have been abstracted by logicians from intuitionistic mathematics, as developed by L. E. J. Brouwer beginning in his [1907] and [1908].
Because these principles also hold for Russian recursive mathematics and the constructive analysis of E. Bishop and his followers, intuitionistic logic may be considered the logical basis of [constructive mathematics](https://plato.stanford.edu/entries/mathematics-constructive/).
Although intuitionistic analysis conflicts with classical analysis, intuitionistic Heyting arithmetic is a subsystem of classical Peano arithmetic.
It follows that intuitionistic propositional logic is a proper subsystem of classical propositional logic, and pure intuitionistic predicate logic is a proper subsystem of pure classical predicate logic.

Philosophically, [intuitionism](https://plato.stanford.edu/entries/intuitionism/) differs from [logicism](https://plato.stanford.edu/entries/logicism/) by treating logic as a part of mathematics rather than as the foundation of mathematics; from finitism by allowing constructive reasoning about potentially uncountable structures (e.g., monotone bar induction on the tree of potentially infinite sequences of natural numbers); and from [Platonism](https://plato.stanford.edu/entries/platonism-mathematics/) by viewing mathematical objects as mental constructs with no independent ideal existence.
Hilbert’s [formalist program](https://plato.stanford.edu/entries/hilbert-program/), to justify classical mathematics by reducing it to a formal system whose consistency should be established by finitistic (hence constructive) means, was the most powerful contemporary rival to Brouwer’s developing intuitionism.
In his 1912 essay Intuitionism and Formalism Brouwer correctly predicted that any attempt to prove the consistency of complete induction on the natural numbers would lead to a vicious circle.

Brouwer rejected [formalism](https://plato.stanford.edu/entries/formalism-mathematics/) per se but admitted the potential usefulness of formulating general logical principles expressing intuitionistically correct constructions, such as modus ponens.
Formal systems for intuitionistic propositional and predicate logic and arithmetic were fully developed by Heyting [1930], Gentzen [1935] and Kleene [1952].
Gödel [1933] proved the equiconsistency of intuitionistic and classical theories.
Beth [1956] and Kripke [1965] provided semantics with respect to which intuitionistic logic is correct and complete, although the completeness proofs for intuitionistic predicate logic require some classical reasoning.

## 1. Rejection of Tertium Non Datur

Intuitionistic logic can be succinctly described as classical logic without the Aristotelian law of excluded middle:

$$ \tag{LEM} A \lor \lnot A $$

or the classical law of double negation elimination:

$$ \tag{DNE} \lnot \lnot A \to A $$

but with the law of contradiction:

$$ (A \to B) \to ((A \to \lnot B) \to \lnot A) $$

and ex falso sequitur quodlibet:

$$ \lnot A \to (A \to B). $$

Brouwer [1908] observed that LEM was abstracted from finite situations, then extended without justification to statements about infinite collections.
For example, let $x,y$ range over the natural numbers $0,1,2,…$ and let $B(y)$ abbreviate $(prime(y) \And prime(y+2))$, where $prime(y)$ expresses “$y$ is a prime number.”
Then $\forall y(B(y) \lor \lnot B(y))$ holds intuitionistically as well as classically, because in order to determine whether or not a natural number is prime we need only check whether or not it has a divisor strictly between itself and $1$.

But if $A(x)$ abbreviates $\exist y (y > x \And B(y))$, then in order to assert $\forall x(A(x) \lor \lnot A(x))$ intuitionistically we would need an effective (cf. the [Church-Turing thesis](https://plato.stanford.edu/entries/church-turing/)) method to determine whether or not there is a pair of twin primes larger than an arbitrary natural number x, and so far no such method is known.
An obvious semi-effective method is to list the prime number pairs using a refinement of Eratosthenes’ sieve (generating the natural numbers one by one and striking out every number $y$ which fails to satisfy $B(y)$), and if there is a pair of twin primes larger than $x$ this method will eventually find the first one.
However, $\forall xA(x)$ expresses the Twin Primes Conjecture, which has not yet been proved or disproved, so in the present state of our knowledge we can assert neither $\forall x(A(x) \lor \lnot A(x))$ nor $\forall xA(x) \lor \lnot ∀xA(x)$.

One may object that these examples depend on the fact that the Twin Primes Conjecture has not yet been settled.
A number of Brouwer’s original “counterexamples” depended on problems (such as Fermat’s Last Theorem) which have since been solved.
But to Brouwer the general LEM was equivalent to the a priori assumption that every mathematical problem has a solution—an assumption he rejected, anticipating Gödel’s incompleteness theorem by a quarter of a century.

The rejection of LEM has far-reaching consequences. On the one hand:

- Intuitionistically, reductio ad absurdum only proves negative statements, since $\lnot \lnot A \to A$ does not hold in general.
(If it did, LEM would follow by modus ponens from the intuitionistically provable $\lnot \lnot (A \lor \lnot A)$.)

- Intuitionistic propositional logic does not have a finite truth-table interpretation.
There are infinitely many distinct axiomatic systems between intuitionistic and classical logic.

- Not every propositional formula has an intuitionistically equivalent disjunctive or conjunctive normal form, built from prime formulas and their negations using only $\lor$ and $\And$.

- Not every predicate formula has an intuitionistically equivalent prenex normal form, with all the quantifiers at the front.

- While $\forall x \lnot \lnot (A(x) \lor \lnot A(x))$ is a theorem of intuitionistic predicate logic, $\lnot \lnot \forall x(A(x) \lor \lnot A(x))$ is not; so $\lnot \forall x(A(x) \lor \lnot A(x))$ is consistent with intuitionistic predicate logic.

On the other hand:

- Every intuitionistic proof of a closed statement of the form $A∨B$ can be effectively transformed into an intuitionistic proof of $A$ or an intuitionistic proof of $B$, and similarly for closed existential statements.

- Intuitionistic propositional logic is effectively decidable, in the sense that a finite constructive process applies uniformly to every propositional formula, either producing an intuitionistic proof of the formula or demonstrating that no such proof can exist.

- The negative fragment of intuitionistic logic (without $∨$ or $∃$) contains a faithful translation of classical logic, and similarly for intuitionistic and classical arithmetic.

- Intuitionistic arithmetic can consistently be extended by axioms which contradict classical arithmetic, enabling the formal study of [recursive mathematics](https://plato.stanford.edu/entries/mathematics-constructive/).

- Brouwer’s controversial [intuitionistic analysis](https://plato.stanford.edu/entries/intuitionism/), which conflicts with LEM, can be formalized and shown consistent relative to a classically and intuitionistically correct subtheory.

## 2. Intuitionistic First-Order Predicate Logic

Formalized intuitionistic logic is naturally motivated by the informal Brouwer-Heyting-Kolmogorov explanation of intuitionistic truth, outlined in the entries on [intuitionism in the philosophy of mathematics](https://plato.stanford.edu/entries/intuitionism/) and [the development of intuitionistic logic](https://plato.stanford.edu/entries/intuitionistic-logic-development/).
The constructive independence of the logical operations $\And , \lor , \to , \lnot , \forall , \exists$ contrasts with the classical situation, where e.g., $A \lor B$ is equivalent to $\lnot (\lnot A \And \lnot B)$, and $\exists xA(x)$ is equivalent to $\lnot \forall x \lnot A(x)$.
From the B-H-K viewpoint, a sentence of the form $A \lor B$ asserts that either a proof of $A$, or a proof of $B$, has been constructed; while $\lnot (\lnot A \And \lnot B)$ asserts that an algorithm has been constructed which would effectively convert any pair of constructions proving $\lnot A$ and $\lnot B$ respectively, into a proof of a known contradiction.

### 2.1 The formal systems $\mathbf{H–IPC}$ and $\mathbf{H–IQC}$

Following is a Hilbert-style formalism $\mathbf{H–IQC}$ from Kleene [1952] (cf. Troelstra and van Dalen [1988]) for intuitionistic first-order predicate logic.
The language $L$ of $\mathbf{H–IQC}$ has predicate letters $P, Q(.), \dots$ of all arities and individual variables $x, y, z, \dots$ (with or without subscripts $1, 2, \dots$), as well as symbols $\And, \lor, \to, \lnot, \forall, \exists$ for the logical connectives and quantifiers, and parentheses (, ).
The atomic (or prime) formulas of $L$ are expressions such as $P, Q(x), R(x, y, x)$ where $P, Q(.), R(\dots)$ are $0$-ary, $1$-ary and $3$-ary predicate letters respectively; that is, the result of filling each blank in a predicate letter by an individual variable symbol is a prime formula.
The (well-formed) formulas of $L$ are defined inductively as follows:

- Each atomic formula is a formula.

- If $A$ and $B$ are formulas, so are $(A \And B),(A \lor B),(A \to B)$ and $\lnot A$.

- If $A$ is a formula and $x$ is a variable, then $\forall xA$ and $\exists xA$ are formulas.

In general, we use $A,B,C$ as metavariables for well-formed formulas and $x,y,z$ as metavariables for individual variables.
Anticipating applications (for example to intuitionistic arithmetic) we use $s,t$ as metavariables for terms; in the case of pure predicate logic, terms are simply individual variables.
An occurrence of a variable $x$ in a formula $A$ is bound if it is within the scope of a quantifier $\forall x$ or $\exists x$, otherwise free.
Intuitionistically as classically, $(A \leftrightarrow B)$ abbreviates $((A \to B) \And (B \to A))$, and parentheses will be omitted when this causes no confusion.

here are three rules of inference:

> Modus Ponens
>
> From $A$ and $A \to B$, conclude $B$.

> $\forall$-Introduction
> 
> From $C \to A(x)$, where $x$ is a variable which does not occur free in $C$, conclude $C \to \forall xA(x)$.

> $\exists$-Elimination
> 
> From $A(x) \to C$, where $x$ is a variable which does not occur free in $C$, conclude $\exists xA(x) \to C$.

The axioms are all formulas of the following forms, where in the last two schemas the subformula $A(t)$ is the result of substituting an occurrence of the term t for every free occurrence of x in $A(x)$, and no variable free in $t$ becomes bound in $A(t)$ as a result of the substitution.

$$
\begin{array}{l}
A \to(B \to A) \\
(A \to B) \to ((A \to (B \to C)) \to(A \to C)) \\
A \to(B \to (A \And B)) \\
(A \And B) \to A \\
(A \And B) \to B \\
A \to (A \lnot B) \\
B \to (A \lnot B) \\
(A \to C) \to ((B \to C) \to((A \lnot B) \to C))	\\
(A \to B) \to ((A \to \lnot B) \to \lnot A) \\
\lnot A \to(A \to B) \\
\forall xA(x) \to A(t) \\
A(t) \to \exists xA(x)
\end{array}
$$

A proof is any finite sequence of formulas, each of which is an axiom or an immediate consequence, by a rule of inference, of (one or two) preceding formulas of the sequence.
Any proof is said to prove its last formula, which is called a theorem or provable formula of first-order intuitionistic predicate logic.
A derivation of a formula $E$ from a collection $F$ of assumptions is any sequence of formulas, each of which belongs to $F$ or is an axiom or an immediate consequence, by a rule of inference, of preceding formulas of the sequence, such that $E$ is the last formula of the sequence.
If such a derivation exists, we say $E$ is derivable from $F$.

Intuitionistic propositional logic $\mathbf{H-IPC}$ the subsystem of $\mathbf{H–IQC}$ which results when the language is restricted to formulas built from proposition letters $P, Q, R, \dots$ using the propositional connectives $\And, \lor, \to$ and $\lnot$, and only the propositional postulates are used.
Thus the last two rules of inference and the last two axiom schemas are absent from the propositional subsystem.

If, in the given list of axiom schemas for intuitionistic propositional or first-order predicate logic, the law expressing ex falso sequitur quodlibet:

$$ \lnot A \to (A \to B) $$

is replaced by the classical law of double negation elimination DNE:

$$ \lnot \lnot A \to A $$

(or, equivalently, if the intuitionistic law of negation introduction:

$$ (A \to B) \to ((A \to \lnot B) \to \lnot A) $$

is replaced by LEM), a formal system $\mathbf{H–CPC}$ for classical propositional logic or $\mathbf{H–CQC}$ for classical predicate logic results.
Since ex falso and the law of contradiction are classical theorems, intuitionistic logic is contained in classical logic.
In a sense, classical logic is also contained in intuitionistic logic; see Section 4.1 below.

It is important to note that while LEM and DNE are equivalent as schemas over $\mathbf{H–IPC}$, the implication

$$ (\lnot \lnot A \to A) \to (A \lor \lnot A) $$

is not a theorem schema of $\mathbf{H–IPC}$. For theories $\mathbf{T}$ based on intuitionistic logic, if $E$ is an arbitrary formula of $L(\mathbf{T})$ then by definition:

$E$ is decidable in $\mathbf{T}$ if and only if $\mathbf{T}$ proves $E \lor \lnot E$.

$E$ is stable in $\mathbf{T}$ if and only if $\mathbf{T}$ proves $\lnot \lnot E \to E$.

$E$ is testable in $\mathbf{T}$ if and only if $\mathbf{T}$ proves $\lnot E \lor \lnot \lnot E$.

Decidability implies stability, but not conversely.
The conjunction of stability and testability is equivalent to decidability.
Brouwer himself proved that “absurdity of absurdity of absurdity is equivalent to absurdity” (Brouwer [1923C]), so every formula of the form $\lnot A$ is stable; but in $\mathbf{H–IPC}$ and $\mathbf{H–IQC}$ prime formulas and their negations are undecidable, as shown in Section 5.1 below.

### 2.2 Alternative formalisms, and the deduction theorem

The Hilbert-style system $\mathbf{H–IQC}$ is useful for metamathematical investigations of intuitionistic logic, but its forced linearization of deductions and its preference for axioms over rules make it an awkward instrument for establishing derivability.
A natural deduction system $\mathbf{N–IQC}$ for intuitionistic predicate logic results from the deductive system $\mathbf{D}$, presented in Section 3 of the entry on [classical logic](https://plato.stanford.edu/entries/logic-classical/) in this Encyclopedia, by omitting the symbol and rules for identity, and replacing the classical rule (DNE) of double negation elimination by the intuitionistic negation elimination rule expressing ex falso:

(INE) If $F$ entails $A$ and $F$ entails $\lnot A$, then $F$ entails $B$.

The keys to proving that $\mathbf{H–IQC}$ is equivalent to $\mathbf{N–IQC}$ are modus ponens and its converse, the:

> **Deduction Theorem**
> 
> If $B$ is derivable from $A$ and possibly other formulas $F$, with all variables free in $A$ held constant in the derivation (that is, without using the second or third rule of inference on any variable x occurring free in $A$, unless the assumption $A$ does not occur in the derivation before the inference in question), then $A \to B$ is derivable from $F$.

This fundamental result, roughly expressing the rule $(\to I)$ of $\mathbf{I}$, can be proved for $\mathbf{H–IQC}$ by induction on the definition of a derivation.
The other rules of $\mathbf{I}$ hold for $\mathbf{H–IQC}$ essentially by modus ponens, which corresponds to $(\to E)$ in $\mathbf{N–IQC}$; and all the axioms of $\mathbf{H–IQC}$ are provable in $\mathbf{N–IQC}$.

To illustrate the usefulness of the Deduction Theorem, consider the (apparently trivial) theorem schema $(A \to A)$.
A correct proof in $\mathbf{H–IPC}$ takes five lines:

1. $A \to (A \to A)$

2. $(A \to (A \to A)) \to ((A \to ((A \to A) \to A)) \to (A \to A))$

3. $(A \to ((A \to A) \to A)) \to (A \to A)$

4. $A \to ((A \to A) \to A)$

5. $A \to A$

where 1, 2 and 4 are axioms and 3, 5 come from earlier lines by modus ponens. However, $A$ is derivable from $A$ (as assumption) in one obvious step, so the Deduction Theorem allows us to conclude that a proof of $A \to A$ exists. (In fact, the formal proof of $A \to A$ just presented is part of the constructive proof of the Deduction Theorem!)

It is important to note that, in the definition of a derivation from assumptions in $\mathbf{H–IQC}$,
the assumption formulas are treated as if all their free variables were universally quantified, so that $\forall xA(x)$ is derivable from the hypothesis $A(x)$. However, the variable x will be varied (not held constant) in that derivation, by use of the rule of $\forall$-introduction; and so the Deduction Theorem cannot be used to conclude (falsely) that $A(x) \to \forall xA(x)$ (and hence, by $\exists$-elimination, $\exists xA(x) \to \forall xA(x)$) are provable in $\mathbf{H–IQC}$. As an example of a correct use of the Deduction Theorem for predicate logic, consider the implication $\exists xA(x) \to \lnot \forall x \lnot A(x)$. To show this is provable in $\mathbf{H–IQC}$, we first derive $\lnot \forall x \lnot A(x)$ from $A(x)$ with all free variables held constant:

1. $\forall x \lnot A(x) \to \lnot A(x)$ 

2. $A(x) \to (\forall x \lnot A(x) \to A(x))$

3. $A(x)$ (assumption)

4. $\forall x \lnot A(x) \to A(x)$

5. $(\forall x \lnot A(x) \to A(x)) \to ((\forall x \lnot A(x) \to \lnot A(x)) \to \lnot \forall x \lnot A(x))$

6. $(\forall x \lnot A(x) \to \lnot A(x)) \to \lnot \forall x \lnot A(x)$

7. $\lnot \forall x \lnot A(x)$

Here 1, 2 and 5 are axioms; 4 comes from 2 and 3 by modus ponens; and 6 and 7 come from earlier lines by modus ponens; so no variables have been varied.
The Deduction Theorem tells us there is a proof $P$ in $\mathbf{H–IQC}$ of $A(x) \to \lnot \forall x \lnot A(x)$, and one application of $\exists$-elimination converts $P$ into a proof of $\exists xA(x) \to \lnot \forall x \lnot A(x)$.
The converse is not provable in $\mathbf{H–IQC}$, as shown in Section 5.1 below.

Other important alternatives to $\mathbf{H–IQC}$ and $\mathbf{N–IQC}$ are the various sequent calculi for intuitionistic propositional and predicate logic.
The first such calculus was defined by Gentzen [1934–5], cf. Kleene [1952].
Sequent systems, which prove exactly the same formulas as $\mathbf{H–IQC}$ and $\mathbf{N–IQC}$, keep track explicitly of all assumptions and conclusions at each step of a proof, replacing modus ponens (which eliminates an intermediate formula) by a cut rule (which can be shown to be an admissible rule (cf. Section 4.2) for the subsystem remaining when it is omitted).

When the details of the formalism are not important, from now on we follow Troelstra and van Dalen [1988] in letting “$\mathbf{IQC}$” or “$\mathbf{IPC}$” refer to any formal system for intuitionistic predicate or propositional logic respectively, and similarly “$\mathbf{CQC}$” and “$\mathbf{CPC}$” for classical predicate and propositional logic.

Both $\mathbf{IPC}$ and $\mathbf{IQC}$ satisfy interpolation theorems, e.g.: If $A$ and $B$ are propositional formulas having at least one proposition letter in common, and if $A \to B$ is provable in $\mathbf{IPC}$, then there is a formula $C$, containing only proposition letters which occur in both $A$ and $B$, such that both $A \to C$ and $C \to B$ are provable.
These topics are treated in Kleene [1952] and Troelstra and Schwichtenberg [2000].

While identity can of course be added to intuitionistic logic, for applications (e.g., to arithmetic) the equality symbol is generally treated as a distinguished predicate constant satisfying the axioms for an equivalence relation (reflexivity, symmetry and transitivity) and additional nonlogical axioms (e.g., the primitive recursive definitions of addition and multiplication).
Identity is decidable, intuitionistically as well as classically, but intuitionistic extensional equality is not always decidable; see the discussion of Brouwer’s continuity axioms in Section 3 of the entry on [intuitionism in the philosophy of mathematics](https://plato.stanford.edu/entries/intuitionism/).

## 3. Intuitionistic Number Theory (Heyting Arithmetic) HA

Intuitionistic (Heyting) arithmetic $\mathbf{HA}$ and classical (Peano) arithmetic $\mathbf{PA}$ share the same first-order language and the same non-logical axioms; only the logic is different.
In addition to the logical connectives, quantifiers and parentheses and the individual variables $x,y,z,\dots$ (also used as metavariables), the language $L(\mathbf{HA})$ of arithmetic has a binary predicate symbol =, individual constant $0$, unary function constant $S$, and finitely or countably infinitely many additional constants for primitive recursive functions including addition and multiplication; the precise choice is a matter of taste and convenience.
Terms are built from variables and $0$ using the function constants; in particular, each natural number $n$ is expressed in the language by the numeral $\mathbf{n}$ obtained by applying $S n$ times to $0$ (e.g., $S(S(0))$ is the numeral for $2$).
Prime formulas are of the form $(s=t)$ where $s,t$ are terms, and compound formulas are obtained from these as usual.

The logical axioms and rules of $\mathbf{HA}$ are those of first-order intuitionistic predicate logic $\mathbf{IQC}$.
The nonlogical axioms include the reflexive, symmetric and transitive properties of $=$:

$$ \forall x (x = x) , $$
$$ \forall x \forall y (x = y \to y = x) , $$
$$ \forall x \forall y \forall z ((x = y \And y = z) \to x = z) ; $$

the axiom characterizing $0$ as the least natural number:

$$ \forall x \lnot(S(x) = 0), $$

the axiom characterizing $S$ as a one-to-one function:

$$ \forall x \forall y(S(x) = S(y) \to x = y), $$

the extensional equality axiom for $S$:

$$ \forall x \forall y(x = y \to S(x) = S(y)); $$

the primitive recursive defining equations for each function constant, in particular for addition:

$$ \forall x(x + 0 = x), $$
$$ \forall x \forall y(x + S(y) = S(x+y)); $$

and multiplication:

$$ \forall x(x \cdot 0=0), $$
$$ \forall x \forall y(x \cdot S(y) = (x \cdot y) + x); $$

and the (universal closure of the) schema of mathematical induction, for arbitrary formulas $A(x)$:

$$ (A(0) \And \forall x(A(x) \to A(S(x)))) \to \forall xA(x). $$

Extensional equality axioms for all function constants are derivable by mathematical induction from the equality axiom for $S$ and the primitive recursive function axioms.

The natural order relation $x<y$ can be defined in $\mathbf{HA}$ by $\exists z(S(z) + x = y)$, or by the quantifier-free formula $S(x) \dot{−} y = 0$ if the symbol and primitive recursive defining equations for predecessor :

$$ Pd(0) = 0, $$
$$ \forall x (Pd(S(x)) = x) $$

and cutoff subtraction :

$$ \forall x (x \dot{−} 0 = x), $$
$$ \forall x \forall y(x \dot{−} S(y) = Pd(x \dot{−} y)) $$

are present in the formalism. $\mathbf{HA}$ proves the comparative law

$$
∀x∀y(x<y∨x=y∨y<x)
$$

and an intuitionistic form of the least number principle, for arbitrary formulas $A(x)$ :

$$
\forall x[\forall y (y < x \to (A(y) \vee \lnot A(y))) \to \\
(\exists y ((y < x \And A(y)) \And \forall z(z < y \to \lnot A(z))) \vee \\
\forall y(y < x \to \lnot A(y)))].
$$

The hypothesis is needed because not all arithmetical formulas are decidable in $\mathbf{HA}$.
However, $\forall x \forall y (x = y \lor \lnot (x = y))$ can be proved directly by mathematical induction, and so: 

- Prime formulas (and hence all quantifier-free formulas) are decidable and stable in $\mathbf{HA}.

If $A(x)$ is decidable in $\mathbf{HA}$, then by induction on $x$ so are $\forall y (y < x \to A(y))$ and $\exists y (y < x \And A(y))$.
Hence:

- Formulas in which all quantifiers are bounded are decidable and stable in $\mathbf{HA}$.

The collection $\Delta_0$ of arithmetical formulas in which all quantifiers are bounded is the lowest level of a classical arithmetical hierarchy based on the pattern of alternations of quantifiers in a prenex formula.
In $\mathbf{HA}$ not every formula has a prenex form, but Burr [2004] discovered a simple intuitionistic arithmetical hierarchy corresponding level by level to the classical.
For the purposes of the next two definitions only, $\forall x$ denotes a block of finitely many universal number quantifiers, and similarly $\exists x$ denotes a block of finitely many existential number quantifiers.
With these conventions, Burr’s classes $\Phi_n$ and $\Psi_n$ are defined by:

- $\Phi_0 = \Psi_0 = \Delta_0,$

- $\Phi_1$ is the class of all formulas of the form $\forall x A(x)$ where $A(x)$ is in $\Psi_0$.
For $n \ge 2$, $\Phi_n$ is the class of all formulas of the form $\forall x[A(x) \to \exists y B(x,y)]$ where $A(x)$ is in $\Phi_{n−1}$ and $B(x,y)$ is in $\Phi_{n−2}$,

- $\Psi_1$ is the class of all formulas of the form $\exists x A(x)$ where $A(x)$ is in $\Phi_0$. For $n \ge 2$, $\Psi_n$ is the class of all formulas of the form $A \to B$ where $A$ is in $\Phi_n$ and $B$ is in $\Phi_{n−1}$.

The corresponding classical prenex classes are defined more simply:

- $\Pi_0 = \Sigma_0= \Delta_0,$

- $\Pi_{n+1}$ is the class of all formulas of the form $\forall x A(x)$ where $A(x)$ is in $\Sigma_n$,

- $\Sigma_{n+1}$ is the class of all formulas of the form $\exists x A(x)$ where $A(x)$ is in $\Pi_n$.

Peano arithmetic $\mathbf{PA}$ comes from Heyting arithmetic $\mathbf{HA}$ by adding LEM or $\lnot \lnot A \to A$ to the list of logical axioms, i.e., by using classical instead of intuitionistic logic. The following results hold even in the fragments of $\mathbf{HA}$ and $\mathbf{PA}$ with the induction schema restricted to $\Delta_0$ formulas.

> **Burr’s Theorem:**
> 
> - Every arithmetical formula is provably equivalent in $\mathbf{HA}$ to a formula in one of the classes $\Phi_n$.
> 
> - Every formula in $\Phi_n$ is provably equivalent in $\mathbf{PA}$ to a formula in $\Pi_n$, and conversely.
> 
> - Every formula in $\Psi_n$ is provably equivalent in $\mathbf{PA}$ to a formula in $\Sigma_n$, and conversely.

$\mathbf{HA}$ and $\mathbf{PA}$ are proof-theoretically equivalent, as will be shown in Section 4. Each is capable of (numeralwise) expressing its own proof predicate.
By Gödel’s famous Incompleteness Theorem, if $\mathbf{HA}$ is consistent then neither $\mathbf{HA}$ nor$\mathbf{PA}$ can prove its own consistency.

## 4. Basic Proof Theory

### 4.1 Translating classical into intuitionistic logic

A fundamental fact about intuitionistic logic is that it has the same consistency strength as classical logic.
For propositional logic this was first proved by Glivenko [1929]:

> **Glivenko’s Theorem**
> 
> An arbitrary propositional formula $A$ is classically provable, if and only if $\lnot \lnot A$ is intuitionistically provable.

Glivenko’s Theorem does not extend to predicate logic, although an arbitrary predicate formula $A$ is classically provable if and only if $\lnot \lnot A$ is provable in intuitionistic predicate logic plus the “double negation shift” schema.

$$
\tag{DNS} \forall x \lnot \lnot B(x) \to \lnot \lnot \forall xB(x)
$$

The more sophisticated **negative translation** of classical into intuitionistic theories, due independently to Gödel and Gentzen, associates with each formula $A$ of the language $L$ another formula $g(A)$ (with no $\lor$ or $\exists$), such that:

- (I) Classical predicate logic proves $A \leftrightarrow g(A)$.

- (II) Intuitionistic predicate logic proves $g(A) \leftrightarrow \lnot \lnot g(A)$.

- (III) If classical predicate logic proves $A$, then intuitionistic predicate logic proves $g(A)$.

The proofs are straightforward from the following inductive definition of $g(A)$ (using Gentzen’s direct translation of implication, rather than Gödel’s in terms of $\lnot$ and $\And$):

$$
\begin{align*}
g(P) &\text{ is } \lnot \lnot P, \text{ if } P \text{ is prime}.\\
g(A \And B) &\text{ is } g(A) \And g(B). \\
g(A \vee B) &\text{ is } \lnot(\lnot g(A) \And \lnot g(B)). \\
g(A \rightarrow B) &\text{ is } g(A) \rightarrow g(B). \\
g(\lnot A) &\text{ is } \lnot g(A). \\
g(\forall xA(x)) &\text{ is }\forall x g(A(x)). \\
g(\exists xA(x)) &\text{ is } \lnot \forall x\lnot g(A(x)).
\end{align*}
$$

For each formula $A$, $g(A)$ is provable intuitionistically if and only if $A$ is provable classically.
In particular, if $B \And \lnot B$ were classically provable for some formula $B$, then $g(B) \And \lnot g(B)$ (which is $g(B \And \lnot B)$) would in turn be provable intuitionistically.
Hence:

- (IV) Classical and intuitionistic predicate logic are equiconsistent.

The negative translation of classical into intuitionistic number theory is even simpler, since prime formulas of intuitionistic arithmetic are stable.
Thus $g(s = t)$ can be taken to be $s = t$, and the other clauses are unchanged.
The negative translation of each instance of the schema of mathematical induction is an instance of the same schema, and the other nonlogical axioms of arithmetic are their own negative translations, so:

- (I), (II), (III) and (IV) hold also for number theory.

Gödel [1933e] interpreted these results as showing that intuitionistic logic and arithmetic are richer than classical logic and arithmetic, because the intuitionistic theory distinguishes formulas which are classically equivalent, and has the same [consistency strength](https://plato.stanford.edu/entries/hilbert-program/) as the classical theory.
In particular, Gödel’s incompleteness theorems apply to $\mathbf{HA}$ as well as to $\mathbf{PA}$.

Direct attempts to extend the negative interpretation to analysis fail because the negative translation of the countable axiom of choice is not a theorem of intuitionistic analysis.
However, it is consistent with intuitionistic analysis, including Brouwer’s controversial continuity principle, by the functional version of Kleene’s recursive realizability (cf. Section 6.3 below).
It follows that intuitionistic mathematics, which can only be expressed by using all the standard logical connectives and quantifiers, is consistent with a faithful translation of classical mathematics avoiding $\lor$ and $\exists$.

This is important because Brouwer’s intuitionistic analysis is inconsistent with LEM.
However, if $A$ is any negative formula (without $\lor$ or $\exists$) then $\lnot \lnot A \to A$ is provable using intuitionistic logic.
A reconciliation of intuitionistic and classical analysis along these lines, inspired by Troelstra [1977] and Kripke[2019], is suggested in Moschovakis [2017].

### 4.2 Admissible rules of intuitionistic logic and arithmetic

Gödel [1932] observed that intuitionistic propositional logic has the **disjunction property**:

> (DP) If $A \lor B$ is a theorem, then $A$ is a theorem or $B$ is a theorem. 

Gentzen [1935] established the disjunction property for closed formulas of intuitionistic predicate logic.
From this it follows that if intuitionistic logic is consistent, then $P \lor \lnot P$ is not a theorem if $P$ is an atomic formula.
Kleene [1945, 1952] proved that intuitionistic first-order number theory also has the related (cf. Friedman [1975]) **existence property**:

> (EP) If $\exists x A(x)$ is a closed theorem, then for some closed term $t, A(t)$ is a theorem. 

The disjunction and existence properties are special cases of a general phenomenon peculiar to nonclassical theories.
The admissible rules of a theory are the rules under which the theory is closed. For example, Harrop [1960] observed that the rule:

- If $\lnot A \to (B \lor C)$ is a theorem, so is $(\lnot A \to B) \lor (\lnot A \to C)$
 
is admissible for intuitionistic propositional logic $\mathbf{IPC}$ because if $A$, $B$ and $C$ are any formulas such that $\lnot A \to (B \lor C)$ is provable in $\mathbf{IPC}$, then $(\lnot A \to B) \lor (\lnot A \to C)$ is provable in $\mathbf{IPC}$.
Harrop’s rule is not derivable in $\mathbf{IPC}$ because the formula

$$ (\lnot A \to (B \lor C)) \to ((\lnot A \to B) \lor (\lnot A \to C)) $$

is not intuitionistically provable.
Another important example of an admissible nonderivable rule of $\mathbf{IPC}$ is Mints’s rule:

- If $(A \to B) \to (A \lor C)$ is a theorem, so is $((A \to B) \to A) \lor ((A \to B) \to C)$.

The two-valued truth table interpretation of classical propositional logic $\mathbf{CPC}$ gives rise to a simple proof that every admissible rule of $\mathbf{CPC}$is derivable: otherwise, some assignment to $A$, $B$, etc. would make the hypothesis true and the conclusion false, and by substituting e.g. $P \to P$ for the letters assigned “true” and $P \And \lnot P$ for those assigned “false” one would have a provable hypothesis and unprovable conclusion.
The fact that the intuitionistic situation is more interesting leads to many natural questions, some of which have recently been answered.

By generalizing Mints’s Rule, Visser and de Jongh identified a recursively enumerable sequence of successively stronger admissible rules (“Visser’s rules”) which, they conjectured, formed a basis for the admissible rules of $\mathbf{IPC}$ in the sense that every admissible rule is derivable from the disjunction property and one of the rules of the sequence.
Building on work of Ghilardi [1999], Iemhoff [2001] succeeded in proving their conjecture.
Rybakov [1997] proved that the collection of all admissible rules of $\mathbf{IPC}$ is decidable but has no finite basis.
Visser [2002] showed that his rules are also the admissible propositional rules of $\mathbf{HA}$, and of $\mathbf{HA}$ extended by Markov’s Principle MP (defined in Section 5.2 below).
More recently, Jerabek [2008] found an independent basis for the admissible rules of $\mathbf{IPC}$, with the property that no rule in the basis derives another.

Much less is known about the admissible rules of intuitionistic predicate logic.
Pure $\mathbf{IQC}$, without individual or predicate constants, has the following remarkable admissible rule for $A(x)$ with no variables free but $x$ :

- If $\exists x A(x)$ is a theorem, so is $\forall x A(x)$.

Not every admissible predicate rule of $\mathbf{IQC}$ is admissible for all formal systems based on $\mathbf{IQC}$; for example, $\mathbf{HA}$ evidently violates the rule just stated.
Visser proved in [1999] that the property of being an admissible predicate rule of $\mathbf{HA}$ is $\Pi_2$ complete, and in [2002] that $\mathbf{HA}$ + MP has the same predicate admissible rules as $\mathbf{HA}$.
Plisko [1992] proved that the predicate logic of $\mathbf{HA}$ + MP (the set of sentences in the language of $\mathbf{IQC}$ all of whose uniform substitution instances in the language of arithmetic are provable in $\mathbf{HA}$ + MP) is Π2 complete; Visser [2006] extended this result to some constructively interesting consistent extensions of $\mathbf{HA}$ which are not contained in $\mathbf{PA}$.

While they have not been completely classified, the admissible rules of intuitionistic predicate logic are known to include **Markov’s Rule** for decidable predicates:

- If $\forall x (A(x) \lor \lnot A(x)) \And \lnot \forall x \lnot A(x)$ is a theorem, so is $\exists x A(x)$.

And the following **Independence-of-Premise** Rule (where $y$ is assumed not to occur free in $A(x)$) :

- If $\forall x (A(x) \lor \lnot A(x)) \And (\forall x A(x) \to \exists y B(y))$ is a theorem, so is $\exists y(\forall xA(x) \to B(y))$.

Both rules are also admissible for $\mathbf{HA}$.
The corresponding implications (MP and IP respectively), which are not provable intuitionistically, are verified by Gödel’s “Dialectica” interpretation of $\mathbf{HA}$ (cf. Section 6.3 below).
So is the implication (CT) corresponding to one of the most interesting admissible rules of Heyting arithmetic, let us call it the **Church-Kleene** Rule: 

- If $\forall x \exists y A(x,y)$ is a closed theorem of $\mathbf{HA}$ then there is a number n such that, provably in $\mathbf{HA}$, the partial recursive function with Gödel number n is total and maps each x to a y satisfying $A(x,y)$ (and moreover $A(x,y)$ is provable, where $\mathbf{x}$ is the numeral for the natural number $x$ and $\mathbf{y}$ is the numeral for $y$).

Combining Markov’s Rule with the negative translation gives the result that classical and intuitionistic arithmetic prove the same formulas of the form $\forall x\exists y A(x,y)$ where $A(x,y)$ is quantifier-free.
In general, if $A(x,y)$ is provably decidable in $\mathbf{HA}$ and if $\forall x\exists y A(x,y)$ is a closed theorem of classical arithmetic $\mathbf{PA}$, the conclusion of the Church-Kleene Rule holds even in intuitionistic arithmetic.
For if $\mathbf{HA}$ proves $\forall x\forall y (A(x,y) \lor \lnot A(x,y))$ then by the Church-Kleene Rule the characteristic function of A(x,y) has a Gödel number m, provably in $\mathbf{HA}$; so $\mathbf{HA}$ proves $\forall x\exists y A(x,y) \leftrightarrow \forall x\exists y\exists zB(m,x,y,z)$ where $B$ is quantifier-free, and the adjacent existential quantifiers can be contracted in $\mathbf{HA}$.
It follows that $\mathbf{HA}$ and $\mathbf{PA}$ have the same provably recursive functions.

Here is a proof that the rule “If $\forall x (A \lor B(x))$ is a theorem, so is $A \lor \forall x B(x)$” (where $x$ is not free in $A$) is not admissible for $\mathbf{HA}$, if $\mathbf{HA}$ is consistent.
Gödel numbering provides a quantifier-free formula $G(x)$ which (numeralwise) expresses the predicate “$x$ is the code of a proof in $\mathbf{HA}$ of $(0 = 1)$.”
By intuitionistic logic with the decidability of quantifier-free arithmetical formulas, $\mathbf{HA}$ proves $\forall x (\exists yG(y) \lor \lnot G(x))$.
However, if $\mathbf{HA}$ proved $\exists yG(y) \lor \forall x \lnot G(x)$ then by the disjunction property, $\mathbf{HA}$ must prove either $\exists yG(y)$ or $\forall x \lnot G(x)$.
The first case is impossible, by the existence property with the consistency assumption and the fact that $\mathbf{HA}$ proves all true quantifier-free sentences.
But the second case is also impossible, by Gödel’s second incompleteness theorem, since $\forall x \lnot G(x)$ expresses the consistency of $\mathbf{HA}$.

## 5. Basic Semantics

The most direct way to show that a formula (or schema) $F$ is provable in a formal system $\mathbf{S}$ is to construct a proof of $F$ in $\mathbf{S}$.
But if a formula (or some substitution instance of a schema) happens not to be provable in $\mathbf{S}$, how can that fact be known? Our failure to find a proof may suggest unprovability, but is not in general decisive unless the proof search is a canonical one in Gentzen’s system for intuitionistic propositional logic.
Usually what is needed is an interpretation with respect to which $\mathbf{S}$ is sound, in the sense that every provable formula is valid under the interpretation.
Then to show $\mathbf{F}$ unprovable in $\mathbf{S}$ it suffices to show that $\mathbf{F}$ is invalid under the interpretation, typically by constructing a countermodel to $\mathbf{F}$.

If a system $\mathbf{S}$ is complete for an interpretation, in the sense that every formula which is valid under the interpretation is provable in $\mathbf{S}$, then an indirect way to show that a formula (or schema) is provable in $\mathbf{S}$ is to establish its validity under the interpretation.
Completeness does not always accompany soundness; for instance, Heyting arithmetic is sound but incomplete for the realizability interpretation described in Section 5.2 below.

Intuitionistic systems have inspired a variety of interpretations, including Beth’s tableaux, Rasiowa and Sikorski’s topological models, Heyting algebras, formulas-as-types, Kleene’s recursive realizabilities, the Kleene and Aczel slashes, and models based on sheafs and topoi.
Of all these interpretations Kripke’s [1965] possible-world semantics, with respect to which intuitionistic predicate logic is sound and complete, most resembles classical model theory.
Recursive realizability interpretations, on the other hand, attempt to effectively implement the B-H-K explanation of intuitionistic truth.

### 5.1 Kripke and Beth semantics for intuitionistic logic

A Kripke structure $\mathbf{K}$ for $L$ consists of a partially ordered set $K$ of nodes and a domain function D assigning to each node $k$ in $K$ an inhabited set $D(k)$, such that if $k \le k′$, then $D(k) \subseteq D(k′)$.
In addition $\mathbf{K}$ has a forcing relation determined as follows.

For each node $k$ let $L(k)$ be the language extending $L$ by new constants for all the elements of $D(k)$.
To each node $k$ and each 0-ary predicate letter (each proposition letter) $P$, either assign $f(P,k)=$ true or leave $f(P,k)$ undefined, consistent with the requirement that if $k \le k′$ and $f(P,k)=$ true then $f(P,k′)=$ true also.
Say that:

> $k \Vdash P$ if and only if $f(P,k)=$ true.

To each node $k$ and each $(n+1)$-ary predicate letter $Q(\dots)$, assign a (possibly empty) set $T(Q,k)$ of $(n+1)$-tuples of elements of $D(k)$ in such a way that if $k \le k′$ then $T(Q,k) \subseteq T(Q,k′)$.
Say that:

> $k \Vdash Q(d0,\dots,dn)$ if and only if $(d0,\dots,dn) \in T(Q,k)$.

Now define $k \Vdash E$ (which may be read “ $k$ forces $E$ ”) for compound sentences $E$ of $L(k)$ inductively as follows:

$$
\begin{align*}
 k \Vdash (A \And B) & \text{ if } k \Vdash A \text{ and } k \Vdash B. \\
 k \Vdash (A \lor B) & \text{ if } k \Vdash A \text{ or } k \Vdash B. \\
 k \Vdash (A \to B) & \text{ if, for every } k' \ge k
 \text{ if } k \Vdash A \text{ then } k' \Vdash B. \\
 k \Vdash \lnot A & \text{ if for no } k' \ge k
 \text{ does } k' \Vdash A. \\
 k \Vdash \forall x A(x) & \text{ if for every } k' \ge k
 \text{ and every } d \in D(k'), k' \Vdash A(d). \\
 k \Vdash \exists x A(x) & \text{ if for some } d \in D(k), k \Vdash A(d).
\end{align*}
$$

Any such forcing relation is consistent:

> For no sentence $A$ and no $k$ is it the case that both $k \Vdash A$ and $k \Vdash \lnot A$.

and monotone:

If $k \le k′$ and $k \Vdash A$ then $k′ Vdash A$.

**Kripke’s Soundness and Completeness Theorems** establish that a sentence of $L$ is provable in intuitionistic predicate logic if and only if it is forced by every node of every Kripke structure.
Thus to show that $¬∀x¬P(x)→∃xP(x)$ is intuitionistically unprovable, it is enough to consider a Kripke structure with $K = \{k, k′\} , k < k′ , D(k) = D(k′) = {0} , T(P, k)$ empty but $T(P,k′) = \{ 0 \}$.
And to show the converse is intuitionistically provable (without actually exhibiting a proof), one only needs the consistency and monotonicity properties of arbitrary Kripke models, with the definition of $\Vdash$.

Kripke models for languages with equality may interpret $=$ at each node by an arbitrary equivalence relation, subject to monotonicity.
For applications to intuitionistic arithmetic, normal models (those in which equality is interpreted by identity at each node) suffice because equality of natural numbers is decidable.

Propositional Kripke semantics is particularly simple, since an arbitrary propositional formula is intuitionistically provable if and only if it is forced by the root of every Kripke model whose frame (the set $K$ of nodes together with their partial ordering) is a finite tree with a least element (the root).
For example, the Kripke model with $K = \{k, k′, k′′ \} , k < k′$ and $k < k′′$, and with $P$ true only at $k′$, shows that both $P \lor \lnot P$ and $\lnot P \lor \lor \lor P$ are unprovable in $\mathbf{IPC}$.

Each terminal node or leaf of a Kripke model is a classical model, because a leaf forces every formula or its negation.
Only those proposition letters which occur in a formula $E$, and only those nodes $k′$ such that $k \le k′$, are relevant to deciding whether or not $k$ forces $E$.
Such considerations allow us to associate effectively with each formula $E$ of $L(\mathbf{IPC})$ a finite class of finite Kripke structures which will include a countermodel to $E$ if one exists.
Since the class of all theorems of $\mathbf{IPC}$ is recursively enumerable, we conclude that:

> $\mathbf{IPC}$ is effectively decidable.
> There is a recursive procedure which determines, for each propositional formula $E$, whether or not $E$ is a theorem of $\mathbf{IPC}$, concluding with either a proof of $E$ or a (finite) Kripke countermodel.

The decidability of $\mathbf{IPC}$ was first obtained by Gentzen in 1935.
The undecidability of $\mathbf{IQC}$ follows from the undecidability of $\mathbf{CQC}$ by the negative interpretation.

Familiar non-intuitionistic logical schemata correspond to structural properties of Kripke models, for example:

- DNS holds in every Kripke model with finite frame.

- $(A \to B) \lor (B \to A)$ holds in every Kripke model with linearly ordered frame. Conversely, every propositional formula which is not derivable in $\mathbf{IPC} + (A \to B) \lor (B \to A)$ has a Kripke countermodel with linearly ordered frame (cf. Section 6.1 below).

- If $x$ is not free in $A$ then $\forall x(A \lor B(x)) \to (A \lor \forall x B(x))$ holds in every Kripke model $\mathbf{K}$ with constant domain (so that $D(k) = D(k′)$ for all $k,k′$ in $K$). The same is true for MP.

**Beth’s semantic tableaux,** inspired by Brouwer’s notion of spread, predated Kripke’s semantics; Troelstra and van Ulsen give an authoritative account of the history.
For a modern version of Beth semantics which facilitates comparison with Kripke semantics, a Beth structure is a Kripke structure in which the partially ordered set $K$ is a rooted tree with $k_0$ as the root, and the forcing conditions in a Beth model are the same as those in a Kripke model with two exceptions.
The forcing conditions for $(A \lor B)$ and $\exists x A(x)$ in a Beth model are as follows, where a branch of $K$ is a maximal linearly ordered subset $k0 \le k1 \le k2 \le \dots$ of $K$.

> $k \Vdash (A∨B)$ if every branch of $K$ passing through $k$ contains a node $k′ \ge k$ such that $k′ \Vdash A$ or $k′ \Vdash B$.

> $k \Vdash \exist x A(x)$ if every branch of $K$ passing through $k$ contains a node $k′ \ge k$ such that $k′ \Vdash A(d)$ for some for some $d \in D(k′)$.

To use a temporal analogy, a Beth model allows a decision between two alternatives, or the production of a witness to an existential statement, to be postponed until more information and possibly more individuals are available.
A Kripke model demands an immediate decision between two alternatives, or the immediate choice of a witness to an existential statement from the current domain of individuals.

Kripke models and Beth models are powerful tools for establishing properties of intuitionistic formal systems; cf.
Troelstra and van Dalen [1988], Smorynski [1973], de Jongh and Smorynski [1976], Ghilardi [1999] and Iemhoff [2001], [2005].
However, there is no purely intuitionistic proof that every sentence which is valid in all Kripke and Beth models is provable in $\mathbf{IQC}$. Following an observation by Gödel, Kreisel [1958] verified that the completeness of intuitionistic predicate logic for Beth semantics is equivalent to Markov’s Principle MP, which Brouwer rejected.

Moreover, Dyson and Kreisel [1961] showed that if $\mathbf{IQC}$ is weakly complete for Beth semantics (that is, if no unprovable sentence holds in every Beth model) then the following consequence of MP holds :

$$
\tag{GDK}
\forall \alpha_{B(\alpha)} \lnot \lnot \exists x R(\alpha, x)
\to
\lnot \lnot \forall \alpha_{B(\alpha)} \exists x R(\alpha, x),
$$

where $x$ ranges over all natural numbers, $\alpha$ ranges over all infinite sequences of natural numbers, $B(α)$ abbreviates $∀x(α(x)≤1)$, and $R$ expresses a primitive recursive relation of $\alpha$ and $x$.
Conversely, GDK entails the weak completeness of $\mathbf{IQC}$.
This interesting principle, considered as a schema with $R$ required to be quantifier-free, would justify the negative interpretation of a form of Brouwer’s Fan Theorem.
It is weaker than MP but unprovable in current systems of intuitionistic analysis.
Kreisel [1962] suggested that GDK may eventually be provable on the basis of as yet undiscovered properties of intuitionistic mathematics.

By modifying the definition of a Kripke model to allow “exploding nodes” which force every sentence, Veldman [1976] and de Swart [1976] independently found completeness proofs using only intuitionistic logic.
However, Veldman questioned whether Kripke models with exploding nodes were intuitionistically meaningful mathematical objects.

### 5.2 Realizability semantics for Heyting arithmetic

One way to implement the B-H-K explanation of intuitionistic truth for arithmetic is to associate with each sentence $E$ of $\mathbf{HA}$ some collection of numerical codes for algorithms which could establish the constructive truth of $E$.
Following Kleene [1945], a number e realizes a sentence $E$ of the language of arithmetic by induction on the logical form of $E$ :

> $e$ realizes $r = t$ if $r = t$ is true.

> $e$ realizes $A \And B$ if $e$ codes a pair $(f, g)$ such that $f$ realizes $A$ and $g$ realizes $B$.

> $e$ realizes $A \lor B$ if $e$ codes a pair $(f, g)$ such that if $f = 0$ then $g$ realizes A, and if $f > 0$ then $g$ realizes $B$.

> $e$ realizes $A \to B$ if, whenever $f$ realizes $A$, then the $e$th partial recursive function is defined at $f$ and its value realizes $B$.

> $e$ realizes $\lnot A$ if no $f$ realizes $A$.

> $e$ realizes $\forall x A(x)$ if, for every $n$, the $e$th partial recursive function is defined at $n$ and its value realizes $A(n)$.

> $e$ realizes $\exists x A(x)$ if $e$ codes a pair $(n, g)$ and g realizes $A(n)$.

An arbitrary formula is realizable if some number realizes its universal closure.
Observe that not both $A$ and $\lnot A$ are realizable, for any formula $A$.
The fundamental result is:

> Nelson’s Theorem [1947]
>
> If $A$ is derivable in $\mathbf{HA}$ from realizable formulas $F$, then $A$ is realizable.

Some nonintuitionistic principles can be shown to be realizable.
For example, Markov’s Principle (for decidable formulas) can be expressed by the schema

$$
\tag{MP}

\forall x
(A(x) \lor \lnot A(x)) \And \lnot \forall x \lnot A(x)
\to \exists x A(x).
$$

Although unprovable in $\mathbf{HA}$, MP is realizable by an argument which uses Markov’s Principle informally.
But realizability is a fundamentally nonclassical interpretation.
In $\mathbf{HA}$ it is possible to express an axiom of recursive choice CT (for “Church’s Thesis”), which contradicts LEM but is (constructively) realizable.
Hence by Nelson’s Theorem, $\mathbf{HA}$ + MP + CT is consistent.

Kleene used a variant of number-realizability to prove $\mathbf{HA}$ satisfies the Church-Kleene Rule; the same argument works for $\mathbf{HA}$ with MP or CT, and for $\mathbf{HA}$ + MP + CT.
In Kleene and Vesley [1965] and Kleene [1969], functions replace numbers as realizing objects, establishing the consistency of formalized intuitionistic analysis and its closure under a second-order version of the Church-Kleene Rule.

Nelson’s Theorem establishes the unprovability in $\mathbf{IQC}$ of some theorems of classical predicate logic.
If, to each n-place predicate letter $P(\dots)$, a formula $f(P)$ of $L(\mathbf{HA})$ with n free variables is assigned, and if the formula $f(A)$ of $L(\mathbf{HA})$ comes from the formula $A$ of $L$ by replacing each prime formula $P(x_1, \dots, x_n)$ by $f(P)(x_1, \dots, x_n)$, then $f(A)$ is called an arithmetical substitution instance of $A$.
As an example, if a formula of $L(\mathbf{HA})$ expressing “$y$ is the code of a sentence and x codes a proof in $\mathbf{HA}$ of the sentence with code $y$” is assigned to $P(x,y)$, then (assuming $\mathbf{HA}$ is consistent) the resulting arithmetical substitution instance of $\forall y (\exists x P(x, y) \lor \lnot \exists x P(x, y))$ is unrealizable and hence unprovable in $\mathbf{HA}$, and so is its double negation.
It follows that $\lnot \lnot \forall y (\exists x P(x, y) \lor \lnot \exists x P(x, y))$ is not provable in $\mathbf{IQC}$.

De Jongh [1970] combined realizability with Kripke modeling to show that intuitionistic propositional logic $\mathbf{IPC}$ and a fragment of $\mathbf{IQC}$ are arithmetically complete for $\mathbf{HA}$.
A uniform assignment of simple existential formulas to predicate letters suffices to prove:

> **De Jongh’s Theorem (for IPC) [1970]**
> If a propositional formula $A$ of the language $L$ is not provable in $\mathbf{IPC}$, then some arithmetical substitution instance of $A$ is not provable in $\mathbf{HA}$.

The proof of this version of de Jongh’s Theorem does not need realizability; cf.
Smorynski [1973]. As an example, Rosser’s form of Gödel’s Incompleteness Theorem provides a sentence $C$ of $L(\mathbf{HA})$ such that $\mathbf{PA}$ proves neither $C$ nor $\lnot C$, so by the disjunction property $\mathbf{HA}$ cannot prove $(C \lor \lnot C)$.
But de Jongh’s semantical proof also established that every intuitionistically unprovable predicate formula of a restricted kind has an arithmetical substitution instance which is unprovable in $\mathbf{HA}$.
Using a syntactic method, Daniel Leivant [1979] extended de Jongh’s Theorem to all intuitionistically unprovable predicate formulas, proving that $\mathbf{IQC}$ is arithmetically complete for $\mathbf{HA}$.
See van Oosten [1991] for a historical exposition and a simpler proof of the full theorem, using abstract realizability with Beth models instead of Kripke models.

Without claiming that number-realizability coincides with intuitionistic arithmetical truth, Nelson observed that for each formula $A$ of $L(\mathbf{HA})$ the predicate “$y$ realizes $A$” can be expressed in $\mathbf{HA}$ by another formula (abbreviated “$y \text{ re } A$”), and the schema $A \leftrightarrow \exists y (y \text{ re } A)$ is consistent with $\mathbf{HA}$. Troelstra [1973] showed that (A↔∃y(yreA)) is equivalent over $\mathbf{HA}$ to “extended Church’s Thesis” ECT, a stronger version of CT enabling recursive choice under assumptions which are “almost negative” (containing no $\lor$, and with $\exists x$ only applied to prime formulas). While $\mathbf{HA}$ is sound but not complete for Kleene’s number-realizability, the next theorem shows that$\mathbf{HA}$ + ECT is both sound and complete for this interpretation.

> **Troelstra’s Characterization Theorem (for number-realizability over $\mathbf{HA}$) [1973]**
> If $A$ is a closed formula of the language $L(\mathbf{HA})$, then:
> 1. $\mathbf{HA}$ + ECT $\vdash (A \leftrightarrow \exists y (y \text{ re } A))$.
> 2. $\mathbf{HA}$ + ECT $\vdash A$ if and only if $\mathbf{HA}$ $\vdash$ $\exists y (y \text{ re } A)$.

In $\mathbf{HA}$ + MP + ECT, which Troelstra considers to be a formalization of Russian recursive mathematics (cf. section 3.2 of the entry on constructive mathematics), every formula of the form $(y \text{ re } A)$ has an equivalent “classical” prenex form $A′(y)$ consisting of a quantifier-free subformula preceded by alternating “classical” quantifiers of the forms $\lnot \lnot \exists x$ and $\forall z \lnot \lnot$, and so $\exists y A′(y)$ is a kind of prenex form of $A$.

## 6. Additional Topics and Further Reading

### 6.1 Subintuitionistic and Intermediate Logics

At present there are several other entries in this encyclopedia treating intuitionistic logic in various contexts, but a general treatment of weaker and stronger propositional and predicate logics appears to be lacking.
Many such logics have been identified and studied.
Here are a few examples.

A subintuitionistic propositional logic can be obtained from$\mathbf{IPC}$ by restricting the language, or weakening the logic, or both. An extreme example of the first is $\mathbf{RN}$, intuitionistic logic with a single propositional variable P, which is named after its discoverers Rieger and Nishimura [1960]. $\mathbf{RN}$ is characterized by the Rieger-Nishimura lattice of infinitely many nonequivalent formulas $F_n$ such that every formula whose only propositional variable is $P$ is equivalent by intuitionistic logic to some $F_n$. Nishimura’s version is

$$
\begin{align*}
F_{\infty} &= P \to P. \\
F_0 &= P \And \lnot P. \\
F_1 &= P. \\
F_2 &= \lnot P.\\
F_{2 n + 3} &= F_{2 n + 1} \lor F_{ 2n + 2}. \\
F_{2 n + 4} &= F_{2 n + 3} \to F_{2 n + 1}.
\end{align*}
$$

In $\mathbf{RN}$ neither $F_{2n+1}$ nor $F_{2n+2}$ implies the other; but $F_{2n}$ implies $F_{2n+1}$, and $F_{2n+1}$ implies each of $F_{2n+3}$ and $F_{2n+4}$.

Fragments of $\mathbf{IPC}$ missing one or more logical connectives restrict the language and incidentally the logic, since the intuitionistic connectives $\And$, $\lor$, $\to$, $\lnot$ are logically independent over $\mathbf{IPC}$.
Rose [1953] proved that the implicationless fragment (without →) is complete with respect to realizability, in the sense that if every arithmetical substitution instance of a propositional formula $E$ without → is (number)-realizable then $E$ is a theorem of $\mathbf{IPC}$.
This result contrasts with:

> **Rose’s Theorem [1953]**
> $\mathbf{IPC}$ is incomplete with respect to realizability.

Let $F$ be the propositional formula

$$
(( \lnot \lnot D \to D)
\to ( \lnot \lnot D \lor \lnot D))
\to ( \lnot \lnot D \lor \lnot D)
$$

where $D$ is $(\lnot P \lor \lnot Q)$ and $P$, $Q$ are prime. Every arithmetical substitution instance of $F$ is realizable (using classical logic), but $F$ is not provable in $\mathbf{IPC}$.

It follows that $\mathbf{IPC}$ is arithmetically incomplete for $\mathbf{HA}$ + ECT (cf. Section 5.2).

Minimal logic $\mathbf{ML}$ comes from intuitionistic logic by deleting ex falso.
Kolmogorov [1925] showed that this fragment already contains a negative interpretation of classical logic retaining both quantifiers, cf.
Leivant [1985]. Minimal logic does prove the special case $ \lnot A \to (A \to \lnot B)$ of ex falso for negations.
Colacito, de Jongh and Vardas [2017] study various subminimal logics, each weaker than $\mathbf{ML}$.

Griss contested Brouwer’s use of negation, objecting to both the law of contradiction and ex falso.
It is worth noting that negation is not really needed for intuitionistic mathematics since $0 = 1$ is a known contradiction so $\lnot A$ can be defined by $A \to 0 = 1$.
Then ex falso can be stated as $0 = 1 \to A$, and the law of contradiction is provable from the remaining axioms of $H$.

An intermediate propositional logic is any consistent collection of propositional formulas containing all the axioms of $\mathbf{IPC}$ and closed under modus ponens and substitution of arbitrary formulas for proposition letters.
Each intermediate propositional logic is contained in $\mathbf{CPC}$.
Some particular intermediate propositional logics, characterized by adding one or more classically correct but intuitionistically unprovable axiom schemas to $\mathbf{IPC}$, have been studied extensively.

One of the simplest intermediate propositional logics is the Gödel-Dummett logic $\mathbf{LC}$, obtained by adding to $\mathbf{IPC}$ the schema $(A \to B)∨(B \to A)$ which is valid on all and only those Kripke frames in which the partial order of the nodes is linear.
Gödel [1932] used an infinite sequence of successively stronger intermediate logics to show that $\mathbf{IPC}$ has no finite truth-table interpretation.
For each positive integer n, let $G_n$ be $\mathbf{LC}$ plus the schema $(A_1 \to A_2) \lor \dots \lor (A_1 \And \dots \And A_n→A_{n+1})$.
Then $G_n$ is valid on all and only those linearly ordered Kripke frames with no more than $n$ nodes.

The Jankov logic $\mathbf{KC}$, which adds to $\mathbf{IPC}$ the principle of testability $\lnot A \lor \lnot \lnot A$, obviously does not have the disjunction property.
The Kreisel-Putnam logic $\mathbf{KP}$, obtained by adding to $\mathbf{IPC}$ the schema $(\lnot A \to (B \lor C)) \to ((\lnot A \to B) \lor (\lnot A \to C))$, has the disjunction property but does not satisfy all the Visser rules.
The intermediate logic obtained by adding the schema

$$
((\lnot \lnot D \to D) \to(D \lor \lnot D))
\to (\lnot \lnot D \lor \lnot D),
$$

corresponding to Rose’s counterexample, to $\mathbf{IPC}$ also has the disjunction property.
Iemhoff [2005] proved that $\mathbf{IPC}$ is the only intermediate propositional logic with the disjunction property which is closed under all the Visser rules.
Iemhoff and Metcalfe [2009] developed a formal calculus for generalized admissibility for $\mathbf{IPC}$ and some intermediate logics.
Goudsmit [2015] is a thorough study of the admissible rules of intermediate logics, with a comprehensive bibliography.

An intermediate propositional logic $\mathbf{L}$ is said to have the finite frame property if there is a class of finite frames on which the Kripke-valid formulas are exactly the theorems of $\mathbf{L}$.
Many intermediate logics, including $\mathbf{LC}$ and $\mathbf{KP}$, have this property.
Jankov [1968] used an infinite sequence of finite rooted Kripke frames to prove that there are continuum many intermediate logics.
De Jongh, Verbrugge and Visser [2009] proved that every intermediate logic $\mathbf{L}$ with the finite frame property is the propositional logic of $\mathbf{HA(L)}$, that is, the class of all formulas in the language of $\mathbf{IPC}$ all of whose arithmetical substitution instances are provable in the logical extension of $\mathbf{HA}$ by $\mathbf{L}$.

An intermediate propositional logic $\mathbf{L}$ is structurally complete if every rule which is admissible for $\mathbf{L}$ is derivable in $\mathbf{L}$, and hereditarily structurally complete if every intermediate logic extending $\mathbf{L}$ is also structurally complete. Every intermediate logic $\mathbf{L}$ has a structural completion $\mathbf{\overline{L}}$, obtained by adjoining all its admissible rules. $\mathbf{LC}$ and $\mathbf{G_n}$ are hereditarily structurally complete. While $\mathbf{IPC}$, $\mathbf{RN}$ and $\mathbf{KC}$ are not structurally complete, their structural completions are hereditarily structurally complete. For these results and more, see Citkin [2016, Other Internet Resources].

Some intermediate predicate logics, extending $\mathbf{IQC}$ and closed under substitution, are $\mathbf{IQC}$ + DNS (Section 4.1), $\mathbf{IQC}$ + MP (cf. Section 5.2), $\mathbf{IQC}$ + MP + IP (cf. Section 4.2), and the intuitionistic logic of constant domains $\mathbf{CD}$ obtained by adding to $\mathbf{IQC}$ the schema $\forall x (A \lor B(x)) \to (A \lor \forall x B(x))$ for all formulas $A, B(x)$ with $x$ not occurring free in $A$.
Mints, Olkhovikov and Urquhart [2013] showed that $CD$ does not have the interpolation property, refuting earlier published proofs by other authors.

### 6.2 Basic Intuitionistic Modal Logic

This section, at present, offers only a glimpse of intuitionistic modal logic. Any classical [modal logic](https://plato.stanford.edu/entries/logic-modal/) has an intuitionistic companion defined by replacing the underlying classical propositional or predicate logic by the corresponding intuitionistic propositional or predicate logic. Simpson [1994] and Plotkin and Stirling [1986] provide a general framework for intuitionistic modal logics which is adaptable to a multitude of uses.

The basic intuitionistic modal propositional logic $\mathbf{iK}$ has as axioms:

- all propositional axioms of intuitionistic logic in the modal language with logical connectives $\land,\lor,\to,\leftrightarrow,\lnot,$ logical constants $\top$ and $\bot$, and a unary operator $\Box$ (necessity), and

- all substitution instances of Kripke’s distributive schema $\Box (A \to B) \to (\Box A \to \Box B)$;

and as rules of inference all substitution instances of:

- modus ponens: from $A$ and $(A \to B)$, infer $B$, and

- necessitation: from $A$ infer $\Box A$.

$\mathbf{iL}$ adds to $\mathbf{iK}$ the Löb axiom schema $\Box (\Box A \to A)\to A$.

$\mathbf{iK4}$ adds to $\mathbf{iL}$ the transitive axiom schema $\Box A \to \Box \Box A$.

The truth axiom schema T: $\Box A \to A$ can be added to any of these.

An additional modality $\Diamond$ can be taken as primitive, or defined by $\Diamond A \leftrightarrow \lnot \Box \lnot A$, depending on context.

## 6.3 Advanced topics

Brouwer’s influence on Gödel was significant, although Gödel never became an intuitionist. Gödel’s [1933f] translation of intuitionistic propositional logic into the [modal logic](https://plato.stanford.edu/entries/logic-modal/) $\mathbf{S4}$ is described in Section 2.5 of the entry on Gödel and in Troelstra’s introductory note to the translation of [1933f] in Volume I of Gödel’s Collected Works. See also Mints [2012]. Kripke models for modal logic predated those for intuitionistic logic.

Alternatives to Kripke and Beth semantics for intuitionistic propositional and predicate logic include the topological interpretation of Stone [1937], Tarski [1938] and Mostowski [1948] (cf. Rasiowa and Sikorski [1963], Rasiowa [1974]), which was extended to intuitionistic analysis by Scott [1968] and Krol [1978]. M. Hyland [1982] defined the effective topos Eff and proved that its logic is intuitionistic. For a very informative discussion of semantics for intuitionistic logic and mathematics by W. Ruitenberg, and an interesting new perspective by G. Bezhanishvili and W. Holliday, see Other Internet Resources (below).

One alternative to realizability semantics for intuitionistic arithmetic is Gödel’s [1958] “Dialectica” interpretation, which associates with each formula $B$ of $L(\mathbf{HA})$ a quantifier-free formula $B_D$ in the language of intuitionistic arithmetic of all finite types. The “Dialectica” interpretation of $B$, call it $B_D$, is $\exists Y \forall x B_D(Y, x)$. If $B$ is a closed theorem of $\mathbf{HA}$, then $B_D(F, x)$ is provable for some term $F$ in Gödel’s theory $T$ of “primitive recursive” functionals of higher type. The translation from $B$ to $B^D$ requires the axiom of choice (at all finite types), MP and IP, so is not strictly constructive; however, the number-theoretic functions expressible by terms $F$ of $T$ are precisely the provably recursive functions of $\mathbf{HA}$ (and of $\mathbf{PA}$).
The interpretation was extended to analysis by Spector [1962]; cf. Howard [1973]. Clear expositions, and additional references, are to be found in Troelstra’s introduction to the English translation in Gödel [1990] of the original Dialectica article, in Avigad and Feferman [1998], and in Ferreira [2008].

While $\mathbf{HA}$ is a proper part of classical arithmetic, the intuitionistic attitude toward mathematical objects results in a theory of real numbers (cf. sections 3.4–3.7 of the entry on [intuitionism in the philosophy of mathematics](https://plato.stanford.edu/entries/intuitionism/)) diverging from the classical.
Kleene’s function-realizability interpretation, developed to prove the consistency of his formalization $\mathbf{FIM}$ of the intuitionistic theory of sequences (“intuitionistic analysis”), changes the interpretation of arithmetical formulas; for example, $\lnot \lnot \forall x(A(x) \lor \lnot A(x))$ is function-realizable for every arithmetical formula $A(x)$.
In the language of analysis, Markov’s Principle and the negative translation of the countable axiom of choice are among the many non-intuitionistic principles which are function-realizable (by classical arguments) and hence consistent with $\mathbf{FIM}$; cf. Kleene [1965], Vesley [1972] and Moschovakis [2003].

Concrete and abstract realizability semantics for a wide variety of formal systems have been developed and studied by logicians and computer scientists; cf. Troelstra [1998] and van Oosten [2002] and [2008]. Variations of the basic notions are especially useful for establishing relative consistency and relative independence of the nonlogical axioms in theories based on intuitionistic logic; some examples are Moschovakis [1971], Lifschitz [1979], and the realizability notions for constructive and intuitionistic set theories developed by Rathjen [2006, 2012] and Chen [2012]. Early abstract realizability notions include the slashes of Kleene [1962, 1963] and Aczel [1968], and Läuchli [1970]. Kohlenbach, Avigad and others have developed realizability interpretations for parts of classical mathematics.

Artemov’s [justification logic](https://plato.stanford.edu/entries/logic-justification/) is an alternative interpretation of the B-H-K explanation of the intuitionistic connectives and quantifiers, with (idealized) proofs playing the part of realizing objects.
See also Artemov and Iemhoff [2007].

Another line of research in intuitionistic logic concerns Brouwer’s controversial “creating subject counterexamples” to principles of classical analysis (such as Markov’s Principle) which could not be refuted on the basis of the theory $\mathbf{FIM}$ of Kleene and Vesley [1965]. By weakening Kleene’s strong form of Brouwer’s principle of continuous choice, and adding an axiom he called Kripke’s Schema (KP), Myhill [1967] formalized Brouwer’s creating subject arguments in the language of intuitionistic analysis.
Krol [1978] and Scowcroft gave topological consistency proofs for intuitionistic analysis with Kripke’s Schema and weak continuity.
Kripke himself preferred Weak Kripke’s Schema (WKP), which still conflicts with strong continuous choice.
Kripke [2019] and Brauer, Linnebo and Shapiro [2022] recently provided an attractive modal interpretation of Brouwer’s theory of the creating subject.

Vesley [1970] found an alternative principle (Vesley’s Schema VS) which can consistently be added to $\mathbf{FIM}$ and implies all the counterexamples for which Brouwer required a creating subject.
Troelstra’s generalized continuous choice (GC), which characterizes Kleene’s function-realizability just as his ECT characterizes number-realizability, and Vesley’s VS express two incompatible possible extensions of intuitionistic analysis, with different mathematical properties.

Constructive mathematicians, following Bishop, traditionally assume intuitionistic logic and work with strong definitions of concepts.
For example, they equate “there is at most one number $n$ such that $P(n)$” with “if $n$ and $m$ are distinct numbers then not $P(n)$ or not $P(m)$,” rather than the more natural “if $n$ and $m$ are numbers such that $P(n)$ and $P(m)$ then $n = m$”.
Shulman [2022] suggests that an “affine” logic of proof and refutation, with additional connectives and an antithesis translation into intuitionistic logic, would be more useful for constructive mathematics.

## 6.4 Recommended reading

The entry on L. E. J. Brouwer discusses Brouwer’s philosophy and mathematics, with a chronology of his life and a selected list of publications including translations and secondary sources.
The best way to learn more is to read some of the original papers.
English translations of Brouwer’s doctoral dissertation and other papers which originally appeared in Dutch, along with a number of articles in German, can be found in L. E. J. Brouwer: Collected Works [1975], edited by Heyting.
Benacerraf and Putnam’s essential source book contains Brouwer [1912] (in English translation), Brouwer [1949] and Dummett [1975]. Mancosu’s [1998] provides English translations of many fundamental articles by Brouwer, Heyting, Glivenko and Kolmogorov, with illuminating introductory material by W. van Stigt whose [1990] is another valuable resource.

A delightful, accessible and authoritative introduction to intuitionistic mathematics and logic is Wim Veldman’s [2021]. The third edition [1971] of Heyting’s classic [1956] is an attractive introduction to intuitionistic philosophy, logic and mathematical practice.
As part of the formidable project of editing and publishing Brouwer’s Nachlass, van Dalen [1981] provides a comprehensive view of Brouwer’s own intuitionistic philosophy.
The English translation, in van Heijenoort [1969], of Brouwer’s [1927] (with a fine introduction by Parsons) is still an indispensable reference for Brouwer’s theory of the continuum.
Veldman [1990] and [2005] are authentic modern examples of traditional intuitionistic mathematical practice.
Troelstra [1991] places intuitionistic logic in its historical context as the common foundation of constructive mathematics in the twentieth century.
Bezhanishvili and de Jongh [2005, Other Internet Resources] includes recent developments in intuitionistic logic.

Kleene and Vesley’s [1965] gives a careful axiomatic treatment of intuitionistic analysis, a proof of its consistency relative to a classically correct subtheory, and an extended application to Brouwer’s theory of real number generators.
Kleene’s [1969] formalizes the theory of partial recursive functionals, enabling precise formalizations of the function-realizability interpretation used in [1965] and of a related q-realizability interpretation which gives the Church-Kleene Rule for intuitionistic analysis.

Troelstra’s [1973], Beeson’s [1985] and Troelstra and van Dalen’s [1988] (with corrections) stand out as the most comprehensive studies of intuitionistic and semi-intuitionistic formal theories, using both constructive and classical methods, with useful bibliographies.
Troelstra and Schwichtenberg [2000] presents the proof theory of classical, intuitionistic and minimal logic in parallel, focusing on sequent systems.
Troelstra’s [1998] presents formulas-as-types and (Kleene and Aczel) slash interpretations for propositional and predicate logic, as well as abstract and concrete realizabilities for a multitude of applications.
Martin-Löf’s constructive theory of types [1984] (cf. Section 3.4 of the entry on constructive mathematics) provides another general framework within which intuitionistic reasoning continues to develop.
