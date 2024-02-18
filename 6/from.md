# Introduction to the Calculus of Inductive Constructions

> [From](https://inria.hal.science/hal-01094195/document)

## 1. Introduction

The Calculus of Inductive Constructions (CIC) is the formalism behind the interactive proof assistant __Coq__.
It is a powerful language which aims at representating both functional programs in the style of the ML language and proofs in higher-order logic.
Many data-structures can be represented in this languages: usual data-types like lists and binary trees (possibly polymorphic) but also infinitely branching trees.
At the logical level, inductive definitions give a natural representation of notions like reachability and operational semantics defined using inference rules.

Inductive definitions in the context of a proof language were formalised in the early 90’s in two different settings.
The first one is Martin-L¨of’s Type Theory.
This theory was originally presented with a set of rules defining basic notions like products, sums, natural numbers, equality.
All of them (except for functions) are an instance of a general scheme of inductive definitions which has been studied by P. Dybjer.
The second one is the pure Calculus of Constructions.
This is a typed polymorphic functional language, which is powerful enough to encode inductive definitions,
but this encoding has some drawbacks: efficiency of computation of functions over these data-types and some natural properties that cannot be proven.
The extension of the formalism with primitive inductive definitions was consequently a natural choice.
In proof assistants based on higher-order logic (HOL), an impredicative encoding of inductive definitions is used:
this is made possible by the existence of a primitive infinite type (including integers) and the fact that HOL is only concerned by extensional properties of objects (not computations).

Inductive definitions, as a primitive or derived notion are one of the main ingredients of the languages for interactive theorem proving both for representing objects and logical notions.

In this paper, we give a quick overview of the Calculus of Inductive Constructions, the formalism behind the Coq proof assistant.
In section 2, we present the language and the typing rules.
We start with the pure functional part and then continue with the inductive declarations.
We shall then briefly discuss the properties of this language in section 3, both from the theoretical and pragmatic points of view.
We shall then conclude with examples of applications, the description of some of the trends in sections 4,5 and 6.

## 2. Proof System

### 2.1 The calculus of constructions

The Calculus of Constructions which is the purely functional language underlying the Calculus of Inductive Constructions has been introduced by Coquand and Huet.
It can be defined as a pure type system (PTS).
A PTS is a typed lambda-calculus with a unique syntactic language describing both terms and types.
Terms include variables, (typed) abstractions (written $\bold{fun} \ x : A ⇒ t$) and applications (written $t$ $u$) as in ordinary lambda-calculus.
The type of an abstraction is a (dependent) product $Πx : A, B$ making possible for the type $B$ of $t$ to depend on the variable $x$.
The notation $A → B$ for the type of functions from type $A$ to type $B$ is just an abbreviation in the special case where $B$ does not depend on $x$.
Types are themselves typed objects, the type of a type will be a special constant called a _sort_.
There is at least one sort called __Type__.
Different __PTS__ depend on the set of sorts we start with (each sort corresponds to a certain universe of objects) and also which products can be done (in which universes).

For instance, with A a type, the identity function $\bold{fun} \ x : A ⇒ x$ is a term of type $A → A$.
With A being a type variable, we may build the polymorphic identity $\bold{fun} \ A : \mathsf{Type} ⇒ \bold{fun} \ x : A ⇒ x$ of type $ΠA : \mathsf{Type}, A → A$.

In the case of the Calculus of Constructions, we have an infinite set of sorts $S \stackrel{def}{=} \{Prop\} ∪ ⋃_{i∈N} \{\mathsf{Type}_i\}$.
The sort Prop captures the type of expressions which denote logical propositions.
We follow the Curry-Howard correspondence where a proposition $A$ is represented by a type (namely the type of proofs of $A$) and a proof of the logical proposition $A$ will correspond to an object $t$ of type $A$.
If $A$ and $B$ are two types corresponding to logical propositions, then the proposition $A ⇒ B$ will be represented by the type $A → B$ of functions transforming proofs of $A$ into proofs of $B$, the proposition $A ∧ B$ will be represented by the type $A × B$ of pairs build with a proof of $A$ and a proof of $B$.
Given a type $T$ , the type $Πx : T, B$ will represent the type of dependent functions which given a term $t : T$ computes a term of type $B[t/x]$ corresponding to proofs of the logical proposition $∀x : T, B$.
Because types represent logical propositions, the language will contain empty types corresponding to unprovable propositions.

Notations. We shall freely use the notation $∀x : A, B$ instead of $Πx : A, B$ when $B$ represents a proposition.
We write $t[u/x]$ for the term $t$ in which the variable $x$ has been replaced by the term $u$.
The term $t \ u_1 . . . u_n$ represents $(. . . (t \ u_1) . . . u_n)$ and $\bold{fun} \ (x_1 : A_1) . . . (x_n : A_n) ⇒ t (resp. Π(x_1 : A_1) . . . (x_n : A_n), B)$ is the same as $\bold{fun} \ x_1 : A_1 ⇒ . . . \bold{fun} \ x_n : A_n ⇒ t (resp.  Π x_1 : A_1, . . . Π x_n : A_n, B)$.
The term $A → B → C$ should be understood as $A → (B → C)$ and $Π x : A, B → C$ is the same as $Π x : A, (B → C)$.
We sometimes omit the type of the variable in abstractions and products when they are clear from the context.

In higher-order logic, propositions and objects are written using the same functional language with abstractions and applications.
We may want to introduce a binary relation on a type $A$ as a variable $R$.
This variable will have type $A → A → Prop$ (this type replaces an arity declaration in first-order logic).
We can build a predicate $\bold{fun} \ x : A ⇒ R \ x \ x$ representing the set of objects which are in relation with themselves, this predicate will have type A → Prop (this expression shall not be confused with the type ∀x : A, R x x of type Prop, expressing the reflexivity of R).

We need A → A → Prop to be a well-formed type, which means it is typed with a sort. This sort will be Type1. If we want to iterate constructions on Type1, we shall need this sort itself to be well-typed, that will require introducing a new sort Type2 to be the type of the object Type1. The
need for an infinite hierarchy of universes comes from the fact that the more naive system where we have only one sort Type of type Type is inconsistent.

The Calculus of Inductive Constructions manipulates judgements which are of the form

x1 : A1, . . . , xn : An ⊢ t : A

In this judgement, x1 : A1, . . . , xn : An is called the context and the part t : A on the right-
hand side of the ⊢ sign is called the conclusion. In the context, xi is a variable declared of type Ai
representing the name of an object. Following the propositions as types paradigm, when Ai denotes
a logical proposition, xi will be a name given to the hypothesis that Ai holds. The judgement can
be read as: under the assumption that we have objects xi of type Ai, the term t is well-formed of
type A.

For instance, in order to reason on Peano integers, it is possible to introduce a signature with a
type variable N : Type for representing the type of Peano integers, an object z : N (for zero) and an
object S : N → N for the successor function. We call ΓS the context N : Type, z : N, S : N → N .
The following judgements are derivable :

ΓS ⊢ z : N ΓS ⊢ S z : N ΓS ⊢ S (S z) : N

It is also possible to introduce a binary relations le which represents the natural order on N . We
shall add le : N → N → Prop and hypotheses like lez : ∀x : N, le z n and leS : ∀x y : N, le x y →
le (S x) (S y). We introduce a new context

ΓN def= ΓS , le : N → N → Prop, lez : (∀x : N, le z x), leS : (∀x y : N, le x y → le (S x) (S y))
