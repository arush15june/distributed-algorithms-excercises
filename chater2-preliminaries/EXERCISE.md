# Chapter 2 - Preliminaries - Exercises

## Exercise 2.1
```math
\text{ For eac h of the following functions} f \text{and} g, \text{say whether } f \in O(g) \text{ and/or } g \in O(f).\\  
\text{(a) } f(n) = 5n^2 + 3n + 7 \text{ and } g(n) = n^3 \\ 
\text{(b) } f(n) = \sum^{n}_{i=1} i \text{ and } g(n) = n^2 \\ 
\text{(c) } f(n) = n^n \text{ and } g(n) =  n! \\
\text{(d) } f(n) = nlog_2n \text{ and } g(n) =  n\sqrt{n/2} \\
\text{(e) } f(n) = n + nlog_2n \text{ and } g(n) =  n\sqrt{n} \\
```
```math
f \in O(g) \text{ if, for some } c \in \mathbb{R}_{>0}, f(n) \leq cg(n) \text{ for all } n \in \mathbb{N}
```

(a)
```math
f(n) = 5n^2 + 3n + 7\\ g(n) = n^3 \\
```
```math
f \in O(g) \text{ as }\\
5n^2 + 3n + 7 \leq c.n^3\\
```
```math
g \notin O(f) \text{ as }\\
n^3 \nleq c.(5n^2 + 3n + 7)\\
```

(b)
```math
f(n) = \sum^{n}_{i=1} i \\ 
```
```math
g(n) = n^2 \\
f(n) = n(n+1)/2 = {\frac{n^2}2} + \frac{n}2\\
```
```math
f \in O(g) \text{ as }\\
{\frac{n^2}2} + \frac{n}2 \leq c.n^2\\
```
```math
g \in O(f) \text{ as }\\
n^2 \leq c.({\frac{n^2}2} + \frac{n}2)\\
```

(c)
```math
f(n) = n^n = n*n*n*...*n \\ 
g(n) = n! = n*(n-1)*(n-2)*...*1 = n^n - \frac{n(n+1)}2 \\
```
```math
f \notin O(g) \text{ as }\\
n^n \nleq c.(n^n - \frac{n(n+1)}2) \\
```
```math
g \in O(f) \text{ as }\\
n^n - \frac{n(n+1)}2 \leq c.(n^n) \\
```

(d)
```math
f(n) = nlog_{2}n \\
g(n) =  n\sqrt{\frac{n}2}\\
```
```math
f \notin O(g) \text{ as }\\
nlog_{2}n \nleq c.(n\sqrt{\frac{n}2}) \\
log_{2}n \nleq c.(\sqrt{\frac{n}2}) \\
```
```math
g \in O(f) \text{ as } \\
\sqrt{\frac{n}2} \leq c.(log_{2}n) \\
```

(e)
```math
f(n) = n + nlog_2n \\
g(n) =  n\sqrt{n}\\
```
```math
f \notin O(g) \text{ as }\\
n + nlog_2n \nleq c.(n\sqrt{n}) \\
nlog_2n \nleq c.(n\sqrt{n}) \\
log_2n \nleq c.(\sqrt{n}) \\
```
```math
g \in O(f) \text{ as } \\
n\sqrt{n} \leq c.(n + nlog_2n) \\
```

## Exercise 2.2
What is more general?
a) An algorithm for directed or undirected networks?
b) A control algorithm for centralized or decentralized basic algorithms?

"More general" - Applicable to more cases.

a) An algorithm for undirected networks is more general because they allow bidirectional communication between all nodes of the network. Undirected networks themselves are a special case of directed networks with two directed pairs from/to each neighbour node in the network.

b) Control algorithms are used to execute a specific basic algorithm in a distributed system, a control plane. A control algorithm for decentralized basic algorithms will be more general. <WHY>

## Exercise 2.3
Give a transition system S and an assertion P such that P is a safety property but not an invariant of S.

Transition System *S*

- Set of configurations B
- Binary transition relations on set of configurations
- Set of initial configurations belonging to set of configurations

A distributed key-value store with two processes.
Global configuration  = local state of both processes.
Processes can execute internal, send and receive events.
A decentralized algorithm, both processes can be initiators.

Initial Configuration
```
I = {
    P1: {},
    P2: {}
} 
(part of set of configurations B)
```

Local State of Process
```
P = {
    <key>: <value>
}
```

Transition Relation
```
Internal Event: Add a key-value
Send event: Notify other process of new key-value
Receive event: Receive new key-value from other process
```

Reachable Configuration

- New keys-value pairs added to a process and synchronized between both processes.

Unreachable Configuration
  
- New key-value pairs added but not synchronized between both processes.

Assertion *P*

- A condition on the set of configurations
- It is a safety property if it is true in each reachable configuration.
- It is an invariant if it is true in all initial configurations and is preserved by all transitions.
- Each invariant is a safety property.
- Each safety property might or might not be an invariant.
- Safety properties only need to applicable for reachable configurations.
- Invariants need to be applicable for both reachable and non-reachable configurations.

Safety Property
```
P: Both processes will have the exact same key-value pairs.
```

This is not an invariant as it will fail in the unreachable configuration as described above.

## Exercise 2.4
Define the union of S1 = (B, ->1, I) and S1 = (B, ->2, I) as S = (B, ->1 U ->2, I)
(a) Prove that if P is an invariant of S1 and S2, then P is an invariant of S.
(b) Give an example where P is a safety property of S1 and S2 but not of S. 

**TODO**

## Exercises 2.5
Consider an execution abcd. Let a < c, b < d be the only causal relationships. Which executions are in the same computations as abcd?

```
a <- b
c <- d

Possible Executions

a    b    a    b    b 
b    a    b    a    d
c    c    d    d    a
d    d    c    c    a
```

## Exercise 2.6

Consider the following sequences of events at processes p0, p1, p2, p3.
```math
\begin{aligned}
p0: s1 \space s2 \space r5\\
p1: r2 \space s5\\
p2: r1 \space a \space s4 \space r3 \space r6\\
p3: s3 \space r4 \space b \space s6\\
\end{aligned}
```
Here si and ri are corresponding send and receive events for all i. a and b are internal events. Use Lamport's logical clock to assign clock values to these events. Do the same for the vector clock.

Lamport's Logical Clock

```math
\begin{aligned}
p0: 1 \space 2 \space 5\\
p1: 3 \space 4\\
p2: 2 \space 3 \space 4 \space 5 \space 8\\
p3: 1 \space 5 \space 6 \space 7\\
\end{aligned}
```

Vector Clock

```math
\begin{aligned}
p0: (1\space0\space0\space0) \space (2\space0\space0\space0) \space (3\space3\space0\space0) \\
p1: (2\space1\space0\space0) \space (2\space2\space0\space0)\\
p2: (2\space0\space1\space0) \space (2\space0\space2\space0) \space (2\space0\space3\space0) \space (2\space0\space4\space1) \space (2\space0\space5\space5)\\
p3: (0\space0\space0\space1) \space (2\space0\space4\space2) \space (2\space0\space4\space3) \space (2\space0\space4\space4)\\
\end{aligned}
```

## Exercise 2.7
Define the causal order for the transitions of a systme with synchronous communication. Adapt Lamport's logical clock for such systems, and give a distributed algorithm for computing the clock at run-time.

**TODO**

## Exercise 2.8
Give an example where LC(a) < LC(b), while a and b are concurrent events.

**TODO**

## Exercise 2.9
Give an algorithm to compute vector clock at run-time

**TODO**

## Exercise 2.10
Propose two adaptations of the MSI cache coherence protocol, in both cases by introducing an additional state for cache lines.

(a) Reduce bus traffic when a process reads a certain variable and then writes to it in its cache, while the corresponding cache line occurs only as invalid in other caches.

(b) Reduce the number of flushes to main memory in case of a continuous stream of reads and writes by different processes to a certain variable.

**TODO**

## Exercise 2.11
For each of the following approaches for handling a free lock to a waiting process, say whether it is starvation-free

(a) Randomly hand the lock to one of the waiting processes
(b) Processes that wait for the lock are placed in a FIFO queue. Hand the lock to the process at the head of thisi queue.
(c) Hand the lock to the waiting process with the Highest ID.

**TODO**
