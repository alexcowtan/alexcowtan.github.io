---
title:  "A short derivation of the ancilla-aided, measurement/feedforward-based fault-tolerant controlled-Z^a gate using the ZH-calculus"
date:   2019-10-15
---

# A short derivation of the ancilla-aided, measurement/feedforward-based fault-tolerant controlled-Z^a gate using the ZH-calculus

Yo.


Earlier this year, Yunseong Nam, Yuan Su and Dmitri Maslov put a paper up on arXiv about how to perform the Approximate Quantum Fourier Transform using $$\mathcal{O}(nlog(n))$$ $$T$$-gates[^1]. In this paper they described their own construction of a controlled-$$Z^a$$ gate using an ancilla, a measurement and 4 $$T$$-gates (not including the $$T$$-gates for the single-qubit rotation, which they show can be placed in a separate layer for the algorithm they are describing and implemented using a different clever trick).

![controlled-Z^a gate construction](/assets/cza_construction.png)

This construction was considered valuable enough that it formed a significant component of a patent that Nam et al. filed as part of IonQ [^2].

To derive this construction, one must first use the Toffoli-measurement construction of Cody Jones [^3] to shift the $$Z^a$$ phase from the target of a controlled gate to a single qubit gate, and then optimise by using the "relative Toffoli", or Toffoli*, from the same paper. When written in circuit notation, this construction is not obvious -- at least not to me.

The ZX-calculus is a language for concisely reasoning about quantum circuits, along with many other uses [^4]. However, in its "standard" form, with a near-optimally small set of generators and axioms [^5], it is notably poor for describing quantum addition (i.e. multi-qubit quantum controlled gates). An encoding of the classical AND gate requires 25 basic generators and non-Clifford phases [^6].

To describe this class of operations more concisely, one can add extra generators to augment the minimal set -- for example, the triangle was initially added as syntactic sugar for ZX-calculus Clifford+T completeness proofs [^7], but it can also be used for describing quantum addition. Here, I am instead going to use the ZH-calculus, another complete calculus for quantum computation [^8], which instead of the triangle adds a generator called the n-arity Hadamard. Only two of these generators are required to encode the AND gate, and it can be defined using triangles [^9]. I won't go into triangles properly here (sorry Harny).

![zh_rules](/assets/zh_rules.png)

As you will see in this short derivation using the ZH-calculus, the fault-tolerant construction of the controlled-$$Z^a$$ gate doesn't just look easier to get to than in the circuit notation, it practically falls out of the diagram as the only logical conclusion once you accept the goal of moving the phase $$Z^a$$ from a controlled gate to a single-qubit gate.

First, we have replaced the initial controlled-$$Z^a$$ gate circuit with an equivalent ZH-diagram. I am following the convention, and will use some of the derived rules, of a paper I recommend reading which derives lots of similarly useful equivalent circuits for quantum addition [^10].

![line_1](/assets/line1.png)

We have pulled the angle from the H-box into an X-spider, using rules HS1, ZS2 and the generator definitions in equation 3 of [^10]. We now need to extend the X-spider into an ancilla qubit.

![line_2](/assets/line2.png)

This can all be performed using the ZS1 rule and the definition of the 2-arity Hadamard in traditional ZX-calculus. This diagram is equivalent to a Toffoli gate acting on an ancilla prepared in the $$\mid 0\rangle$$ state. However, there are two problems. Firstly, we have postselected the ancilla measurement to be in the $$\langle 0 \mid$$ state. Secondly, the Toffoli gate will require 7 $$T$$-gates to perform [^11]. Let's fix the postselection problem first.

If we measure a $$\langle 1 \mid$$ state on the ancilla qubit, we instead have a $$\pi$$ rotation on the last X-spider and we must apply a correction. Following the same rules as in equation 9 of [^10], we get a classically controlled $$CZ$$-gate, dependent on the measurement outcome of our ancilla. This must be applied here, rather than having, for example, an $$X$$ gate on the ancilla, so that the correction gate can be in the causal future of our measurement.

![line_3](/assets/line3.png)

Lastly, we would like to reduce the computation cost by trimming down the $$T$$-count. To do this, note that at the very start of our derivation we could have pulled out a controlled-$$S^{\dagger}$$ gate from the controlled-$$Z^a$$, changing the coefficient of our H-box accordingly. When we perform the rest of the derivation, we get an additional $$S$$-gate on the ancilla. This gives the Toffoli* gate, as demonstrated in equation 6 of [^10], and therefore we have completed the derivation.

We have proved this nice result and reduced the required $$T$$-count significantly relative to the controlled-$$Z^a$$ gate's naive decomposition, and we have done so with relative ease and only using a fraction of the available axioms. Why is this interesting? Well, the ZH-calculus hasn't been used yet to prove any new results for quantum controlled gates, but the ease with which you can derive the current state-of-the-art results gives me hope that there is relatively low-hanging fruit out there.

Contributors to PyZX [^12] are also working on automating use of the ZH-calculus, in much the same way as they have automated rewrite rules on the ZX-calculus, in order to reduce circuits relying on quantum-addition to some kind of normal form and potentially reduce the resources required. It seems to still be in early stages, but there is a branch on their repo [^13].

In much the same way as we have incorporated techniques derived using ZX-calculus into our compiler [^14], this might too be an interesting avenue to explore, for classes of circuits the ZX-calculus struggles with.

[^1]: [Approximate Quantum Fourier Transform using O(nlog(n)) $$T$$-gates](https://arxiv.org/pdf/1803.04933.pdf)
[^2]: [Optimal Fault-Tolerant Implementations of Heisenberg Interactions and Controlled-Za Gates](https://patentimages.storage.googleapis.com/02/c6/2f/1ae76f4e15261b/US20190258757A1.pdf)
[^3]: [Novel constructions for the fault-tolerant Toffoli gate](https://arxiv.org/pdf/1212.5069.pdf)
[^4]: [ZX-calculus](http://zxcalculus.com/publications.html)
[^5]: [A Near-Optimal Axiomatisation of ZX-Calculus for Pure Qubit Quantum Mechanics](https://arxiv.org/pdf/1812.09114.pdf)
[^6]: [Picturing Quantum Processes: A First Course in Quantum Theory and Diagrammatic Reasoning](https://dx.doi.org/10.1017/9781316219317), 12.1.3.1
[^7]: [Completeness of the ZX-calculus](https://arxiv.org/pdf/1903.06035.pdf), p3
[^8]: [ZH: A Complete Graphical Calculus for Quantum Computations Involving Classical Non-linearity](https://arxiv.org/pdf/1805.02175.pdf)
[^9]: [Completeness of the Phase-free ZH-calculus](https://arxiv.org/pdf/1904.07545.pdf)
[^10]: [Graphical Fourier Theory and the Cost of Quantum Addition](https://arxiv.org/abs/1904.07551)
[^11]: [Toffoli Gate Wiki](https://en.wikipedia.org/wiki/Toffoli_gate#Relation_to_quantum_computing)
[^12]: [PyZX: Large Scale Automated Diagrammatic Reasoning](https://arxiv.org/abs/1904.04735)
[^13]: [PyZX branch "zh"](https://github.com/Quantomatic/pyzx/tree/zh)
[^14]: [Phase Gadget Synthesis for Shallow Circuits](https://arxiv.org/abs/1906.01734)