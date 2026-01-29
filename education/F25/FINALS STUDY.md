## EECS → need 85% final (for B-) or 70% to pass
- LECTURES 12 → onward
- ~~REVIEW SESSION VIDEO/NOTES~~
- HOMEWORKS 5 → onwards
- FINAL EXAMPLE → look for topics
- DISCUSSIONS 7 → onwards

Review
- Strictly Increasing Functions: $mx+b, x^3, e^x, ln(x),$ and $\sqrt{x}$
- Gradient → derivative of each variable
- Hessian → two gradients
- Affine Set → infinitely flat (is it linear?)
- Positive Semi-Definite → $A⪰0$ and convex (multiple convex points), used in Second-Order
	- if all eigenvalues of A are non-negative ($\lambda_i \ge 0$)
	- the scalar value $x^TAx$ is always non-negative ($x^TAx≥0$)
- Positive Definite → $A≻0$ and strictly convex (only one convex point)
- Indefinite → saddle point and non-convex
	- Difference between PSD and PD is PSD is equal to and PD is not
- $\nabla x^Tx =$ $\nabla$Euclidean Norm = $\nabla ||x||_2^2$ = $\nabla(x_1^2+ x_2^2+ x_3^2 + x_4^2)$ is equivalent to $2x$
-  $\nabla (-\lambda 1^Tx) = -\lambda 1$ 

Convexity → used to prove that any two points in a shape will never leave the shape
- Slater’s Condition → guarantee strong duality → basically if feasible based on constraints
	- one feasible point $x$ that is strictly inside the inequality constraints
		- inequality constraints: $g_i(x) \le 0$, there must be a point where $g_i(x) < 0$
		- equality constraints: $h_i(x) = 0$ needs to be affine
- Convex Sets
	- Linear Programming (LP): convex combination $αx^{(1)} + (1 − α)x^{(2)} ∈ C$
	- Quadratic Programming (QP): linear constraints and quadratic objective function
		- $f(x)=\frac{1}{2}x^TPx+q^Tx+r$ ← quadratic function
	- Quadratically Constrained Quadratic Program (QCQP): the constraints and objective functions are both quadratic functions
	- Convex Hull: smallest possible convex set that contains all the data points
	- Union Sets: unions of convex sets are convex
- Convex Functions
	- always use the highest order first
	- use orders to prove convex or not
	-  $x^2$, $|x|$, and $-log$ are convex functions
	- Zeroth-Order: $f(αx + (1 − α)y) = αf(x) + (1-α)f(y)$
		- use if not differentiable like $max(x), |x|, sine(x), ||x|| \space or \space x^{1/3}$
	- First-Order (once differential): $f(y) ≥ f(x) + ∇f(x)^T(y-x)$
	- Second-Order (twice differential): $∇^2 f(x) ≥ 0$  
		- hessian has to be positive semi-definite
	- non-negative weighted sums
		- $5(x_1​−10x_2​)^4−7log(x_1​−x_2​+1)$
		- weights are 5 and 7, convex functions are $x^4$ and $-log(x)$ so the function is convex

Convex Optimization
- The problem
	$min \space f(x)$ 
	$s.t. \space x ∈ X$ 
- is a convex function if *f* is convex function and *X* is a convex set
	$min \space f(x)$ 
	$s.t. \space h_i (x) = 0$ → is convex if *h* is affine → equality constraints
	   $g_i (x) ≤ 0$ → is convex if *g* is convex → inequality constraints
- Implications
	- all local minima of a convex optimization problem are also a global minima ← the point of convex functions
	- if convex problem is feasible and strictly convex obj function, then it is a unique solution
- Solutions
	- $\mu$ = multipliers for equality constraints
	- $\lambda$ = multipliers for inequality constraints
	- Before we solved unconstrained convex problems
		1.  2nd derivative test or positive semi-definite Hessian
		2. then x is global minimum iff gradient f(x) = 0 (first derivative)
	- Now constrained convex problems
		1. verify convexity
			1. f is convex
			2. h is affine
			3. g is convex
			4. Check Slater’s condition
		2. x is a global minimum iff there exists multipliers $\mu$ and $\lambda \ge 0$ (Lagrange Multipliers)
			- KKT Conditions (lecture 21)
				1. Primal Feasibility → $h_i(x) = 0$ ← The candidate $x$ must satisfy the original constraints.
				2. Primal Feasibility → $g_i(x) = 0$ ← The candidate $x$ must satisfy the original constraints.
				3. Dual Feasibility → $\lambda_i \ge 0$ ← The multipliers for inequality constraints must be non-negative.
				4. Complementary Slackness → $\lambda_i g_i(x) = 0$ ← For every inequality constraint, either the constraint is active (equals 0) or the multiplier is zero
				5. Lagrangian Stationarity → $∇f(x) + ∑ μ_i∇h_i(x) + ∑ λ_i∇g_i(x) = 0$
	- **Two Types of KKT (TYPE 2 MOST IMPORTANT)**
		1. given $x^*$, check whether it is a global minimum (hw8 #1)
			1. take the gradient of every constraint
			2. then check every constraint against the KKT conditons
		2. use KKT Conditions to derive the set of global minima (hw8 #2&3)
			- tricks to solve KKT with weird constraints
				1. reorganize the constraints then do edge cases
				2. two

Optimization Techniques
- Epigraphs
	- introduce temporary variables to reorganize the objective function
	- example
		- absolute value
			$min \space 3|x|+2x+5$ → convert to
			$min \space 3t+2x+5$
			$x-t \le 0$
			$-x-t \le 0$
		- max functions
			$min \space max \space (x_i)$ → convert to
			$min \space t$
			$x_i \le t$ for all i
	- 
- LP Standard Form **(hw7 #1)**
	- LP is where the objective function and all constraints are linear (affine)
	- If LP is not in standard form introduce slack variables
		- $Ax \le b$ → $Ax + s = b, s\ge 0$
		- $x = x^+ - x^-$ where $x^+, x^- \ge 0$
	- example
		$max \space 2x_1 + x_2$
		$s.t. \space x_1 + x_2 \le 10$
		$x_1 \ge 0, x_2 \space free$ → convert to
		$min \space -2x_1 - x_2$
		$x_1 + x_2 + s_1 = 10$ when $s_1 \ge 0$
		make $x_2$ not free → $x_2 = x_2^+ -x_2^-$
		$min \space -2x_1 - (x_2^+ -x_2^-)$
		$s.t. \space x_1 + (x_2^+ -x_2^-) + s_1 = 10$
		$x_1, x_2^+, x_2^-, s_1 \ge 0$

- Convex Relaxations
	- when the constraint is $x \in \{{0, 1}\}$ when $min \space x^2 -0.5x$
	- relax $x \in \{{0, 1}\}$ → $0 \le x \le 1$
	- in Integer Programming (IP) → check floor and ceiling values to get a range

Duality
- Lagrangian: $L(x, \mu, \lambda) = f(x) + \sum \mu_i h_i (x) + \sum \lambda_i g_i (x)$
	- $\mu$ = multipliers for equality constraints
	- $\lambda$ = multipliers for inequality constraints
- Dual Function is minimizing Lagrangian
	- $d(\mu, \lambda) = min \space L(x, \mu, \lambda)$
- Weak Duality → the optimal value of the dual is less than or equal to the optimal value of the primal
	- provides a floor to the solution
- Strong Duality → the optimal values are equal
	- happens when the problem is convex and satisfies Slater’s conditions
- Infeasibility Certificates
	- a proof that the optimization problem has no solution\
	- using the dual, make x disappear and find values of $\tilde{\mu}$ and $\tilde{\lambda}$  that make $d(\tilde{\mu}, \tilde{\lambda}) > 0$. if $> 0$, then the problem is infeasible or an empty set

Primal/Duality (linear programming)
- Weak Duality/Strong Duality
- Slater’s Conditions
- KKT Conditions
	- Lagrangian stationarity
	- Primal Feasibility
	- Dual Feasibility
	- Complementary Slackness
- Convex Optimizations
- QCQP (Quadratically Constrained Quadratic Program)
- LP Relaxation
	- example ← uses both Epigraphs & Relaxations
		$min \space ||x||_1$
		s.t. $Ax=b$
		  $x_i \in \{-1, 0, 1\}$ for $i = 1, 2, ... , n$
		1. Relax the Discrete Constraints
			- ${-1, 0 , 1}$ → continuous interval → $[-1, 1]$ or $-1 \le x_i \le 1$ for $i = 1, 2, ..., n$
		2. Linearize the L1/L2-Norm Objective
			- $||x||_1 = \sum_{i=1}^n |x_i|$
				- $min \space \sum_{i=1}^n u_i$
				- $x_i - u_i\le 0$ for $i = 1,2, ... ,n$
				- $-x_i - u_i\le 0$ for $i = 1,2, ... ,n$
			- $||x||_\infty = max_i|x_i|$
				- $min \space s$
				- $x_i - s\le 0$ for $i = 1,2, ... ,n$
				- $-x_i - s\le 0$ for $i = 1,2, ... ,n$
			- $||x||_2 = \sum_{i=1}^n (x_i)^2$ ← cannot linearize
		3. Formulate the LP Relaxation
			$min \space \sum_{i=1}^n u_i$
			s.t. $Ax=b$
			  $x_i \le u_i$ for $i = 1,2, ... ,n$
			  $-x_i \le u_i$ for $i = 1,2, ... ,n$
			  $-1 \le x_i \le 1$ for $i = 1,2, ... ,n$
- Finding Primal/Dual using Lagrangian Multipliers
	$L(x, λ) = c⊤x + λ(x⊤Ax − 1)$
	To find dual function is to minimize Lagrangian

HW#8



## IEOR → need 85% final (for B+) or 60% to pass
- DISCUSSION 7 → onwards
- HOMEWORK → 
- FINAL EXAMPLE

Review
- Linear Programming
	- no strict inequalities ($< or >$)
	- cannot be quadratic/trig/multiplicative variables only linear
	- feasibility
		- feasible: satisfies all constraints
		- feasible region: all points that satisfies the constraints
		- optimal solution: the best points in the feasible region for the objective value
		- feasible problem: meaning has at least one feasible solution
			- minimize problem: find best upper bound
			- maximize problem: find best lower bound
		- infeasible: at least one constraint is unsatisfied
		- unbounded: objective function can be proved indefinitely
	- auxiliary variables: temporary variables
		- all equivalent
		- $min \space x$<br>$s.t. \space 2x \ge 1$ 
		- $min \space x$<br>$s.t. \space 2x-s = 1$<br>$s \ge 0$
		- $min \space x$<br>$2x+s = 1$<br>$s \le 0$
	- absolute values → replace the absolute value with a new variable, only works with minimization problems
		- in constraints
			- $min \space 3x$
			  $s.t. |x| \le 5$
			- $min \space 3x$
			  $x \le 5$
			  $x \ge -5$
		- in objective function
			- approach 1
				- $min \space 2x_1 + 3|x_2|$
				  $s.t. x_1 + x_2 \le 3$
				- $min \space 2x_1 + 3z$
				  $x_1+x_2 \le 3$
				  $-z-x_2 \ge 0$
				  $x_2 - z \le 0$
			- approach 2
				- $min \space 2x_1 + 3|x_2|$
				  $s.t. x_1 + x_2 \le 3$
				- $min \space 2x_1 + 3(z^++z^-)$
				  $s.t. x_1 + x_2 \le 3$
				  $x_2 = z^+-z^-$
				  $z^+ \ge 0$
				  $z^- \ge 0$
	- $max \space f(x)$ = $min \space -f(x)$

- Graphical Method → plot every constraint on a graph to help find objective value
- Sensitivity Analysis ← check limiting constraints
	- $min \space 40x_1 + 50x_2$
	  $s.t. 2x_1 + 3x_2 \ge 30$
	  $x_1 + x_2 \ge 12$
	  $2x_1 + x_2 \ge 20$
	  $x_1, x_2 \ge 0$
	- if objective function same slope as constraint, then infinitely many solutions
	- $min \space 2x_1 + 3x_2$
	  $s.t. 2x_1 + 3x_2 \ge 30$
	  $x_1 + x_2 \ge 12$
	  $2x_1 + x_2 \ge 20$
	  $x_1, x_2 \ge 0$
	- if objective function changes to $C_1$
		- $min \space c_1x_1 + 50x_2$
		  $s.t. 2x_1 + 3x_2 \ge 30$
		  $x_1 + x_2 \ge 12$
		  $2x_1 + x_2 \ge 20$
		  $x_1, x_2 \ge 0$
		- given the objective value (7.5, 5), the values are limited by constraint 1 and constraint 3 ← check graphical graph
		- constraint 1 slope: -2/3, constraint 2 slope: -2
			- $-2 \le \frac{-c_1}{50} \le \frac{-2}{3}$, so any value between $\frac{100}{3}$ and 100 lets the optimal solution stay (7.5, 5)
	- Shadow Price: how much does one unit of change in the RHS affect the objective function
		- shadow price is zero for all non-binding constraints
- Simplex Method (using Tableau)
	- Non-Basic Variables (NBV): any variable equals zero
	- Basic Variables (BV): anything not equal to zero
	- Build a table and select the column with the biggest negative number when setting the objective function to Z
	- Degenerate: when one of the basic variables is equal to zero
- Primal / Dual
	- Primal → n variables, m constraints
	  $\sum_{j=1}^{n}c_j x_j$
	  s.t. $\sum_{j=1}^{n} a_{ij} x_j \le b_i$ for $i = 1, 2, ..., m$
	  $x_j \ge 0$ for $j = 1, 2, ... n$
	- Dual → m variables, n constraints
	  $\sum_{i=1}^{m}b_i y_i$
	  s.t. $\sum_{i=1}^{m} a_{ij} y_i \ge c_j$ for $j = 1, 2, ..., n$
	  $y_i \ge 0$ for $i = 1, 2, ... m$
	- Finding Dual Linear Program in Non-Standard Form
		- $min \space 3x_1 + 5x_2 + 4x_3$
		  s.t. $x_1 + 3x_2 + x_3 \le 8 \space (y_1)$ → $-x_1 - 3x_2 - x_3 \ge -8$
		  $2x_1 + x_2 - 2x_3 = 5 \space (y_2)$
		  $3x_1 - 2x_2 + 4x_3 \ge 7 \space (y_3)$
		  $x_1, x_2 \ge 0, x_3 \space free$
		- Method A
			- First Transform to Standard Form
			- $max \space -3x_1 - 5x_2 - 4(x_3^+ - x_3^-)$
			  s.t. $x_1 + 3x_2 + (x_3^+ - x_3^-) \le 8 \space (y_1)$
			  $2x_1 + x_2 - 2(x_3^+ - x_3^-) \le 5 \space (y_2)$
			  $-2x_1 - x_2 + 2(x_3^+ - x_3^-) \le -5 \space (y_3)$
			  $-3x_1 + 2x_2 - 4(x_3^+ - x_3^-) \ge -7 \space (y_4)$
			  $x_1, x_2, x_3^+,x_3^- \ge 0$
			- Dual
			  $min \space 8y_1 + 5y_2 + -5y_3 - 7y_4$
			  s.t. $y_1 + 2y_2 -2y_3-3y_4 \ge -3$
			  $3y_1 + y_2 - y_3 + 2y_4 \ge -5$
			  $y_1 - 2y_2 + 2y_3 - 4y_4 \ge -4$
			  $-y_1 + 2y_2 - 2y_3 + 4y_4 \ge 4$
			  $y_1, y_2, y_3, y_4 \ge 0$
		- Method B ← this way better
			- $max \space -8y_1 + 5y_2 + 7y_3$
			  s.t. $-y_1 + 2y_2 + 3y_3 \le 3$
			  $-3y_1 + y_2 - 2y_3 \le 5$
			  $-y_1 -2y_2 + 4y_3 = 4$ ← since $x_3$ is free
			  $y_1, y_2 \space free, y_3 \ge 0$
![[Screenshot 2025-12-12 at 1.39.43 PM.png]]
- Duality Rules

| Case | Primal                                    | Dual                                      |
| ---- | ----------------------------------------- | ----------------------------------------- |
| 1    | Feasible with finite optimal objective    | Feasible with finite optimal objective    |
| 2    | Feasible with unbounded optimal objective | Infeasible                                |
| 3    | Infeasible                                | Feasible with unbounded optimal objective |
| 4    | Infeasible                                | Infeasible                                |

- Weak Duality → feasible solution in Primal is also feasible for Dual
- Strong Duality →  optimal solution to Primal and optimal solution to Dual
- Complementary Slackness
	- solving the optimal solution by using graphical method and corner points
- Standard Form
	- convert $max \space f(x)$ = $min \space -f(x)$
	- all less than or equal to inequality constraints
	- no unrestricted/free variables
- Integer Programming Formulation
	- linear programming but their cannot be decimal points or fractions so the programming is always whole numbers like pilots, no such thing as 1.5 pilots
- Complementary Slackness Theorem ← similar to eecs definition
	- Primal Variable $X$ Dual Slack = 0
	- Dual Variable $X$ Primal Slack = 0

Linearizing Objective Functions
- Absolute Values
	- $min \space |x|$ → $min \space max \space \{x, - x\}$ ← no linear
	- $z=|x|$ → $z = (x^+ - x^-)$ and $x^+,x^- \ge 0$


Branch and Bound ← used for integer programming
- only work for MAXIMIZATIONS problems only ← so convert min to max if needed
- general idea is to solver integer programming by dividing the feasible region of the IP into smaller regions, then solve the LP-Relaxation of the problem for each sub-region
- Upper Bound → LP-relaxation of an IP will have a better optimal objective function value than the optimal IP
	- LP-relaxation: remove integer constraints
	- when having more constraints, leads to smaller feasible region
- Lower Bound → any feasible region solution of an IP will have a worse objective function value than the optimal solution of the IP
- Branch all non-integer variables floor/ceiling whole numbers then redo the optimizations with new constraints
	- $x^* = (2, \frac{7}{5})$ → $x_2 \le 2$ and $x_2 \ge 3$, then find optimal values
	- if new variables are integers branch again, but check if new programming is feasible, if infeasible then Fathomed

Knapsack
- Decision Variables
	$x_i$ → 1 if packed item $i$
	  0 otherwise
- IP Formulation
	values → $4x_1 + 2x_2 + x_3 + 7x_4 + 3x_5 + 6x_6$
  weights → $5x_! + 8x_2 + 8x_3 + 6x_4 + x_5 + 5x_6 \le 15$
  $x_i \in \{0, 1\}$ $\forall i = \{1, ... , 6\}
- Greedy Algorithm: choose the items with the greatest value per weight first
- $x^* = (0.6, 0, 0, 1, 1, 1)$ ← not integer programming
- start branching $x^* = 0.6$ to $x_1 \le 0$ and $x_1 \ge 1$

Network Flow
- edges are undirected
- arcs are directed
- Circulation Arc: from sink node to source node
	- used when supply and demand are not known (model choose total amount of flow) or unbalanced (produced to much)
- Dump Node: used when supply and demand are unbalanced
- MCNF (minimum-cost network flow)
	- Transportation (quantities)
	- Assignment (binary)

Shortest Paths ← source node s to every other node
- Dijkstra’s Algorithm
	- non-negative edge weights
	- node by node and look at the outgoing edges, then update the edges as progress through nodes
- Dynamic Programming
	- only works on DAGs (no cycles)
	- can work with negative edge weights
	- topological order
	- update one node at a time by looking at all incoming edges for the node in topological order

Project Management (CPM)
- EFT = EST + duration
- EST = MAX(EFT of all predecessors)
- Critical Path Method
	- zero slack → EST = LST and EFT = LFT

Sensitivity Analysis
Simplex Tableau Algorithm
Cutting Planes
- rubber band around integer points in graphical method
Minimum Maximum Problems
Project Management Expediting



## CS → 0.5 SD above average
- LECTURES
- HOMEWORKS
- FINAL EXAMPLES (spam)

Review
- Big O Notation
	- Big O → grows no faster than the given function ← upper bound
	- Big $\Omega$ → grows at least as fast as the given function ← lower bound
	- Big $\Theta$ → grows at the same rate as the given function ← equal
- **Recurrence Relations** (Masters Theorem)
	- $T(n) = aT(\frac{n}{b}) + O(n^d)$
	- geometric finite sum: $a+ar+ar^2+...+ar^{n-1}=\frac{a(1-r^n)}{1-r}$
	- Master Theorem
		- only works if in form $T(n) = aT(\frac{n}{b}) + O(n^d)$
		- $T(n)$ → $O(n^d)$ if $d > log_ba$
				$O(n^dlogn)$ if $d = log_ba$
				$O(n^{log_ba})$ if $d < log_ba$
- Divide-and-Conquer
	- 
- Dynamic Programming
	- Bellman-Ford → Dijkstra with negative edges, shortest path from s to all nodes
- Ford-Fulkerson
	- a
- Traveling Salesman
	- a
- Knapsack
	- a
- Zero-Sum Games
	- a
- Huffman Encoding
	- a
- Linear Programming
	- a
- Network Flow
	- a
- Boba Shop
	- a
- Complexity Classes ← insert visual image
	- P: solvable in polynomial time
	- NP: solutions are verifiable in polynomial time
	- NP-Hard: at least as hard as the hardest problem in NP
		- If problem A is NP-Hard, every problem in NP can be reduced to problem A
	- NP-Complete: problem in NP that all problems in NP can reduce to
![[Screenshot 2025-12-11 at 1.15.07 PM.png]]

Reductions
- reducing a hard problem we do not know how to solve into a different problem that we know how to solve
NP-Completeness
- 
Approximation Algorithms
- Vertex Cover Approximation
	1. Find maximal matching M
	2. Return endpoints of all edges in M
- Vertex Cover is NP-HARD
Randomized Algorithms
- Las Vegas
	- Correctness is guaranteed
	- Runtime is random
	- Goal
		- Analyze its expected worse-case runtime: T(n) = m
		- Show that runtime is low with high probability
	- QuickSelect
		- pick a random pivot, a pivot can be good or a bad with probability $\frac{1}{2}$
	- One Sided Error ← right based on its outcome
		- If answer is Yes, then ALG always output Yes
		- If answer is NO, then algo outputs No with probability $p > 0$
		- To get a probability 0.999 of success, we have the following
			- for i in range(10/p):
				- if ALG == NO, return NO
			- return Yes
	- Two Sided Error ← could be wrong based on its outcome
		- ALG outputs the correct answer with probability $\frac{1}{2}$ + eps
		- To get probability 0.999 of success, we have the following
			- 
- Monte Carlo
	- Correctness is random
	- Runtime is bounded
	- Primality Testing
		- given a number N, is it a prime number?
		- Fermat’s Little Theorem
	
- Karger’s Algorithm
	- 
- Markov’s and Chebyshev’s Inequality
Online Algorithms
- Randomized Weighted Majority (Multiplicative Weights)
	- 
Quantum Computing
- 
## DATA → just do good
- NOTEBOOKLM
- study linking AUTHORS to TITLES to ONE SENTENCE SUMMARIES

Review
- Week 1
- Week 2
- Week 3
- Week 4
- Week 5
- Week 6
- Week 7
- Week 8
- Week 9
- Week 10
- Week 11
- Week 12
- Week 13
- Week 14
