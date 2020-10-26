# Chapter 2 - Preliminaries - Exercises

## Exercise 2.1
```math
\text{ For each of the following functions} f \text{and} g, \text{say whether } f \in O(g) \text{ and/or } g \in O(f).\\  
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

a) An algorithm for undirected networks is more general because they allow bidirectional communication between all nodes of the network. An algorithm for directed networks can be implemented as a special case in an undirected network..

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

```math
S1 = (B, \rightarrow_1, I)\\
S2 = (B, \rightarrow_2, I)\\
```

The two transitions systems have the same set of configurations and initial configurations.
Only the binary relations differ between the two transition systems.
i.e. the two systems will start with the same configuration but reach different configurations at the end of execution.

Thus, the union of the two binary relations should represent the union of the two transition systems encompassing reachable configurations of both S1 and S2.
```math
S = (B, \rightarrow_1 \cup \rightarrow_2, I)
```

**(a)** P is an invariant of S1 and S2.
Thus, P is valid for all initial configurations.
```math
P \in I
```
S has the same initial configurations as S1 and S2 thus P is valid for all initial configurations.

P is preserved by all transitions in the binary relations ->1 and ->2 in S1 and S2 according to the definition of invariants.

The union of S1 and S2 is the union of the binary relations encompassing all possible transitions defined in ->1 and ->2.
Thus, the invariant P will also be valid for all transitions of S.

**(b)** A safety property should be true in each reachable configuration.
If a safety property P is true in S1 and S2 implies P is true in all reachable configurations of S1 and S2.
The reachable configurations of S1 and S2 are defined by ->1 and ->2 and the safety property P depends on reachable configurations of either S1 and S2.
If the ->1 and ->2 are disjointed sets, the reachable configurations will end up in the reachable configurations defined by either ->1 or ->2 and the safety property P applicable for S1 or S2 will not hold for the union of ->1 and ->2.

## Exercises 2.5
Consider an execution abcd. Let a < c, b < d be the only causal relationships. Which executions are in the same computations as abcd?

```math
a \prec b\\
c \prec  d\\

\text{Possible Executions}\\

a \space   b \space    a \space    b \space    b\\
b \space    a \space    b \space    a \space    d\\
c \space    c \space    d \space    d \space    a\\
d \space    d \space    c \space     c \space    a\\
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
p0:&\space 1 \space 2 \space 5\\
p1:&\space 3 \space 4\\
p2:&\space 2 \space 3 \space 4 \space 5 \space 8\\
p3:&\space 1 \space 5 \space 6 \space 7\\
\end{aligned}
```

Vector Clock

```math
\begin{aligned}
p0:&\space (1\space0\space0\space0) \space (2\space0\space0\space0) \space (3\space3\space0\space0) \\
p1:&\space (2\space1\space0\space0) \space (2\space2\space0\space0)\\
p2:&\space (2\space0\space1\space0) \space (2\space0\space2\space0) \space (2\space0\space3\space0) \space (2\space0\space4\space1) \space (2\space0\space5\space5)\\
p3:&\space (0\space0\space0\space1) \space (2\space0\space4\space2) \space (2\space0\space4\space3) \space (2\space0\space4\space4)\\
\end{aligned}
```

## Exercise 2.7
Define the causal order for the transitions of a system with synchronous communication. Adapt Lamport's logical clock for such systems, and give a distributed algorithm for computing the clock at run-time.

**TODO**

## Exercise 2.8
Give an example where LC(a) < LC(b), while a and b are concurrent events.

In exercise 2.6, events r1 and r2 are concurrent.
However, the lamport clock values fulfils the condition.
```math
LC(r1) < LC(r2)
```

This irregularity is fixed in the vector clock where 
```math
\begin{aligned}
r1 &= (2\space0\space1\space0)\\
r2 &= (2\space1\space0\space0)
\end{aligned}
```
there is no causal order between the events, thus the events are concurrent.

## Exercise 2.9
Give an algorithm to compute vector clock at run-time
Consider an event a at process i,
let VC = (k0, ..., ki) be the clock value of the previous event v at the same process.
If a is an internal event, then 
```math
VC(a) = (k0,..., ki + 1)
```
If a is a receive event from process f and b the send event corresponding to a, then 
```math
VC(a) = max\{VC(v), (k0, .., kf+1, .., ki+1)\}
```
## Exercise 2.10
Propose two adaptations of the MSI cache coherence protocol, in both cases by introducing an additional state for cache lines.

(a) Reduce bus traffic when a process reads a certain variable and then writes to it in its cache, while the corresponding cache line occurs only as invalid in other caches.

(b) Reduce the number of flushes to main memory in case of a continuous stream of reads and writes by different processes to a certain variable.

MSI Cache Coherence Protocol: Maintain cache consistency across caches.

Modified - cache line has been writen in the cache, and must be eventually stored in the main memory.
Shared - line has not been written to in any cache and can be read.
Invalid - line must be refreshed before it can be read

A cache line in a single cache starts
- nonmodified, 
- process write data, cache line becomes modified in that cache and invalidated in all other caches
- modified cache line read by a process in some other cache, then in both caches this line becomes shared.
- until a cache line is written to byte another process it isnt invalidated.

**TODO**

## Exercise 2.11
For each of the following approaches for handling a free lock to a waiting process, say whether it is starvation-free

(a) Randomly hand the lock to one of the waiting processes
(b) Processes that wait for the lock are placed in a FIFO queue. Hand the lock to the process at the head of thisi queue.
(c) Hand the lock to the waiting process with the Highest ID.

(a) No, it will not be starvation free.
If the waiting process is randomy selected, then the probability that each waiting process will eventually get a lock is not deterministic.

(b) Yes, it will be starvation free.
Assuming each process holding the lock will eventually free it, . 

(c) No it will not be starvation free.
Processes with higher process IDs could keep trying to get hold of the lock, a process if able to impersonate IDs could hold the lock forever.
