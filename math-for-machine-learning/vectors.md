# Vectors

## Machine Learning Context

- feature extraction into vectors and matrices
- modeling uses geometry/norms or probability/statistics
- optimization uses vector calculus and numerical methods to do gradient decent

## Definitions

"data structure of machine learning"

- vector
  - types
    - column vectors: vertical list of numbers (notated `v` with an arrow over it)
    - row rectors: horizontal list of numbers (notated `W` with an arrow over it)
  - dimension
    - number of elements in the vector
- matrix
  - `m*n` matrix has `m` rows and `n` columns
    - `a_1,1` is top left
    - `a_m,n` is bottom right
    - can be viewed as a collection of either row of column vectors

## Operations

- vector addition: element-wise addition of the items, constraint that they are the same length
  - "zero vector" can be added to anything for identity property
- scalar multiplication: element-wise multiplication by a real number
  - any vector \* 0 will give zero vector
  - any vector \* 1 will be identity
- transpose: flip indices (flip over diagonal) `a_m,n` matrix transposed will be of dimension `n,m`

## Geometry of Column Vectors

- not just lists of numbers, but can represent a direction in space
- `a = [3, 2, 1]` can represent a direction where change in x = 3, change in y = 2, change in z = 1
  - direction, not a point since can start anywhere
  - addition is concatenation of the two vectors
- subtraction is mapping
  - `w = (w-v) + v`: `w-v` is the vector that goes from `v` to `w`

## Magnitude of Vectors

- Norm: a measure of distance
  - axiom 1: all distances (lengths) are non negative
  - axiom 2: distances multiply with scalar multiplication
  - axiom 3: A to B then B to C is at least as far as A to C
    - `||v + w|| <= ||v|| + ||w||`
    - can be equal if A, B, C are all on the same line

**Euclidean Norm**

- `||v|| = sqrt(v_1^2 + ... + v_n^2)`
- `||[3,4]||` = sqrt(9+16) = 5

**L_p Norm**

- `||v|| = 1/p root(|v_1|^p + ... + |v_n|^p)`
- absolute value so odd values of `p` don't make things negative
- all axioms hold for p >= 1
- why?

**L_1 Norm**

- simplifies it to the sum of absolute values of each element
- geometric meaning "taxi cab metric", "manhattan norm"
  - L_2 norm gives distance as the crow flies in two dimensions
  - L_1 norm gives distance "along the grid" if you can only go left/right or up/down at a time

**L_infinity Norm**

- doesn't make sense, but actually means limit as `p` approaches infinity
- approaches length of longest dimension of the vector since that value dominates
- can be used for worst case analysis in machine learning - how much can I be off?

**L_zero Norm**

- not actually a norm since doesn't abide by multiplication axiom
- number of non-zero elements of a vector
- result is the limit as `p` approaches 0 of an L_p norm
- used to measure sparsity of vectors since that is helpful in ML

## Geometry of Norms

- for a variety of norms, what is the set of vectors where the norm equal to one?
  - Euclidean: circle
    - circle of radius 1 around the origin
    - includes (sqrt(0.5), sqrt(0.5)) approx (0.7, 0.7)
  - L_1: diamond inside circle
    - `v_1 + v_2 = 1`, `v_2 = 1 - v_1`
    - set of points from the origin to ending on the line between (0,1) and (1,0)
    - includes (0.5, 0.5)
  - L_infinity: square outside circle
    - at least one of v_1, v_2 has to be 1, and then other has to be <= 1
