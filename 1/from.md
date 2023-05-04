# Intuitionistic Type Theory

> [From](https://plato.stanford.edu/entries/type-theory-intuitionistic/)
> 
> First published Fri Feb 12, 2016; substantive revision Mon Jun 8, 2020

Intuitionistic type theory (also constructive type theory or Martin-Löf type theory) is a formal logical system and philosophical foundation for constructive mathematics.
It is a full-scale system which aims to play a similar role for constructive mathematics as Zermelo-Fraenkel Set Theory does for classical mathematics.
It is based on the propositions-as-types principle and clarifies the Brouwer-Heyting-Kolmogorov interpretation of intuitionistic logic.
It extends this interpretation to the more general setting of intuitionistic type theory and thus provides a general conception not only of what a constructive proof is, but also of what a constructive mathematical object is.
The main idea is that mathematical concepts such as elements, sets and functions are explained in terms of concepts from programming such as data structures, data types and programs.
This article describes the formal system of intuitionistic type theory and its semantic foundations.

In this entry, we first give an overview of the most important aspects of intuitionistic type theory—a kind of “extended abstract”.
It is meant for a reader who is already somewhat familiar with the theory.
Section 2 on the other hand, is meant for a reader who is new to intuitionistic type theory but familiar with traditional logic, including propositional and predicate logic, arithmetic, and set theory.
Here we informally introduce several aspects which distinguishes intuitionistic type theory from these traditional theories.
In Section 3 we present a basic version of the theory, close to Martin-Löf’s first published version from 1972.
The reader who was intrigued by the informality of Section 2 will now see in detail how the theory is built up.
Section 4 then presents a number of important extensions of the basic theory.
In particular, it emphasizes the central role of inductive (and inductive-recursive) definitions.
Section 5 introduces the underlying philosophical ideas including the theory of meaning developed by Martin-Löf.
While Section 5 is about philosophy and foundations, Section 6 gives an overview of mathematical models of the theory.
In Section 7 finally, we describe several important variations of the core Martin-Löf “intensional” theory described in Section 3 and 4.

## 1.Overview

We begin with a bird’s eye view of some important aspects of intuitionistic type theory.
Readers who are unfamiliar with the theory may prefer to skip it on a first reading.

The origins of intuitionistic type theory are Brouwer’s intuitionism and Russell’s type theory.
Like Church’s classical simple theory of types it is based on the lambda calculus with types,
but differs from it in that it is based on the propositions-as-types principle,
discovered by Curry (1958) for propositional logic and extended to predicate logic by Howard (1980) and de Bruijn (1970).
This extension was made possible by the introduction of indexed families of types (dependent types) for representing the predicates of predicate logic.
In this way all logical connectives and quantifiers can be interpreted by type formers.
In intuitionistic type theory further types are added,
such as a type of natural numbers, a type of small types (a universe) and a type of well-founded trees.
The resulting theory contains intuitionistic number theory (Heyting arithmetic) and much more.

The theory is formulated in natural deduction where the rules for each type former are classified as formation, introduction, elimination, and equality rules.
These rules exhibit certain symmerties between the introduction and elimination rules following Gentzen’s and Prawitz’ treatment of natural deduction, as explained in the entry on proof-theoretic semantics.

The elements of propositions, when interpreted as types, are called proof-objects.
When proof-objects are added to the natural deduction calculus it becomes a typed lambda calculus with dependent types, which extends Church’s original typed lambda calculus.
The equality rules are computation rules for the terms of this calculus.
Each function definable in the theory is total and computable.
Intuitionistic type theory is thus a typed functional programming language with the unusual property that all programs terminate.

Intuitionistic type theory is not only a formal logical system but also provides a comprehensive philosophical framework for intuitionism.
It is an interpreted language, where the distinction between the demonstration of a judgment and the proof of a proposition plays a fundamental role (Sundholm 2012).
The framework clarifies the Brouwer-Heyting-Kolmogorov interpretation of intuitionistic logic and extends it to the more general setting of intuitionistic type theory.
In doing so it provides a general conception not only of what a constructive proof is, but also of what a constructive mathematical object is.
The meaning of the judgments of intuitionistic type theory is explained in terms of computations of the canonical forms of types and terms.
These informal, intuitive meaning explanations are “pre-mathematical” and should be contrasted to formal mathematical models developed inside a standard mathematical framework such as set theory.

This meaning theory also justifies a variety of inductive, recursive, and inductive-recursive definitions.
Although proof-theoretically strong notions can be justified, such as analogues of certain large cardinals, the system is considered predicative.
Impredicative definitions of the kind found in higher-order logic, intuitionistic set theory, and topos theory are not part of the theory.
Neither is Markov’s principle, and thus the theory is distinct from Russian constructivism.

An alternative formal logical system for predicative constructive mathematics is Myhill and Aczel’s constructive Zermelo-Fraenkel set theory (CZF).
This theory, which is based on intuitionistic first-order predicate logic and weakens some of the axioms of classical Zermelo-Fraenkel Set Theory, has a natural interpretation in intuitionistic type theory.
Martin-Löf’s meaning explanations thus also indirectly form a basis for CZF.

Variants of intuitionistic type theory underlie several widely used proof assistants, including NuPRL, Coq, and Agda.
These proof assistants are computer systems that have been used for formalizing large and complex proofs of mathematical theorems, such as the Four Colour Theorem in graph theory and the Feit-Thompson Theorem in finite group theory.
They have also been used to prove the correctness of a realistic C compiler (Leroy 2009) and other computer software.

Philosophically and practically, intuitionistic type theory is a foundational framework where constructive mathematics and computer programming are, in a deep sense, the same.
This point has been emphasized by (Gonthier 2008) in the paper in which he describes his proof of the Four Colour Theorem:

```
The approach that proved successful for this proof was to turn almost every mathematical concept into a data structure or a program in the Coq system, thereby converting the entire enterprise into one of program verification.
```

## 2. Propositions as Types

### 2.1 Intuitionistic Type Theory: a New Way of Looking at Logic?

Intuitionistic type theory offers a new way of analyzing logic, mainly through its introduction of explicit proof objects.
This provides a direct computational interpretation of logic, since there are computation rules for proof objects.
As regards expressive power, intuitionistic type theory may be considered as an extension of first-order logic, much as higher order logic, but predicative.

#### 2.1.1 A Type Theory

Russell developed type theory in response to his discovery of a paradox in naive set theory.
In his ramified type theory mathematical objects are classified according to their types: the type of propositions, the type of objects, the type of properties of objects, etc.
When Church developed his simple theory of types on the basis of a typed version of his lambda calculus he added the rule that there is a type of functions between any two types of the theory.
Intuitionistic type theory further extends the simply typed lambda calculus with dependent types, that is, indexed families of types.
An example is the family of types of $n$-tuples indexed by $n$.

Types have been widely used in programming for a long time.
Early high-level programming languages introduced types of integers and floating point numbers.
Modern programming languages often have rich type systems with many constructs for forming new types.
Intuitionistic type theory is a functional programming language where the type system is so rich that practically any conceivable property of a program can be expressed as a type.
Types can thus be used as specifications of the task of a program.

#### 2.1.2 An intuitionstic logic with proof-objects

Brouwer’s analysis of logic led him to an intuitionistic logic which rejects the law of excluded middle and the law of double negation.
These laws are not valid in intuitionistic type theory.
Thus it does not contain classical (Peano) arithmetic but only intuitionistic (Heyting) arithmetic.
(It is another matter that Peano arithmetic can be interpreted in Heyting arithmetic by the double negation interpretation, see the entry on intuitionistic logic.)

Consider a theorem of intuitionistic arithmetic, such as the division theorem

$$
\forall m , n . m > 0
\supset
\exists q , r . mq + r = n \land m > r
$$

A formal proof (in the usual sense) of this theorem is a sequence (or tree) of formulas, where the last (root) formula is the theorem and each formula in the sequence is either an axiom (a leaf) or the result of applying an inference rule to some earlier (higher) formulas.

When the division theorem is proved in intuitionistic type theory, we do not only build a formal proof in the usual sense but also a construction (or proof-object) “$\rm{div}$” which witnesses the truth of the theorem. We write

$$
\def\N{\text{N}}

\text{div} : \forall m , n : \N .\ m > 0
\supset 
\exists q , r : \N .\ mq + r = n \land m > r
$$

to express that $\rm{div}$ is a proof-object for the division theorem, that is, an element of the type representing the division theorem.
When propositions are represented as types, the -quantifier is identified with the dependent function space former (or general cartesian product) $\Pi$ , the $\exists$-quantifier with the dependent pairs type former (or general disjoint sum) $\Sigma$ , conjunction $\land$ with cartesian product $\times$ , the identity relation = with the type former $\rm{I}$ of proof-objects of identities, and the greater than relation $>$ with the type former $\rm{GT}$ of proof-objects of greater-than statements.
Using “type-notation” we thus write

$$
\def\N{\text{N}}
\def\GT{\text{GT}}
\def\I{\text{I}}

\text{div} : \Pi m , n : \N .\ \GT(m, 0)
\to
\Sigma q , r : \N .\ \I(\N, mq + r, n) \times \GT(m, r)
$$

to express that the proof object “$\text{div}$” is a function which maps two numbers $m$ and $n$ and a proof-object $p$ witnessing that $m>0$ to a quadruple $(q,(r,(s,t)))$ , where $q$ is the quotient and $r$ is the remainder obtained when dividing $n$ by $m$ .
The third component $s$ is a proof-object witnessing the fact that $mq+r=n$ and the fourth component $t$ is a proof object witnessing $m>r$ .

Crucially, $\text{div}$ is not only a function in the classical sense; it is also a function in the intuitionistic sense, that is, a program which computes the output $(q,(r,(s,t)))$ when given $m$, $n$, $p$ as inputs.
This program is a term in a lambda calculus with special constants, that is, a program in a functional programming language.

#### 2.1.3 An extension of first-order predicate logic

Intuitionistic type theory can be considered as an extension of first-order logic, much as higher order logic is an extension of first order logic.
In higher order logic we find some individual domains which can be interpreted as any sets we like.
If there are relational constants in the signature these can be interpreted as any relations between the sets interpreting the individual domains.
On top of that we can quantify over relations, and over relations of relations, etc.
We can think of higher order logic as first-order logic equipped with a way of introducing new domains of quantification: if $S_1,\dots,S_n$
are domains of quantification $(S_1,\dots,S_n)$ then is a new domain of quantification consisting of all the n-ary relations between the domains $S_1,\dots,S_n$ . Higher order logic has a straightforward set-theoretic interpretation where $(S_1,\dots,S_n)$ is interpreted as the power set $P(A_1 \times\dots\times A_n)$ where $A_i$ is the interpretation of $S_i$ , for $i = 1 , \dots , n$ .
This is the kind of higher order logic or simple theory of types that Ramsey, Church and others introduced.

Intuitionistic type theory can be viewed in a similar way, only here the possibilities for introducing domains of quantification are richer, one can use $\Sigma,\Pi,+,\text{I}$ to construct new ones from old.
(Section 3.1; Martin-Löf 1998 [1972]).
Intuitionistic type theory has a straightforward set-theoretic interpretation as well, where $\Sigma$ , $\Pi$ etc are interpreted as the corresponding set-theoretic constructions; see below.
We can add to intuitionistic type theory unspecified individual domains just as in HOL.
These are interpreted as sets as for HOL.
Now we exhibit a difference from HOL: in intuitionistic type theory we can introduce unspecified family symbols.
We can introduce $T$ as a family of types over the individual domain $S$ :

$$
T(x) \text{ type } (x:S).
$$

If $S$ is interpreted as $A$ , $T$ can be interpreted as any family of sets indexed by $A$ .
As a non-mathematical example, we can render the binary relation loves between members of an individual domain of people as follows.
Introduce the binary family Loves over the domain People

$$
\def\loves{\text{Loves}}
\def\type{\text{ type }}
\def\people{\text{People}}

\loves(x, y) \type (x:\people, y:\people)
$$

The interpretation can be any family of sets $B_{x,y}$ ($x:A$, $y:A$). How does this cover the standard notion of relation? Suppose we have a binary relation $R$ on $A$ in the familiar set-theoretic sense. We can make a binary family corresponding to this as follows

$$
x = \begin{cases}
  \{ 0 \}       &\text{if } R(x,y) \text{ holds } \\
  \varnothing   &\text{if } R(x,y) \text{ is false }
\end{cases}
$$

Now clearly $B_{x,y}$ is nonempty if and only if $R(x,y)$ holds.
(We could have chosen any other element from our set theoretic universe than 0 to indicate truth.)
Thus from any relation we can construct a family whose truth of $x,y$ is equivalent to $B_{x,y}$ being non-empty.
Note that this interpretation does not care what the proof for $R(x,y)$ is, just that it holds.
Recall that intuitionistic type theory interprets propositions as types, so $p:\text{Loves(John, Mary)}$ means that $\text{Loves(John, Mary)}$ is true.

The interpretation of relations as families allows for keeping track of proofs or evidence that $R(x,y)$ holds, but we may also chose to ignore it.

In Montague semantics, higher order logic is used to give semantics of natural language (and examples as above).
Ranta (1994) introduced the idea to instead employ intuitionistic type theory to better capture sentence structure with the help of dependent types.

In contrast, how would the mathematical relation $>$ between natural numbers be handled in intuitionistic type theory? First of all we need a type of numbers $\text{N}$ .
We could in principle introduce an unspecified individual domain $\text{N}$ , and then add axioms just as we do in first-order logic when we set up the axiom system for Peano arithmetic.
However this would not give us the desirable computational interpretation.
So as explained below we lay down introduction rules for constructing new natural numbers in $\text{N}$ and elimination and computation rules for defining functions on $\text{N}$ (by recursion).
The standard order relation $>$ should satisfy

$$
x > y \text{ iff there exists } z \text{:N such  that } y + z + 1 = x.
$$

The right hand is rendered as $\Sigma z \text{:N . I(N}, y + z + 1, x)$ in intuitionistic type theory, and we take this as definition of relation $>$ .
($+$ is defined by recursive equations, $\text{I}$ is the identity type construction).
Now all the properties of $>$ are determined by the mentioned introduction and elimination and computation rules for $\text{N}$ .

#### 2.1.4 A logic with several forms of judgment

The type system of intuitionistic type theory is very expressive.
As a consequence the well-formedness of a type is no longer a simple matter of parsing, it is something which needs to be proved.
Well-formedness of a type is one form of judgment of intuitionistic type theory.
Well-typedness of a term with respect to a type is another.
Furthermore, there are equality judgments for types and terms.
This is yet another way in which intuitionistic type theory differs from ordinary first order logic with its focus on the sole judgment expressing the truth of a proposition.

#### 2.1.5 Semantics

While a standard presentation of first-order logic would follow Tarski in defining the notion of model, intuitionistic type theory follows the tradition of Brouwerian meaning theory as further developed by Heyting and Kolmogorov, the so called BHK-interpretation of logic.
The key point is that the proof of an implication $A \supset B$ is a method that transforms a proof of $A$ to a proof of $B$.
In intuitionistic type theory this method is formally represented by the program $f: A \supset B$ or $f: A \to B$ : the type of proofs of an implication $A \supset B$ is the type of functions which maps proofs of $A$ to proofs of $B$ .

Moreover, whereas Tarski semantics is usually presented meta-mathematically, and assumes set theory, Martin-Löf’s meaning theory of intuitionistic type theory should be understood directly and “pre-mathematically”, that is, without assuming a meta-language such as set theory.

#### 2.1.6 A functional programming language

Readers with a background in the lambda calculus and functional programming can get an alternative first approximation of intuitionistic type theory by thinking about it as a typed functional programming language in the style of Haskell or one of the dialects of ML.
However, it differs from these in two crucial aspects: (i) it has dependent types (see below) and (ii) all typable programs terminate.
(Note that intuitionistic type theory has influenced recent extensions of Haskell with generalized algebraic datatypes which sometimes can play a similar role as inductively defined dependent types.)

### 2.2 The Curry-Howard Correspondence

As already mentioned, the principle that

```
a proposition is the type of its proofs.
```

is fundamental to intuitionistic type theory.
This principle is also known as the Curry-Howard correspondence or even Curry-Howard isomorphism.
Curry discovered a correspondence between the implicational fragment of intuitionistic logic and the simply typed lambda-calculus.
Howard extended this correspondence to first-order predicate logic.
In intuitionistic type theory this correspondence becomes an identification of proposition and types, which has been extended to include quantification over higher types and more.

### 2.3 Sets of Proof-Objects

So what are these proof-objects like? They should not be thought of as logical derivations, but rather as some (structured) symbolic evidence that something is true.
Another term for such evidence is “truth-maker”.

It is instructive, as a somewhat crude first approximation, to replace types by ordinary sets in this correspondence.
Define a set $E_{m,n}$ , depending on $m,n \in \N$ , by:

$$
E_{m,n} = \begin{cases}
  \{0\}       &\text{if } m = n \\
  \varnothing &\text{if } m \not = n
\end{cases}
$$
