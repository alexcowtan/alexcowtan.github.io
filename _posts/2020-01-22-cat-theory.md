---
title:  "On the successes of Applied Category Theory, and in particular graphical calculi, in quantum computing"
date:   2020-01-22
---

# On the successes of Applied Category Theory, and in particular graphical calculi, in quantum computing

There have recently been discussions on Twitter about whether Applied Category Theory (ACT) has actually had much success in the "Real World". There have been conversations about its application to logic, type theory, geometry and some extremely theoretical physics, but these are already well-known, and depending on your definition of "Applied" the results of these may not be "Real World" enough. There are also people working on compositional neural networks [^5], databases [^6], lenses for game theory [^1], pregroups for linguistics [^2], PROPs for signal flow graphs [^3] and lots of other stuff [^4].

I will now give a list of examples where category theory has been used in the process of deriving or computing practically applicable results in quantum information. All of these come from the body of work related to the ZX-calculus [^7].

1. Deriving and verifying error correction codes [^8].
2. Reducing Clifford circuits to have the smallest known number of layers of two-qubit gates [^9].
3. T-count optimisation [^10] [^11].
4. Deriving techniques for optimising NISQ chemistry circuits [^12].
5. Deriving low space-time volume surface code defect braiding results for magic state distillation (and other benchmarks) [^13].
6. Reasoning about the logical operations of lattice surgery [^14] [^15].

There are other, more questionable examples: in our compiler, we use structured cospans [^16] to stitch together disparate data structures. However, I don't think it is necessary to have a categorical framework to reason about stitching in this context. Another example is the use of diagrammatic frameworks for linguistics to design circuits for quantum natural language processing -- I don't know how far along this project is, and whether anything will come out of it.

[^1]: [Coherence for lenses and open games](https://arxiv.org/abs/1704.02230)
[^2]: [Linguistics using Category Theory](https://golem.ph.utexas.edu/category/2018/02/linguistics_using_category_the.html)
[^3]: [Seven Sketches in Compositionality: An Invitation to Applied Category Theory](https://arxiv.org/abs/1803.05316)
[^4]: [Applied Category Theory Resources](https://www.appliedcategorytheory.org/resources/)
[^5]: [Compositional Deep Learning](https://arxiv.org/abs/1907.08292)
[^6]: [Databases are Categories](http://math.mit.edu/~dspivak/informatics/talks/galois.pdf)
[^7]: [ZX-calculus](http://zxcalculus.com)
[^8]: [Graphical Structures for Design and Verification of Quantum Error Correction](https://arxiv.org/abs/1611.08012)
[^9]: [Graph-theoretic Simplification of Quantum Circuits with the ZX-calculus](https://arxiv.org/abs/1902.03178)
[^10]: [Reducing T-count with the ZX-calculus](https://arxiv.org/abs/1903.10477)
[^11]: [Techniques to reduce π/4-parity phase circuits, motivated by the ZX calculus](https://arxiv.org/abs/1911.09039)
[^12]: [Phase Gadget Synthesis for Shallow Circuits](https://arxiv.org/abs/1906.01734)
[^13]: [Efficient compression of quantum braided circuits](https://arxiv.org/abs/1912.11503)
[^14]: [Pauli Fusion: a computational model to realise quantum transformations from ZX terms](https://arxiv.org/abs/1904.12817)
[^15]: [The ZX calculus is a language for surface code lattice surgery](https://arxiv.org/abs/1704.08670)
[^16]: [Structured Cospans](https://arxiv.org/abs/1911.04630)