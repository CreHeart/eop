## Loose Ends

3.1: Prove that for an associative operation, all possible parentheses groupings are equivalent
Footnote 3.3 (page 34)
Footnote 4.4 (page 55)
Exercise 4.5: Prove that my solution performs 5 2/3 comparisons on average
Exercise 4.6: My solution is really sloppy
Footnotes 5.9-5.11 (page 81)
Draw out the hierarchy of algebraic types
Prove that NonnegativeDiscreteArchimedeanSemiring and DiscreteArchimedeanRing are univalent
Implement an adapter that converts an IndexedIterator into a RandomAccessIterator
Exhaustive test cases for bifurcate_compare
    Generating random trees?
[DONE] traverse that can terminate early
Revisit Exercise 8.1 more rigorously
Rewrite the proof of Lemma 8.2 more concisely
Exercise 8.3:
    Something more precise than “it’s about n lg n”?
    How to calculate average case?
How does the Writable concept justify exactly one assignment to sink(x)?
How do we know that only multipass algorithms both read from and write to the same range?
Why does the definition of write_aliased use a forall instead of an exists?
Exercise 9.4
What’s an example of an ordering-based arrangement?
Lemma 10.18
Clarify axioms for arithmetic between iterators and integers
[DONE] *Lemma 10.26
Add versions of reduce (my_iterator.h, plus my_reduce_balanced) that don’t take that god damn “fun” parameter
Lemma 11.12
Lemma 11.13
Mechanism for tracing assignments and comparisons
Fix linked list iterator type so that arithmetic works
What is an “output-restricted” deque?

## Questions

What would it look like for a programming language to distinguish value types from object types?
How can we tell when a given finite set of procedures actually forms a computational basis for a type?
What does it mean to have a concept defined on more than one type?  What's an example of such a concept?
How would you formally define the "action" concept?
When would a transformation be more efficient than an action?
Footnote 3.6 (page 42): How would you write such an identity_element function?
What's an example of an optimization that can be made for non-regular functions / types?
Is the difficulty of order-selection with order 5 somehow related to the insolubility of quintics?
What's the motivation for the axiom w(a * b) >= w(a) in the definition of a EuclideanSemiring?
Chapter 5 Conclusion: What's a case of "adjusting theories to fit algorithmic requirements"?
What are some sample implementations of "source" for a readable type, and how can we verify that the implementation is about as fast as an ordinary pointer dereference?
How should we define equality for iterators?
What's the motivation for having count_if accept (and return) an iterator, as opposed to an integer?
What sort of copy semantics do we need to ensure for iterators?
When would operations involving the identity element "be slow or require extra logic to implement"?
How did floor(lg(n)) + 1 become lg(n) in Lemma 6.13?
When would we have an IndexedIterator that's not (already) a RandomAccessIterator?
[DONE] How is WeightType (for a BifurcateCoordinate) used?
What's a (useful) example where traversing a binary tree would change its shape, i.e. what's a useful example of a WeakBifurcateCoordinate that's not a BifurcateCoordinate?
[DONE] Is it possible to implement height using traverse and a function object?
When would it be useful to traverse multiple trees concurrently?
What does it mean for traversal to be "uniform"?
What do we gain by thinking about "concept schemas"?
Why doesn't the book make more use of optional parameters?
In linker_to_tail, why don't we need the precondition that successor(t) is defined?
[DONE] What's meant by "to avoid sharing of proper tails"?
    Sharing proper tails can save memory, but would also lead to strange behavior (i.e. changing one iterator's source value can change the outcome of seemingly unrelated traversals)
Is there a stable way to partition a range of n elements using 2n + 1 assignments?
How can the iterative version do up to a linear amount of extra work, and what does that even mean (page 202)?
Exercise 12.1: is the implementation of less any different from operator<?
How would make “requires” serve as more than just documentation?

## Definitions

### 1.1

An **abstract entity** is an individual thing that is eternal and unchangeable
A **concrete entity** is an individual thing that comes into and out of existence in space and time
An **attribute** is a correspondence between a concrete entity and an abstract entity that describes some property, measurement, or quality of the concrete entity
**Identity** determines the sameness of a thing changing over time
A **snapshot** (of a concrete entity) is a complete collection of its attributes at a particular point in time
An **abstract species** describes common properties of essentially equivalent abstract entities
A **concrete species** describes the set of attributes of essentially equivalent concrete entities
A **function** is a rule that associates one or more abstract entities, called **arguments** (from corresponding species) with an abstract entity, called the **result**, from another species
An **abstract (or concrete) genus** describes different abstract (or concrete) species that are similar in some respect

### 1.2

A **datum** is a finite sequence of 0s and 1s
A **value type** is a correspondence between a species (abstract or concrete) and a set of datums
  A datum corresponding to a particular entity is called a **representation** of the entity (we say the datum **represents** the entity)
  An entity corresponding to a particular datum is called an **interpretation** of the datum
  A **value** is a datum (which we sometimes refer to as the representation of the value; we also sometimes say that the datum represents the value) together with the datum's interpretation (which we sometimes refer to as the interpretation of the value; we also sometimes say that the value represents its datum's interpretation)
    [When we say value, we may be referring to the actual value (i.e. the datum together with its interpretation), only the datum, or only the interpretation; the usage should (hopefully) be clear from context]
A datum is **well-formed** (with respect to a value type) if that datum represents an abstract entity
A value type is **properly partial** if its values represent a proper subset of the abstract entities in the corresponding species; otherwise it is **total**
A value type is **uniquely represented** if at most one value corresponds to each abstract entity
A value type is **ambiguous** if a datum has more than one interpretation; otherwise, it is **unambiguous**
Two values of a value type are **equal** if they represent the same abstract identity (i.e. if they have the same interpretation)
Two values of a value type are **representationally equal** if their datums are identical sequences of 0s and 1s
A function defined on a value type is **regular** if substituting an equal value for an argument gives an equal result

### 1.3

A **memory** is a set of words, each with an **address** and a **content**
  The addresses are values of a fixed size, called the **address length**
  The contents are values of another fixed size, called the **word length**
  The content of an address is obtained by a **load** operation
  The association of a content with an address is changed by a **store** operation
An **object** is a representation of an entity as a value in memory
  An object has a **state** that is a value of some value type
    The state is changeable
    The state corresponds to a snapshot of the concrete entity corresponding to the object
  An object owns a set of **resources** (memory, file) to hold its state
  An object (for the purposes of this book) has a unique **starting address** from which all of its resources can be reached
An **object type** is a pattern for storing and modifying values in memory
An object is {well-formed, properly partial, total, uniquely represented} if its state is {well-formed, properly partial, total, uniquely represented}
  Each object type has a corresponding value type describing states of objects of that type
An **identity token** is a value expressing the identity of an object, and is computed from the value of the object and the address of its resources
  Testing equality of identity tokens corresponds to testing equality of identity
Two objects of the same type are equal if their states are equal
  If two objects are equal, and the two objects do not have equal identity tokens, then we say that one is a **copy** of the other
  Making a change to an object does not affect any copy of it
When we say type (without qualification), we mean object type

### 1.4

A **procedure** is a sequence of instructions that modifies the state of some objects; it may also construct or destroy objects
Procedures interact with four different kinds of objects:
  1. Input/output: objects passed to/from a procedure directly or indirectly through its arguments or returned result
  2. Local state: objects created, destroyed, and usually modified during a single invocation of the procedure
  3. Global state: objects accessible to this and other procedures across multiple invocations
  4. Own state: objects accessible only to this procedure (and its affiliated procedures) but shared across multiple invocations
An object is passed **directly** if it is passed as an argument or returned as a result
An object is passed **indirectly** if it is passed by a pointer or a pointerlike object
An object is an **input** to a procedure if it is read, but not modified, by a procedure
An object is an **output** from a procedure if it is written, created, or destroyed by the procedure, but its initial state is not read by the procedure
An object is an **input/output** of a procedure if it is modified as well as read by the procedure
A **computational basis** for a type is a finite set of procedures that enable the construction of any other procedure on the type
  A basis is **efficient** if any proceduer implemented using it is as [asymptotically] efficient as an equivalent procedure written in terms of an alternative basis
  A basis is **expressive** if it allows compact and convenient definitions of procedures on the type

### 1.5

A type is **regular** if its basis includes equality, assignment, destructor, default constructor, copy constructor, total ordering, and underlying type
**Equality** is a procedure that takes two objects of the same types and returns true if and only if the object states are equal (inequality is the negation of equality)
**Assignment** is a procedure that takes two objects of the same type and makes the first object equal to the second without modifying the second; the meaning of assignment does not depend on the initial value of the first object
A **destructor** is a procedure causing the cessation of an object's existence
A **constructor** is a procedure transforming memory locations into an object
An object is in a **partially formed** state if it can be assigned to or destroyed
A **default constructor** is a constructor that takes no arguments and leaves the object in a partially formed state
A **copy constructor** for a type is a constructor that takes an argument of the same type and constructs a new object equal to the argument

### 1.6

A procedure is **regular** if replacing its inputs with equal objects results in equal output objects
A **functional procedure** is a regular procedure defined on regular types, with one or more direct inputs and a single output that is returned as a result of the procedure
  Note that we can pass inputs either by value (making a local copy) or by constant reference
  A functional procedure can be implemented as a C++ function, function pointer, or functor (function object)
The **definition space** for a functional procedure is the subset of values for tis inputs to which it is intended to be applied
  A functional procedure always terminates on input in its definition space
A **homogeneous** functional procedure is one whose input objects are all the same type
The **domain** of a homogeneous functional procedure is the type of its inputs
The **codomain** for a functional procedure is the type of its output
The **result space** for a functional procedure is the set of all values from its codomain returned by the procedure for inputs from its definition space

### 1.7

A **concept** is a collection of requirements (expressed as syntactic and semantic properties) on types
  Type represents species; concepts represent genera
A **type attribute** is a mapping from a type to a value describing some characteristic of the type
A **type function** is a mapping from a type to an affiliated type
  An indexed type function takes an additional constant integer parameter
A **type constructor** is a mechanism for creating a new type from one or more existing types
More formally, a **concept** is a description of requirements on one or more types stated in terms of the existence and properties of procedures, type attributes, and type functions defined on the types
We say a concept is **modeled by** specific types, or that the types **model** the concept, if the requirements are satisfied for those types
A concept C' **refines** another concept C if whenever C' is satisfied for a set of types, C is also satisfied for that set of types
A concept C **weakens** another concept C' if C' refines C
A **type concept** is a concept defined on one type
We define a concept C by writing

        C(T_0, ..., T_{n-1}) := E_0 ^ E_1 ^ ... ^ E^{k-1}

  The T_i are formal type parameters
  Each E_i is a concept clause that takes one of three forms:
    1. Application of a previously defined concept, indicating a subset of the formal type parameters that model it
    2. Signature of a type attribute, type function, or procedure that must exist for any types modeling the concept
        A procedure signature takes the form f: T -> T', where T is the domain and T' is the codomain
        A type function signature takes the form F: C -> C', where the domain and codomain are concepts
    3. Axiom expressed in terms of these type attributes, type functions, and procedures
  We sometimes include the definition of a type attribute, type function, or procedure following its signature in the second kind of concept clause, though particular models may override this definition

        UnaryFunction(F) :=
            FunctionalProcedure(F)
          ^ Arity(F) = 1
          ^ Domain: UnaryFunction -> Regular
                F |-> InputType(F, 0)

        HomogeneousFunction(F) :=
            FunctionalProcedure(F)
          ^ Arity(F) > 0
          ^ (forall i, j in N)(i, j < Arity(F)) => (InputType(F, i) = InputType(F, j))
          ^ Domain: HomogeneousFunction -> Regular
                F |-> InputType(F, 0)

An **abstract** procedure is parametrized by types and constant values, with requirements on those parameters
  An abstract procedure is regular if all its instantiations are regular
**Preconditions** describe properties of particular objects

### 2.1

    Predicate(P) :=
        FunctionalProcedure(P)
      ^ Codomain(P) = bool

    HomogeneousPredicate(P) :=
        Predicate(P)
      ^ HomogeneousFunction(P)

    UnaryPredicate(P) :=
        Predicate(P)
      ^ UnaryFunction(P)

    Operation(Op) :=
        HomogeneousFunction(Op)
      ^ Codomain(Op) = Domain(Op)

A procedure is **partial** if its definition space is a subset of the direct product of the types of its inputs
A procedure is **total** if its definition space is equal to the direct product of the types of its inputs (we consider a total function to be partial)
A procedure is **nontotal** if it is partial but not total
A **definition-space predicate** for a partial procedure f is a [total] predicate p, with the same input types as f, that returns true if and only if the inputs are within the definition space of f

    Transformation(F) :=
        Operation(F)
      ^ UnaryFunction(F)
      ^ DistanceType: Transformation -> Integer

When f is a transformation, we define its powers as follows:

    f^n(x) = | x              if n = 0
             | f^{n-1}(f(x))  if n > 0

### 2.2

y is **reachable** from x under a transformation f if for some n >= 0, y = f^n(x)
x is **cyclic** under f if for some n >= 1, x = f^n(x)
x is **terminal** under f if x is not in the definition space of f
The **orbit** of x under a transformation f is the set of all elements reachable from x under f
If y is reachable from x under f, the **distance** from x to y is the smallest non-negative integer n such that f^n(x) = y
Given a transformation type F, DistanceType(F) is an integer type large enough to encode the distance between any two elements of Domain(F)
An orbit of x under a transformation is:
  **infinite**      if it has no cyclic or terminal elements (otherwise, it is **finite**)
  **terminating**   if it has a terminal element
  **circular**      if x is cyclic
  **p-shaped**      if x is not cyclic, but its orbit contains a cyclic element
The **orbit cycle** is the set of cyclic elements in the orbit (empty for infinite orbits and terminating orbits)
The **orbit handle** is the complement of the orbit cycle with respect to the orbit (empty for circular orbits)
The **connection point** is the first cyclic element (i.e. f^n(x) where n is the smallest non-negative integer such that f^n(x) is cyclic under f)
  The connection point of a circular orbit is the first element
  The connection point of a p-shaped orbit is the first element after the handle
  Infinite orbits and terminating orbits do not have a connection point
The **orbit size (o)** of an orbit is the number of distinct elements in the orbit
The **handle size (h)** of an orbit is the number of elements in the orbit handle
The **cycle size (c)** of an orbit is the number of elements in the orbit cycle

### 2.3

The **collision point** of a transformation f and a starting point x is the unique y such that y = f^n(x) = f^{2n+1}(x), and n >= 0 is the smallest integer satisfying this condition

### 2.5

An **action** is a procedure that changes the state of an object

## Chapter 3

    BinaryOperation(Op) :=
        Operation(Op)
      ^ Arity(Op) = 2

If f and g are transformations on the same domain, their **composition**, g o f, is a transformation mapping x to g(f(x))
An element x has **finite order** under an associative operation if there exist integers 0 < n < m such that x^n = x^m
An element x is an **idempotent element** under an associative operation if x = x^2

**Theorem 3.1.** An element of finite order has an idempotent power.
**Proof.** Suppose x has finite order, i.e. x^n = x^m for integers 0 < n < m.  Let f be the transformation that maps y to xy; then the orbit of x under f contains the cyclic element x^n (since f^{m-n}(x^n) = x^{m-n} * x^n = x^m = x^n).  Then

    x^{n*(m-n)}^2 = x^{n*(m-n)} * x^n * x^{n*(m-n-1)}
                  = f^{n*(m-n)}(x^n) * x^{n*(m-n-1)}
                  = x^n * x^{n*(m-n-1)}
                  = x^{n*(m-n)}

which shows that x^{n*(m-n)} is idempotent.

**Proof.** (EoP) Suppose x has finite order, and let f be the transformation that maps z to xz.  Then the orbit of x under f has a cyclic element.  Let y = f^n(x) be the collision point of f and x; then f^n(x) = f^{2n+1}(x), and by the definition of f, x^{n+1} = x^{2n+2}, which shows that x^{n+1} is idempotent.

A recursive procedure is in **tail-recursive form** if the procedure's execution ends with the recursive call
A recursive procedure is in **strict tail-recursive form** if all the tail-recursive calls are done with the formal parameters of the procedure being the corresponding arguments
Using an operator symbol or procedure name with the same semantics on different types is called **overloading**
  In this case, we say that the operator symbol or procedure name is **overloaded** on the type
A **linear recurrence function of order k** is a function f such that

    f(y_0, ..., y_{k-1}) = \Sum_{i=0}^{k-1} a_i y_i, where a_0, a_{k-1} != 0

A sequence is a **linear recurrence of order k** if there is a linear recurrence function of order k--say f--and

    (forall n >= k) x_n = f(x_{n-1}, ..., x_{n-k})

Changing the state of an object by combining it with another object via a binary operation defines an **accumulation procedure** on the object
An algorithm is **abstract** if it can be used with different models satisfying the same requirements (eg. associativity)

## Chapter 4

A [binary] **relation** is a predicate taking two parameters of the same type:

    Relation(Op) :=
        HomogeneousPredicate(Op)
      ^ Arity(Op) = 2

A relation is **transitive** if whenever it holds between a and b, and between b and c, it holds between a and c

    property(R: relation)
    transitive: R
        r |-> (forall a, b, c in Domain(R)) (r(a, b) ^ r(b, c) implies r(a, c))

A relation is **strict** if it never holds between an element and itself
A relation is **reflexive** if it always holds between an element and itself

    property(R: relation)
    strict: R
        r |-> (forall a in Domain(R)) !r(a, a)

    property(R: relation)
    reflexive: R
        r |-> (forall a in Domain(R)) r(a, a)

A relation is **symmetric** if whenever it holds in one direction, it holds in the other
A relation is **asymmetric** if it never holds in both directions

    property(R: relation)
    symmetric: R
        r |-> (forall a, b in Domain(R)) (r(a, b) implies r(b, a))

    property(R: relation)
    asymmetric: R
        r |-> (forall a, b in Domain(R)) (r(a, b) implies !r(b, a))

Given a relation r(a, b), we define the following **derived relations** with the same domain:

                complement_r(a, b) <=> !r(a, b)
                  converse_r(a, b) <=> r(b, a)
    complement_of_converse_r(a, b) <=> !r(b, a)

A relation is an **equivalence** if it is transitive, reflexive, and symmetric

    property(R: relation)
    equivalence: R
        r |-> transitive(r) ^ reflexive(r) ^ symmetric(r)

An **equivalence class** for an equivalence relation is a subset of its domain containing all elements equivalent to a given element
We can implement an equivalence relation by defining a **key function**, a function that returns the same value for all elements in a given equivalence class (and different values for elements in different equivalence classes)

    property(F: UnaryFunction, R: Relation)
        requires(Domain(F) = Domain(R))
    key_function: F x R
        (f, r) |-> (forall a, b in Domain(F)) (r(a, b) <=> f(a) = f(b))

A relation is a **total ordering** if it is transitive and obeys the **trichotomy law** (for every pair of elements, exactly one of the following holds: the relation, its converse, or equality)

    property(R: Relation)
    total_ordering: R
        r |-> transitive(r) ^
              (forall a, b in Domain(R)) exactly one of the following holds:
                  r(a, b), r(b, a), or a = b

A relation is a **weak ordering** if it is transitive and there is an equivalence relation on the same domain such that the original relation obeys the **weak-trichotomy law** (for every pair of elements, exactly one of the following holds: the relation, its converse, or the equivalence relation)

    property(R: Relation, E: Relation)
        requires(Domain(R) = Domain(E))
    weak_ordering: R
        r |-> transitive(r) ^ (exists e in E) equivalence(e) ^
              (forall a, b in Domain(R)) exactly one of the following holds:
                  r(a, b), r(b, a), or e(a, b)

Given a relation r, the relation !r(a, b) ^ !r(b, a) is called the **symmetric complement** of r
Given a key function f on a set T, together with a total ordering r on the codomain of f, we can define the following weak ordering on T:

    r'(x, y) <=> r(f(x), f(y))

We refer to total and weak orderings as **linear orderings**
An algorithm is **stable** if it respects the original order of equivalent objects

    TotallyOrdered(T) :=
        Regular(T)
      ^ <: T x T -> bool
      ^ total_ordering(<)

## Chapter 5

An element is called an **identity element** of a binary operation if, when combined with any other element as the first or second element, the operation returns the other element:

    property(T: Regular, Op: BinaryOperation)
        requires(T = Domain(Op))
    identity_element: T x Op
        (e, op) |-> (forall a in T) op(a, e) = op(e, a) = a

A transformation is called an **inverse operation** of a binary operation with respect to a given element (usually the identity of the binary operation) if it satisfies the following:

    property(F: Transformation, T: Regular, Op: BinaryOperation)
        requires(Domain(F) = T = Domain(Op))
    inverse_operation: F x T x Op
        (inv, e, op) |-> (forall a in T) op(a, inv(a)) = op(inv(a), a) = e

A binary operation is **commutative** if its result is the same when its arguments are interchanged:

    property(Op: BinaryOperation)
    commutative: Op
        op |-> (forall a, b in Domain(Op)) op(a, b) = op(b, a)

A set with an associative operation is called a **semigroup**
A type with + (which should be commutative) is called an **additive semigroup**

    AdditiveSemigroup(T) :=
        Regular(T)
      ^ +: T x T -> T
      ^ associative(+)
      ^ commutative(+)

A type with * (which is not necessarily commutative) is called a **multiplicative semigroup**

    MultiplicativeSemigroup(T) :=
        Regular(T)
      ^ *: T x T -> T
      ^ associative(*)

A semigroup with an identity element is called a **monoid**
We denote the additive identity element by 0, and define an **additive monoid** as follows:

    AdditiveMonoid(T) :=
        AdditiveSemigroup(T)
      ^ 0 in T
      ^ identity_element(0, +)

We denote the multiplicative identity element by 1, and define a **multiplicative monoid** as follows:

    MultiplicativeMonoid(T) :=
        MultiplicativeSemigroup(T)
      ^ 1 in T
      ^ identity_element(1, *)

A monoid with an inverse operation is called a **group**
We denote the inverse operation of an additive monoid by -, and define an **additive group** as follows:

    AdditiveGroup(T) :=
        AdditiveMonoid(T)
      ^ -: T -> T
      ^ InverseOperation(unary -, 0, +)
      ^ -: T x T -> T
            (a, b) |-> a + (-b)

Similarly, we define a **multiplicative group** as follows:

    MultiplicativeGroup(T) :=
        MultiplicativeMonoid(T)
      ^ multiplicative_inverse: T -> T
      ^ InverseOperation(multiplicative_inverse, 1, *)
      ^ /: T x T -> T
            (a, b) |-> a * multiplicative_inverse(b)

We write multiplicative_inverse(x) as x^{-1}
When both + and * are present on a type, they are [i.e. should be] interrelated with axioms defining a **semiring**:

    Semiring(T) :=
        AdditiveMonoid(T)
      ^ MultiplicativeMonoid(T)
      ^ 0 != 1
      ^ (forall a in T) a * 0 = 0
      ^ (forall a, b, c in T)
            a * (b + c) = a * b + a * c
          ^ (a + b) * c = a * c + b * c

The axiom about multiplication by zero is called the **annihilation property**
The axiom connecting + and * is called the **distributive property**, or **distributivity**

    CommutativeSemiring(T) :=
        Semiring(T)
      ^ commutative(*)

    Ring(T) :=
        AdditiveGroup(T)
      ^ Semiring(T)

    CommutativeRing(T) :=
        AdditiveGroup(T)
      ^ CommutativeSemiring(T)

A **relational concept** is a concept defined on two types
**semimodule** is a relational concept that connects an additive monoid and a commutative semiring:

    Semimodule(T, S) :=
        AdditiveMonoid(T)
      ^ CommutativeSemiring(S)
      ^ *: S x T -> T
      ^ (forall A, B in S) (forall a, b, in T)
            A * (B * a) = (A * B) * a
            (A + B) * a = A * a + B * a
            A * (a + b) = A * a + A * b
                  1 * a = a

If Semimodule(T, S), we say that T is a semimodule over S; we call elements of T **vectors** and elements of S **scalars**

**Theorem 5.1** AdditiveMonoid(T) implies Semimodule(T, N), where scalar multiplication is defined as n * x = x + ... + x (n times).
**Proof.** Let A, B be natural numbers, and let a, b be vectors in T.  Then

    A * (B * a) = (B * a) + ... + (B * a)
                = (a + ... + a) + ... + (a + ... + a)

where there are A parenthesized terms and B copies of a inside each parenthesized term, for a total of A * B copies of a; thus A * (B * a) = (A * B) * a.  Next,

    A * a + B * a = (a + ... + a) + (a + ... + a)

where there are A copies of a in the left parenthesized term and B copies of a in the right parenthesized term, for a total of A + B copies of a; thus A * a + B * a = (A + B) * a.  Furthermore,

    A * (a + b) = (a + b) + ... + (a + b)

and by commutativity of addition, the expression on the left becomes (a + ... + a) + (b + ... + b); thus A * (a + b) = A * a + A * b.  Finally, 1 * a = a follows immediately from the definition of *.

Replacing the additive monoid with an additive group and replacing the semiring with a ring in the definition of a semimodule transforms the semimodule into a **module**:

    Module(S, T) :=
        Semimodule(T, S)
      ^ AdditiveGroup(T)
      ^ Ring(S)

A model is called **partial** when the operations satisfy the axioms where they are defined, but are not everywhere defined

    OrderedAdditiveSemigroup(T) :=
        AdditiveSemigroup(T)
      ^ TotallyOrdered(T)
      ^ (forall a, b, c in T) a < b implies a + c < b + c

    OrderedAdditiveMonoid(T) :=
        OrderedAdditiveSemigroup(T)
      ^ AdditiveMonoid(T)

    OrderedAdditiveGroup(T) :=
        OrderedAdditiveMonoid(T)
      ^ AdditiveGroup(T)

    CancellableMonoid(T) :=
        OrderedAdditiveMonoid(T)
      ^ -: T x T -> T
      ^ (forall a, b in T) b <= a implies
            a - b is defined ^ (a - b) + b = a

    ArchimedeanMonoid(T) :=
        CancellableMonoid(T)
      ^ (forall a, b in T) (a >= 0 ^ b > 0) implies slow_remainder(a, b) terminates
      ^ QuotientType: ArchimedeanMonoid -> Integer

    HalvableMonoid(T) :=
        ArchimedeanMonoid(T)
      ^ half: T -> T
      ^ (forall a, b in T) b > 0 ^ a = b + b implies half(a) = b

For a >= b and b > 0 in an Archimedean monoid T, we define **divisibility** as follows:

    b divides a <=> (exists n in QuotientType(T)) a = nb

A **greatest common divisor** of a and b, denoted by gcd(a, b), is a divisor of a and b that is divisible by any other common divisor of a and b

**Theorem.** subtractive_gcd_nonzero(sqrt(2), 1) does not terminate [assuming an arbitrary precision representation of sqrt(2)]
**Proof.** Suppose it terminates and returns d.  Write m = sqrt(2) / d and n = 1 / d.  Then m / n = sqrt(2), so m^2 = 2n^2, and m is even.  Write m = 2u; then (2u)^2 = 4u^2 = 2n^2, so n is even.  This contradicts Lemma 5.15; we conclude that subtractive_gcd_nonzero does not terminate.

A **Euclidean monoid** is an Archimedean monoid where subtractive_gcd_nonzero always terminates:

    EuclideanMonoid(T) :=
        ArchimedeanMonoid(T)
      ^ (forall a, b in T) (a > b ^ b > 0) implies subtractive_gcd_nonzero(a, b) terminates

    EuclideanSemiring(T) :=
        CommutativeSemiring(T)
      ^ NormType: EuclideanSemiring -> Integer
      ^ w: T -> NormType(T)
      ^ (forall a in T) w(a) >= 0
      ^ (forall a in T) w(a) = 0 <=> a = 0
      ^ (forall a, b in T) b != 0 implies w(a * b) >= w(a)
      ^ remainder: T x T -> T
      ^ quotient: T x T -> T
      ^ (forall a, b in T) b != 0 implies a = quotient(a, b) * b + remainder(a, b)
      ^ (forall a, b in T) b != 0 implies w(remainder(a, b)) < w(b)

w is called the **Euclidean function** [Euclidean norm?]

    EuclideanSemimodule(T, S) :=
        Semimodule(T, S)
      ^ remainder: T x T -> T
      ^ quotient: T x T -> S
      ^ (forall a, b in T) b != 0 implies a = quotient(a, b) * b + remainder(a, b)
      ^ (forall a, b in T) (a != 0 v b != 0) implies gcd(a, b) terminates

An Archimedean group must also satisfy the following properties (b != 0):

    a = quotient(a, b) * b + remainder(a, b)
    |remainder(a, b)| < |b|
    remainder(a + b, b) = remainder(a - b, b) = remainder(a, b)

Dirichlet: If two numbers a and b have the same remainder r relative to the same modulus k they will be called **congruent** relative to the modulus k (following Gauss)

    ArchimedeanGroup(T) :=
        ArchimedeanMonoid(T)
      ^ AdditiveGroup(T)

    DiscreteArchimedeanSemiring(T) :=
        CommutativeSemiring(T)
      ^ ArchimedeanMonoid(T)
      ^ (forall a, b, c in T) a < b ^ 0 < c implies a * c < b * c
      ^ !(exists a in T) 0 < a < 1

**Discreteness** refers to the property that there is no element between 0 and 1

    NonnegativeDiscreteArchimedeanSemiring(T) :=
        DiscreteArchimedeanSemiring(T)
      ^ (forall a in T) 0 <= a

    DiscreteArchimedeanRing(T) :=
        DiscreteArchimedeanSemiring(T)
      ^ AdditiveGroup(T)

Two types T and T' are **isomorphic** if it is possible to write conversion functions from T to T' and from T' to T that preserve the procedures and their axioms
A concept is **univalent** if any types satisfying it are isomorphic.
A proposition is **independent** from a set of axioms if there is a model in which all of the axioms are true, but the proposition is false
A proposition is **dependent** or **provable** from a set of axioms if it can be derived from them [in which case for every model where the axioms are true, the proposition is also true]
A concept is **consistent** if it has a model
A concept is **inconsistent** if both a proposition and its negation can be derived from its axioms [in which case no model exists for that concept]
A concept is **useful** if there are useful algorithms for which this is the most abstract setting
A **bounded unsigned binary integer type** U_n, where n = 8, 16, 32, 64, ..., is an unsigned integer type capable of representing a value in the interval [0, 2^n)
A **bounded signed binary integer type** S_n, where n = 8, 16, 32, 64, ..., is a signed integer type capable of representing a value in the interval [-2^{n-1}, 2^{n-1})

## Chapter 6

A type T is **readable** if a unary function "source" defined on it returns an object of type ValueType(T):

    Readable(T) :=
        Regular(T)
      ^ ValueType: Readable -> Regular
      ^ source: T -> ValueType(T)

A **pseudotransformation** has the signature of a transformation but is not necessarily regular

    Iterator(T) :=
        Regular(T)
      ^ DistanceType: Iterator -> Integer
      ^ successor: T -> T
      ^ successor is not necessarily regular

An iterator algorithm is **single-pass** if it applies successor to the value of each iterator once

    property(I: Iterator)
    weak_range: I x DistanceType(I)
        (f, n) |-> (forall i in DistanceType(I))
                       (0 <= i <= n) implies successor^i(f) is defined

    property(I: Iterator, N: Integer)
    counted_range: I x N
        (f, n) |-> weak_range(f, n) ^
                       (forall i, j in N) (0 <= i < j <= n) implies
                           successor^i(f) != successor^j(f)

    property(I: Iterator)
    bounded_range: I x I
        (f, l) |-> (exists k in DistanceType(I))
                       counted_range(f, k) ^ successor^k(f) = l

A **half-open weak (or counted) range** [[f, n|), where n >= 0 is an integer, denotes the sequence of iterators

    {successor^k(f) | 0 <= k < n}

A **closed weak (or counted) range** [[f, n]], where n >= 0 is an integer, denotes the sequence of iterators

    {successor^k(f) | 0 <= k <= n}

A **half-open bounded range** [f, l) is equivalent to the half-open counted range[[f, l - f|)
A **closed bounded range** [f, l] is equivalent to the closed counted range [[f, l - f]]
    [Also known as a compact range--jk lol]
If r is a range and i is an iterator, we say i is in r, or i is an element of r, if i is a member of r when we consider the set of iterators in r (note that r itself is a sequence of iterators, not a set of iterators)
We denote empty half-open ranges by [[i, 0|) or [i, i) for some iterator i
An iterator l is called the **limit** of a half-open bounded range [f, l); also, f + n is the limit of the half-open weak range [[f, n|)
    Note that i is the limit of the empty ranges [[i, 0|) and [i, i)
Given two iterators i and j in a counted or bounded range, we say i precedes j if i != j and bounded_range(i, j), i.e. one or more applications of successor leads from i to j
A range of iterators from a type modeling Readable and Iterator is **readable** if source is defined on all iterators in the range:

    property(I: Readable)
        requires(Iterator(I))
    readable_bounded_range: I x I
        (f, l) |-> bounded_range(f, l) ^ (forall i in [f, l)) source(i) is defined

    property(I: Readable)
        requires(Iterator(I))
    readable_weak_range: I x DistanceType(I)
        (f, n) |-> weak_range(f, n) ^ (forall i in [[f, n))) source(i) is defined

    property(I: Readable)
        requires(Iterator(I))
    readable_counted_range: I x DistanceType(I)
        (f, n) |-> counted_range(f, n) ^ (forall i in [[f, n))) source(i) is defined

    property(Op: BinaryOperation)
    partially_associative: Op
        op |-> (forall a, b, c in Domain(Op))
                   if op(a, b) and op(b, c) are defined,
                   op(op(a, b), c) and op(a, op(b, c)) are defined
                   and are equal

Given a weak ordering r, we say that a range is **r-increasing** if it is relation preserving with respect to the complement of the converse of r (i.e. adjacent elements i, j of the range satisfy !r(j, i))
Given a weak ordering r, we say that a range is **strictly r-increasing** if it is relation preserving with respect to r (i.e. adjacent elements i, j of the range satisfy r(i, j))
Given a predicate p on the value type of some iterator, a range over that iterator type is called **p-partitioned** if any values of the range satisfying the predicate follow every value of the range not satisfying the predicate
    The first iterator in the range whose value satisfies the predicate is called the **partition point**

    ForwardIterator(T) :=
        Iterator(T)
      ^ regular_unary_function(successor)

The **lower bound** of an r-increasing range with respect to a given value a is the first iterator in that range whose value x satisfies !r(x, a)
The **upper bound** of an r-increasing range with respect to a given value a is the first iterator in that range whose value x satisfies r(a, x)

    IndexedIterator(T) :=
        ForwardIterator(T)
      ^ +: T x DistanceType(T) -> T
      ^ -: T x T -> DistanceType(T)
      ^ + takes constant time
      ^ - takes constant time

    BidirectionalIterator(T) :=
        ForwardIterator(T)
      ^ predecessor: T -> T
      ^ predecessor takes constant time
      ^ (forall i in T) successor(i) is defined implies
                            predecessor(successor(i)) is defined and equals i
      ^ (forall i in T) predecessor(i) is defined implies
                            successor(predecessor(i)) is defined and equals i

    RandomAccessIterator(T) :=
        IndexedIterator(T)
      ^ BidirectionalIterator(T)
      ^ TotallyOrdered(T)
      ^ (forall i, j in T) i < j <=> i precedes j
      ^ DifferenceType: RandomAccessIterator -> Integer
      ^ +: T x DifferenceType(T) -> T
      ^ -: T x DifferenceType(T) -> T
      ^ -: T x T -> DifferenceType(T)
      ^ < takes constant time
      ^ - between an iterator and an integer takes constant time

**Theorem 6.1** For any procedure defined on an explicitly given range of random-access iterators, there is another procedure defined on indexed iterators with the same complexity.
**Proof.** Suppose we are given a range [f, l).  We will show that each of the operations listed in the definition of RandomAccessIterator can be simulated with an IndexedIterator in constant time.

(1) predecessor: given an iterator i in the range [f, l), predecessor(i) is given by f + ((i - f) - 1), where the latter subtraction is over the integer type DistanceType(T)
(2) <: given two iterators i and j in the range [f, l), i < j <=> (i - f) < (j - f), where the latter comparison is over the integer type DistanceType(T)
(3) -: T x DifferenceType(T) -> T: given an iterator i in the range [f, l) and an integer n in DistanceType(T), i - n is the same as f + ((i - f) - n)

Thus we can implement an adapter that, given an IndexedIterator, produces a RandomAccessIterator without any (asymptotic) loss of efficiency.

## Chapter 7

    BifurcateCoordinate(T) :=
        Regular(T)
      ^ WeightType: BifurcateCoordinate -> Integer
      ^ empty: T -> bool
      ^ has_left_successor: T -> bool
      ^ has_right_successor: T -> bool
      ^ left_successor: T -> T
      ^ right_successor: T -> T
      ^ (forall i, j in T) (left_successor(i) = j v right_successor(i) = j) implies !empty(j)

A bifurcate coordinate y is a **proper descendent** of another coordinate x if y is the left or right successor of x, or if it is a proper descend of the left or right successor of x
A bifurcate coordinate y is a **descendent** of a coordinate x if y = x or y is a proper descendent of x
The descendents of x for a **directed acyclic graph** (DAG) if for all y in the descendents of x, y is not its own proper descendent
    x is called the **root** of the DAG of its descendents
    If the descendents of x form a DAG and are finite in number, then they form a **finite** DAG
    The **height** of a finite DAG is one more than the maximum sequence of successors starting from its root, or zero if it is empty
A bifurcate coordinate y is **left reachable** from x if it is a descendent of the left successor of x
A bifurcate coordinate y is **right reachable** if it is a descendent of the right successor of x
The descendents of x form a **tree** if they form a finite DAG and for all y, z in the descendents of x, z is not both left reachable and right reachable from y (i.e. there is a unique sequence of successors from a coordinate to any of its descendents)
Algorithms for traversing DAGs and cyclic structures require **marking**, a way of remembering which coordinates have been previously visited
There are three primary depth-first tree-traversal orders; all three fully traverse the left descendents and then the right descendents
    **preorder** visits to a coordinate occur before the traversal of its descendents
    **inorder** visits to a coordinate occur between the traversals of the left and right descendents
    **postorder** visits occur after traversing all descendents

    BidirectionalBifurcateCoordinate :=
        BifurcateCoordinate(T)
      ^ has_predecessor: T -> bool
      ^ (forall i in T) !empty(i) implies has_predecessor(i) is defined
      ^ predecessor: T -> T
      ^ (forall i in T) has_left_successor(i) implies
            predecessor(left_successor(i)) is defined and equals i
      ^ (forall i in T) has_right_successor(i) implies
            predecessor(right_successor(i)) is defined and equals i
      ^ (forall i in T) has_predecessor(i) implies
            is_left_successor(i) v is_right_successor(i)

    property(C: Readable)
        requires(BifurcateCoordinate(C))
    readable_tree: C
        x |-> (forall y in C) reachable(x, y) implies source(y) is defined

A **concept schema** is a way of describing some common properties of a family of concepts
A concept is a **coordinate structure** if it consists of one or more coordinate types, zero or more value types, one or more traversal functions, and zero or more access functions
Let c = {c1, ..., cn} be a collection of coordinates of a type C, and let d = {d1, ..., dm} be a collection of coordinates of a type D, where C and D belong to the same coordinate structure concept.  We say c and d are **isomorphic** if there is a bijection f from c to d such that for any traversal function t and any element ci, t(ci) is defined if and only if t(f(ci)) is defined, and if whenever both are defined, they are equal
Let c = {c1, ..., cn} and d = {d1, ..., dn} be isomorphic collections of coordinates that have the same value types, and let f be an isomorphism between c and d.  We say that c and d are **equivalent** under given equivalence relations (one per value type) if for any access function a and any element ci, a(ci) is defined if and only if a(f(c)), and if whenever both are defined, they are equivalent under the corresponding equivalence relation
Replacing the equivalence relations on the value types with equality on the value types leads to a definition of equality for collections of coordinates

## Chapter 8

A **linked iterator** type is a forward iterator type for which a **linker object** (an object that, when applied to an iterator, allows the successor of that iterator to be changed)

    ForwardLinker(S) :=
        IteratorType: ForwardLinker -> ForwardIterator
      ^ Let I = IteratorType(S) in:
            (forall s in S) (s: I x I -> void)
          ^ (forall i, j in I) if successor(i) is defined, then
                s(i, j) establishes successor(i) = j

    BackwardLinker(S) :=
        IteratorType: BackwardLinker -> BidirectionalIterator
      ^ Let I = IteratorType(S) in:
            (forall s in S) (s: I x I -> void)
          ^ (forall i, j in I) if predecessor(j) is defined, then
                s(i, j) establishes i = predecessor(j)

    BidirectionalLinker :=
        ForwardLinker(S)
      ^ BackwardLinker(S)

Two ranges are **disjoint** if they include no iterator in common

    property(I: Iterator)
    disjoint: I x I x I x I
        (f0, l0, f1, l1) |-> (forall i in I) !(i in [f0, l0] and i in [f1, l1])

    property(I: Iterator)
    disjoint: I x DistanceType(I) x I x DistanceType(I)
        (f0, n0, f1, n1) |-> (forall i in I) !(i in [[f0, n0]] and i in [[f1, n1]])

A **link rearrangement** is an algorithm taking one or more linked ranges, returning one or more linked ranges, and satisfying the following properties:

    * Input ranges (either counted or bounded) are pairwise disjoint
    * Output ranges (either counted or bounded) are pairwise disjoint
    * Every iterator in an input range appears in an output range
    * Every iterator in an output range appeared in an input range
    * Every iterator in each output range designates the same object as before the rearrangement, and this object has the same value

Note that successor and predecessor relationships that held in the input range might not hold in the output ranges
A link rearrangement is **precedence preserving** if, whenever two iterators i, j in an output range, with i preceding j, came from the same input range, the same precedence relation held in the input range
A sort on a linked range is **stable** with respect to a weak ordering r if, whenever i and j have equivalent values with respect to r but i precedes j in the input range, i precedes j in the output range.

    LinkedBifurcateCoordinate(T) :=
        BifurcateCoordinate(T)
      ^ set_left_successor: T x T -> void
            (i, j) |-> establishes left_successor(i) = j
      ^ set_right_successor: T x T -> void
            (i, j) |-> establishes right_successor(i) = j

    EmptyLinkedBifurcateCoordinate(T) :=
        LinkedBifurcateCoordinate(T)
      ^ empty(T())
      ^ !empty(i) implies left_successor(i) and right_successor(i) are defined
      ^ !empty(i) implies (!has_left_successor(i) <=> empty(left_successor(i)))
      ^ !empty(i) implies (!has_right_successor(i) <=> empty(right_successor(i)))

## Chapter 9

A type is **writable** if a unary procedure sink is defined on it (sink can only be used on the left side of an assignment whose right side evaluates to the corresponding value type):

    Writable(T) :=
        ValueType: Writable -> Regular
      ^ (forall x in T) (forall v in ValueType(T))
            sink(x) <- v is a well-formed statement

A writable object x and a readable object y are **aliased** if sink(x) and source(y) are both defined and if assigning any value v to sink(x) causes it to appear as the value of source(y)

    property(T: Writable, U: Readable)
        requires(ValueType(T) = ValueType(U))
    aliased: T x U
        (x, y) |-> sink(x) is defined ^
                   source(y) is defined ^
                   (forall v in ValueType(T))
                       sink(x) <- v establishes source(y) = v

    Mutable(T) :=
        Readable(T)
      ^ Writable(T)
      ^ (forall x in T) sink(x) is defined <=> source(x) is defined
      ^ (forall x in T) sink(x) is defined <=> aliased(x, x)
      ^ deref: T -> ValueType(T)&
      ^ (forall x in T) sink(x) is defined <=> deref(x) is defined

    property(I: Writable)
        requires(Iterator(I))
    writable_bounded_range: I x I
        (f, l) |-> bounded_range(f, l) ^ (forall i in [f, l)) sink(i) is defined

(similarly for writable_weak_range and writable_counted_range)

    property(I: Mutable)
        requires(ForwardIterator(I))
    mutable_bounded_range: I x I
        (f, l) |-> bounded_range(f, l) ^ (forall i in [f, l)) sink(i) is defined

(similarly for mutable_weak_range and mutable_counted_range)

    property(I: Readable, O: Writable)
        requires(Iterator(I) ^ Iterator(O))
    not_overlapped_forward: I x I x O x O
        (f_i, l_i, f_o, l_o) |->
            readable_bounded_range(f_i, l_i) ^
            writable_bounded_range(f_o, l_o) ^
            (forall k_i in [f_i, l_i), k_o in [f_o, l_o))
                aliased(k_o, k_i) implies k_i - f_i <= k_o - f_o

    property(I: Readable, O: Writable)
        requires(Iterator(I) ^ Iterator(O))
    not_overlapped_backward: I x I x O x O
        (f_i, l_i, f_o, l_o) |->
            readable_bounded_range(f_i, l_i) ^
            writable_bounded_range(f_o, l_o) ^
            (forall k_i in [f_i, l_i), k_o in [f_o, l_o))
                aliased(k_o, k_i) implies l_i - k_i <= l_o - k_o

    property(I: Readable, O: Writable)
        requires(Iterator(I) ^ Iterator(O))
    not_overlapped: I x I x O x O
        (f_i, l_i, f_o, l_o) |->
            readable_bounded_range(f_i, l_i) ^
            writable_bounded_range(f_o, l_o) ^
            (forall k_i in [f_i, l_i), k_o in [f_o, l_o))
                !aliased(k_o, k_i)

    property(I: Readable, O: Writable)
        requires(Iterator(I) ^ Iterator(O))
    not_overlapped_reverse_forward: I x I x O x O
        (f_i, l_i, f_o, l_o) |->
            readable_bounded_range(f_i, l_i) ^
            writable_bounded_range(f_o, l_o) ^
            (forall k_i in [f_i, l_i), k_o in [f_o, l_o))
                aliased(k_o, k_i) implies l_i - k_i <= k_0 - f_o

    property(I: Readable, O: Writable)
        requires(Iterator(I) ^ Iterator(O))
    not_overlapped_reverse_backward: I x I x O x O
        (f_i, l_i, f_o, l_o) |->
            readable_bounded_range(f_i, l_i) ^
            writable_bounded_range(f_o, l_o) ^
            (forall k_i in [f_i, l_i), k_o in [f_o, l_o))
                aliased(k_o, k_i) implies k_i - f_i <= l_o - k_o

    property(T: Writable, U: Writable)
        requires(ValueType(T) = ValueType(U))
    write_aliased: T x U
        (x, y) |-> sink(x) is defined ^ sink(y) is defined ^
                   (forall V in Readable) (forall v in V)
                     aliased(x, v) <=> aliased(y, v)

    property(O_0: Writable, O_1: Writable)
        requires(Iterator(O_0) ^ Iterator(O_1))
    not_write_overlapped: O_0 x O_0 x O_1 x O_1
        (f_0, l_0, f_1, l_1) |->
            writable_bounded_range(f_0, l_0) ^
            writable_bounded_range(f_1, l_1) ^
            (forall k_0 in [f_0, l_0))
            (forall k_1 in [f_1, l_1))
                !write_aliased(k_0, k_1)

    property(I: Readable, O: Writable, N: Integer)
        requires(Iterator(I) ^ Iterator(O))
    backward_offset: I x I x O x O x N
        (f_i, l_i, f_o, l_o, n) |->
            readable_bounded_range(f_i, l_i) ^
            n >= 0 ^
            writable_bounded_range(f_o, l_o) ^
            (forall k_i in [f_i, l_i))
            (forall k_o in [f_o, l_o))
                aliased(k_o, k_i) implies
                    k_i - f_i + n <= k_o - f_o

    property(I: Readable, O: Writable, N: Integer)
        requires(Iterator(I) ^ Iterator(O))
    forward_offset: I x I x O x O x N
        (f_i, l_i, f_o, l_o, n) |->
            readable_bounded_range(f_i, l_i) ^
            n >= 0 ^
            writable_bounded_range(f_o, l_o) ^
            (forall k_i in [f_i, l_i))
            (forall k_o in [f_o, l_o))
                aliased(k_o, k_i) implies
                    l_i - k_i + n <= l_o - k_o

##  Chapter 10

A transformation f is an **into** transformation if, for all x in its definition space, there exists a y in its definition space such that y = f(x)
A transformation f is an **onto** transformation if, for all y in its definition space, there exists an x in its definition space such that y = f(x)
A transformation f is a **one-to-one** transformation if, for all x, x’ in its definition space, f(x) = f(x’) implies x = x’
A **fixed point** of a transformation is an element x such that f(x) = x
An **identity transformation** is one that has every element of its definition space as a fixed point
    We denote the identity transformation on a set S as identity_S
A **permutation** is an onto transformation on a finite definition space
A **cycle** is a circular orbit within a permutation
A **trivial cycle** is a cycle with one element (the element in a trivial cycle is a fixed point)
A permutation containing a single nontrivial cycle is called a **cyclic permutation**
A **transposition** is a cyclic permutation with a cycle size of 2
A **finite set** S of size n is a set for which there exists a pair of functions

    choose_S: [0, n) -> S
     index_S: S -> [0, n)

satisfying

    choose_S(index_S(x)) = x
    index_S(choose_S(i)) = i

If p is a permutation on a finite set S of size n, there is a corresponding **index permutation** p’ on [0, n) defined as:

    p’(i) = index_S(p(choose_S(i)))

A **rearrangement** is an algorithm that copies the objects from an input range to an output range such that the mapping between the indices of the input and output ranges is a permutation
    In a **position-based rearrangement**, the destination of a value depends only on its original position and not on the value itself
    In a **predicate-based rearrangement**, the destination of a value depends only on the result of applying a predicate to the value
    In an **ordering-based arrangement**, the destination of a value depends only on the ordering of values
A **mutative rearrangement** is a rearrangement in which the input and output ranges are identical; every mutative rearrangement corresponds to two permutations:
    (1) a **to-permutation** that maps an iterator i to the iterator j that points to the destination of the element at i
    (2) a **from-permutation** that maps an iterator j to the iterator i that points to the origin of the element moved to j
A **memory-adaptive** algorithm uses as much additional space as it can acquire to maximize performance
The permutation p of n elements defined by an index permutation p(i) = (i + k) mod n, where we define (i + k) mod n to be the unique integer in [0, n) that is congruent to i + k (mod n), is called the **k-rotation**

## Chapter 11

A partition rearrangement is **stable** if the relative order of elements not satisfying the predicate is preserved, as is the relative order of elements satisfying the predicate
A partition rearrangement is **semistable** if the relative order of elements not satisfying the predicate is preserved

    property(I: ForwardIterator, N: Integer, R: Relation)
        requires(Mutable(I) ^ ValueType(I) = Domain(R))
    mutable: I x N x I x N x R
        (f0, n0, f1, n1, r) |-> f0 + n0 = f1 ^
            mutable_counted_range(f0, n0 + n1) ^
            weak_ordering(r) ^
            increasing_range(f0, n0) ^
            increasing_range(f1, n1)

A merge is **stable** if the output range preserves the relative order of equivalent elements both within each input range and between the first and second input range
A sorting algorithm is **stable** if it preserves the relative order of elements with equivalent values
An iterator i in a range is a **pivot** if its value is not smaller than any value preceding it and not larger than any value following it

    Linearizable(W) :=
        Regular(W)
      ^ IteratorType: Linearizable -> Iterator
      ^ ValueType: Linearizable -> Regular
            W |-> ValueType(IteratorType(W))
      ^ SizeType: Linearizable -> Integer
            W |-> DistanceType(IteratorType(W))
      ^ begin: W -> IteratorType(W)
      ^ end: W -> IteratorType(W)
      ^ size: W -> SizeType(W)
            x |-> end(x) - begin(x)
      ^ empty: W -> bool
            x |-> begin(x) == end(x)
      ^ []: W x SizeType(W) -> ValueType(W)&
            (w, i) |-> deref(begin(x) + i)

A **container** is a sequence that owns its elements; a linearizable type is not necessarily a container
An object is a **composite object** if it is made up of other objects, called its **parts**; the whole-part relationship satisfies the following properties:
    (1) **connectedness**: an object has an affiliated coordinate structure that allows every part of the object to be reached from the object’s starting address
    (2) **noncircularity**: an object is not a subpart of itself, where **subparts** of an object are its parts and subparts of its parts
    (3) **disjointness** means that if two objects have a subpart in common, one of the two is a subpart of another
    (4) **ownership** means that copying an object copies its parts, and destroying an object destroys its parts
[Note that B might be reachable from A’s starting address even though B is not a subpart of A]
A composite object is **dynamic** if the set of its parts could change over its lifetime

    Sequence(S) :=
        Linearizable(S)
      ^ (forall s in S) (forall i in [begin(s), end(s)))
            deref(i) is a part of s
      ^ =: S x S -> bool
            (s, s’) |-> lexicographical_equal(begin(s), end(s), begin(s’), end(s’))
      ^ <: S x S -> bool
            (s, s’) |-> lexicographical_less(begin(s), end(s), begin(s’), end(s’))

    property(I: Readable, F: UnaryFunction)
        requires(Domain(F) = I)
    projection_regular_function: F
        f |-> (forall i, j in I) source(i) = source(j) implies f(i) = f(j)

A part is **remote** if it does not reside at a constant offset from the address of an object but must be reached via a traversal of the object’s coordinate structure starting at its **header**
The header of a composite object is the collection of its **local** parts