---
id: dd15523a-91b7-4d50-8542-ce3ff9687107
---

# Can somebody explain this to me?: The computability of the laws of physics and hypercomputation — LessWrong
#Omnivore

[Read on Omnivore](https://omnivore.app/me/https-www-lesswrong-com-posts-rc-2-ymaj-8-sfa-g-4-crt-8-can-some-18985dac443)
[Read Original](https://www.lesswrong.com/posts/Rc2Ymaj8sfaG4Crt8/can-somebody-explain-this-to-me-the-computability-of-the)

["Hypercomputation"](http://en.wikipedia.org/wiki/Hypercomputation) is a term coined by two philosophers, Jack Copeland and Dianne Proudfoot, to refer to allegedly computational processes that do things Turing machines are in principle incapable of doing. I'm somewhat dubious of whether any of the proposals for "hypercomputation" are really accurately described as computation, but here, I'm more interested in another question: is there any chance it's possible to build a physical device that answers questions a Turing machine cannot answer?

I've read a number of Copeland and Proudfoot's articles promoting hypercomputation, and they claim this is an open question. I have, however, seen some indications that they're wrong about this, but my knowledge of physics and computability theory isn't enough to answer this question with confidence. 

Some of the ways to convince yourself that "hypercomputation" might be physically possible seem like obvious confusions, for example if you convince yourself that some physical quality is allowed to be any real number, and then notice that because some reals are non-computable, you say to yourself that if only we could measure such a non-computable quantity then we could answer questions no Turing machine could answer. Of course, the idea of doing such a measurement is physically implausible even if you could find a non-computable physical quantity in the first place. And that mistake can be sexed up in various ways, for example by talking about "analog computers" and assuming "analog" means it has components that can take any real-numbered value.

Points similar to the one I've just made exist in the literature on hypercomputation (see [here](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.10.4467&rep=rep1&type=pdf) and [here](http://www1.maths.leeds.ac.uk/~pmt6sbc/docs/davis.myth.pdf), for example). But the critiques of hypercomputation I've found tend to focus on specific proposals. It's less clear whether there are any good _general_ arguments in the literature that hypercomputation is physically impossible, because it would require infinite-precision measurements or something equally unlikely. It seems like it might be possible to make such an argument; I've read that the laws of physics are consiered to be computable, but I don't have a good enough understanding of what that means to tell if it entails that hypercomputation is physically impossible.

Can anyone help me out here?

## 23

There are spacetime models in general relativity (i.e. solutions to the [Einstein equations](http://en.wikipedia.org/wiki/Einstein%5Fequations)) that permit hypercomputation. In a [Malament-Hogarth](http://en.wikipedia.org/wiki/Malament%E2%80%93Hogarth%5Fspacetime) spacetime, there are wordlines such that an object traveling along the worldline will experience infinite time, but for an observer at some point p outside the wordline, the time it takes for the object to traverse the worldline is finite, and the wordline is entirely within p's causal past. So if you had a Turing machine traveling along this wordline, it could send a signal to p if and onliy if it halted, and the observer at p is guaranteed to receive the signal if the machine ever halts. No infinite-precision measurements are involved (unless perhaps you believe that a Turing machine operating reliably for an indefinite period of time is tantamount to an infinite-precision measurement).

Are these spacetimes physically possible? Well, like I said, they satisfy the basic laws of GR. However, they are not [globally hyperbolic](http://en.wikipedia.org/wiki/Globally%5Fhyperbolic), which means there is is no space-like surface (analogous to an "instant of time") such that providing all data on that surface fully determines the data over the rest of space-time uniquely. In other words, determinism of a particularly strong variety fails.

The strong version of the [cosmic censorship hypothesis](http://en.wikipedia.org/wiki/Cosmic%5Fcensorship) essentially states that a physically reasonable spacetime must be globally hyperbolic, so if you take it as a criterion of physical possibility, then Malament-Hogarth spacetimes are not physically possible. I guess this just brings up a certain amount of vagueness in the phrase "physically possible". It is usually taken to mean "possible according to the physical laws", but what exactly delimits what counts as a physical law? Suppose our universe is globally hyperbolic. Would it then be a law that space-time is globally hyperbolic? Anyway, if you have a more restrictive notion of physical law, such that only laws of temporal evolution count, then the laws of general relativity at least appear to permit hypercomputation.

At the end of your post you suggest that the computability of physical law might rule out hypercomputation. But the M-H spacetime argument does not require that the laws are uncomputable. There is a simple argument from the computability of the physical laws to the impossibility of hypercomputation _if you assume full determinism_, but that is an additional assumption. You can easily prove that hypercompuation is physically impossible if you make the following four assumptions (presented in reverse order of plausibility, according to my own metric): 

(1) The laws of physics are computable.

(2) The laws of physics are complete (i.e. there are no phenomena that are not covered by the laws).

(3) Spacetime must be globally hyperbolic (i.e. there must be a space-like surface of the kind described above).

(4) Finite-precision data over any space-like surface is sufficient for accurately determining the data everywhere on that surface's domain of dependence. 

> In a Malament-Hogarth spacetime, there are wordlines such that an object traveling along the worldline will experience infinite time, but for an observer at some point p outside the wordline, the time it takes for the object to traverse the worldline is finite, and the wordline is entirely within p's causal past.

Is it an actual spacetime, or just a class of every spacetime with this property? I'm having trouble locating a paper describing the metric that is not just the inside of the Kerr metric.

> Are these spacetimes physically possible? Well, like I said, they satisfy the basic laws of GR.

As a self-appointed resident GR expert, I would like to caution against this misapplication of GR. You cannot simply "place a Turing machine into a spacetime". The Turing machine is not a test particle. It has mass, it computes stuff and hence radiates heat, it increases the entropy of the universe. As a result, the spacetime with the Turing machine in it is different from the spacetime without. The change is tiny and can be neglected in many circumstances, but most emphatically not in this case.

The reason that placing a material object at non-zero temperature into a spacetime which maps an infinite affine-parameter geodesic into a finite one is that you get infinite amount of radiation and entropy in a finite time. As a result, your spacetime blows up into bits. This is a modification of Hawking's argument in favor of his famous Chronology Protection Conjecture (he used CTCs and virtual particles, not real objects).

This argument is quite general, but not often appreciated and not formalized, except in a few cases. It also applies to any attempts to use a CTC as an actual trajectory of a warm material object: you cannot hope to match up every microstate exactly after a complete loop simply by evolution. Hence the Novikov's disclaimer about his self-consistency principle: it's vacuous unless you presume "new physics" beyond GR.

> Is it an actual spacetime, or just a class of every spacetime with this property? I'm having trouble locating a paper describing the metric that is not just the inside of the Kerr metric.

It's the class of every spacetime with the property. Examples besides the Kerr spacetime are the universal covering of anti-de Sitter spacetime, the Reissner-Nodstrom spacetime, even a simple Minkowski spacetime rolled up along the temporal axis (or in fact any spacetime with CTCs).

> As a self-appointed resident GR expert, I would like to caution against this misapplication of GR. You cannot simply "place a Turing machine into a spacetime". The Turing machine is not a test particle. It has mass, it computes stuff and hence radiates heat, it increases the entropy of the universe. As a result, the spacetime with the Turing machine in it is different from the spacetime without. The change is tiny and can be neglected in many circumstances, but most emphatically not in this case.

Fair point. The spacetime structure will indeed indefinitely amplify even the tiniest bit of thermal radiation. And it is also true that Landauer's principle tells us that a computational process must radiate heat. 

But Landauer's principle is a consequence of the Second Law of Thermodynamics, and the Second Law is not, to the best of our knowledge, a fundamental law. It holds in our universe because of special boundary conditions, but it is entirely possible to construct universes with the same fundamental laws and different boundary conditions so that entropy stops increasing at some point in time and begins decreasing, or where entropy does not exhibit any significant monotonic tendency at all.

Does rigging boundary conditions in this manner take us outside the realm of physical possibility? Again, that depends on what the OP means by "physically possible". If all he means is "consistent with the fundamental laws of temporal evolution" then no, choosing special boundary conditions which negate the Second Law does not violate physical possibility. Of course, one would need very specifically (and implausibly) rigged boundary conditions in order to get a universe with a M-H setup that does not blow up, but astronomical unlikelihood is not the same as impossibility.

ETA: If you're interested, here's a [nice paper](http://faculty.washington.edu/manchak/manchak.supertasks.pdf) showing that a Malament-Hogarth spacetime can be constructed that satisfies various criteria of physical reasonableness (energy conditions, stable causality, etc.).

> It's the class of every spacetime with the property. Examples besides the Kerr spacetime are the universal covering of anti-de Sitter spacetime, the Reissner-Nodstrom spacetime, even a simple Minkowski spacetime rolled up along the temporal axis (or in fact any spacetime with CTCs).

Thanks for the examples, that's what I suspected, though I find the CTC examples dubious at best, as you appeal to a much stronger impossibility to justify a weaker one. I am not a stickler for global hyperbolicity, I can certainly imagine topological and/or geometric instantons "magically" appearing and disappearing. These don't cause infinite backreaction the way CTCs do.

> If you're interested, here's a nice paper showing that a Malament-Hogarth spacetime can be constructed that satisfies various criteria of physical reasonableness (energy conditions, stable causality, etc.).

It does indeed attempts to address most of the issues, but not the divergent emissions one, which seems mutually exclusive with non-divergent red shift. I am even fine with the "requires infinite energy" issue, since I can certainly imagine pumping energy through a whitehole from some other inaccessible spacetime (or some other instanton-like event).

> Does rigging boundary conditions in this manner take us outside the realm of physical possibility?

My interest is whether some hypercomputational construct can be embedded into our universe (which is roughly of the expanding FRW-dS type), not whether some other universe where entropy can decrease can perform these tricks. The reason, again, is that if you use much stronger assumptions to justify something weaker, the argument becomes much less interesting. In an extreme case "because DM decided so" would trivially support anything you want.

> But Landauer's principle is a consequence of the Second Law of Thermodynamics, and the Second Law is not, to the best of our knowledge, a fundamental law. It holds in our universe because of special boundary conditions, but it is entirely possible to construct universes with the same fundamental laws and different boundary conditions so that entropy stops increasing at some point in time and begins decreasing, or where entropy does not exhibit any significant monotonic tendency at all.

What about the Drescher/Barbour argument that the Second Law is an artifact of observers' ability to record time histories? That is, the only states that will contain "memories" (however implemented) of past states are the ones where entropy is higher than in the "remembering" state, because all processes of recording increase entropy.

So even in those thought experiments where you "reverse time" of the chaotic billiards-ball-world back to a low-entropy t = 0 _and keep going_ so that entropy increases in the negative time direction, the observers in that "negative time" state will still regard t = 0 to be in their past. Furthermore, any scenario you could set up where someone is only entangled with stuff that you deliberately decrease the entropy of (by increasing entropy outside the "bubble"), will result in that person thinking that the flow of time was the opposite of what you think.

I don't know how well this arguments meshes with the possibility of such GR solutions.

Truly infinite runtime has some problems, though they're different ones than infinite precision. What would you make your computer out of, and how would you ensure it didn't simply decay into a sphere of iron by quantum tunneling?

I'm not sure which of that vs voltage precision is more of a "mere engineering detail"; they both seem problematic at a level that, say, atom-perfect construction does not.

> So if you had a Turing machine traveling along this wordline, it could send a signal to p if and onliy if it halted, and the observer at p is guaranteed to receive the signal if the machine ever halts. No infinite-precision measurements are involved (unless perhaps you believe that a Turing machine operating reliably for an indefinite period of time is tantamount to an infinite-precision measurement).

Even if such spacetimes were possible, in order to exploit them for hypercomptation you would require a true Turing machine with infinite tape, infinite energy supply (unless it was perfectly reversible) and enough durability to run for a literally infinite amount of proper time without breaking. Such requirements seem inconsistent with the known laws of physics.

Why do you believe infinite memory is incompatible with the fundamental laws of physics? In any case, if it is, then Turing machines are physically impossible as well, the only physically possible computational systems are finite state automata, and there is no halting problem. You are right that in this case the infinite run-time provided by M-H spacetimes will not give any computational advantage, since every finite state machine either halts or loops anyway. But in discussions of computability theory I always assume that we are idealizing away memory constraints (unless explicitly stated otherwise).

As for the infinite energy requirement, there are three things to say. First, a Turing machine with infinite tape does not need to perform any irreversible computations (such as erasure). Second, even if it does perform computationally irreversible steps, this does not mean they are _thermodynamically_ irreversible unless the Second Law of Thermodynamics holds, and this is not a fundamental law of physics (see [this comment](https://www.lesswrong.com/r/discussion/lw/h9c/can%5Fsomebody%5Fexplain%5Fthis%5Fto%5Fme%5Fthe%5Fcomputability/8twb)). Third, even if infinite energy is required, I don't think the assumption of an infinite energy source is incompatible with any of the fundamental laws of physics.

The durability concern also seems to depend on thermodynamic considerations, although perhaps there is some genuine inconsistency with fundamental law here once quantum mechanics enters the picture.

Well, an infinite memory store or an infinite energy source would have infinite mass. So it would either take up the entire universe and have nowhere external to send its results to or, if it had finite size, it would be inside its own Schwarzchild radius, and there would be no way to send a signal out through its event horizon.

So yeah, I'd call infinite storage or power sources (as politely as possible) "unphysical".

And I don't see why you think the halting problem goes away just because you can't put infinite tape in your Turing machine, or because you use finite state automata instead. You still can't set an upper bound on the size of computation needed to determine whether any algorithm in general will terminate, and I kind of thought the point of the halting problem was that it doesn't only apply to actual Turing machines.

> So it would either take up the entire universe and have nowhere external to send its results to or, if it had finite size, it would be inside its own Schwarzchild radius, and there would be no way to send a signal out through its event horizon.

These are not the only options. Infinite sets have infinite proper subsets, so an object in a spatially infinite universe could have infinite size without taking up the entire universe. In a universe with an infinite amount of matter, a computational process could requisition an infinite proper subset of that matter as memory while still leaving plenty of matter to build other stuff. Or (if you don't take the cosmic censorship hypothesis as a constraint on physical possibility) you could have a naked singularity functioning as a white hole (the time reverse of a black hole, allowed by the time reversal invariant Einstein Field Equations) disgorging matter as needed for the computation.

That said, I am concerned about the fact that making the computational device too large would significantly modify the background metric, so (as shminux pointed out) one can't glibly consider a M-H spacetime, put a massive (perhaps infinitely large) Turing machine in it, and still assume that it is the same spacetime. It's not obvious to me that it would be impossible to have a device of this sort in an M-H spacetime, but neither is it obvious that it would be possible (and FWIW, I would bet against the possibility).

I think the right response is that infinite memory is always an idealization in discussions of computability. When we talk about the Church-Turing thesis as limning the notion of "computable", we are ignoring spatial constraints. Computability is a pure mathematical concept, not an engineering concept. When a theorist says that X is computable, she is not committing herself to the claim that the universe contains physical resources sufficient for the construction of a computer that implements X. Why should this usual standard become more rigid when we consider M-H spacetimes?

> And I don't see why you think the halting problem goes away just because you can't put infinite tape in your Turing machine, or because you use finite state automata instead. You still can't set an upper bound on the size of computation needed to determine whether any algorithm in general will terminate, and I kind of thought the point of the halting problem was that it doesn't only apply to actual Turing machines.

Every finite state machine will either halt or start repeating itself in finite time. This is guaranteed. To figure out whether a particular machine halts, simply wait until it either halts or enters a state it has entered before. One of these will happen within finite time, so you will always be able to determine within finite time whether or not the machine halts. It's true that if you want a single halting oracle that works for finite state machines of arbitrary size, it cannot itself be a finite state machine, it would have to be a Turing machine. Is this what you mean by the halting problem for FSAs? If so, then I agree, but that is a different sort of problem from the halting problem for Turing machines. My point was just that in the case of FSA's (unlike Turing machines) there's no computation that is ruled out _solely_ due to the lack of infinite runtime; allowing infinite runtime doesn't increase the power of FSAs.

> There are spacetime models in general relativity (i.e. solutions to the Einstein equations) that permit hypercomputation. In a Malament-Hogarth spacetime, there are wordlines such that an object traveling along the worldline will experience infinite time, but for an observer at some point p outside the wordline, the time it takes for the object to traverse the worldline is finite, and the wordline is entirely within p's causal past. So if you had a Turing machine traveling along this wordline, it could send a signal to p if and onliy if it halted, and the observer at p is guaranteed to receive the signal if the machine ever halts.

Don't you have the problem of the signal getting blue-shifted out of the range of your detector?

Not necessarily. For an example of an M-H setup without divergent blueshift see the paper I linked at the end of [this comment](https://www.lesswrong.com/r/discussion/lw/h9c/can%5Fsomebody%5Fexplain%5Fthis%5Fto%5Fme%5Fthe%5Fcomputability/8twb).

Infinite time is not enough to do hypercomputation. You also need infinite memory. If you only have n bits of memory, you only have 2^n possible states, so after time 2^n, your computation must terminate or have entered a loop, so more time is not useful.

Also, your and wikipedia's description is pretty vague. Deutsch proposed a more precise model of computation along a CTC. It assumes that you only have finitely many bits of memory (and thus are computable), but it avoids the problems that shminux mentions. John Watrous and Scott Aaronson [proved](http://www.scottaaronson.com/democritus/lec19.html) that in this model, you can take full advantage of the time and compute full PSPACE problems. While such problems are not supposed to be tractable in short time without a CTC, that's a far cry from halting. Also, reversible computing should make PSPACE problems practical in some sense.

I'm not sure I understand why determinism would be a necessary assumption in ruling out hypercomputation. As I understand it, Turing showed that probabilistic machines aren't any more powerful, computationally, than deterministic ones. But you word (4) to include finite precision data being determinitive. How far could that assumption be weakened? Could it, perhaps, be replaced by an assumption that you can't exploit infinite precision in building your device--maybe there's some chaotic behavior that stops you from predicting the behavior of a system from your data, but it's no more useful than true randomness for building any computing device?

I should clarify: Assumptions (1)-(4) in my comment were only supposed to be _sufficient_ conditions for the impossibility of hypercomputation, not necessary conditions. The basic idea is this. If hypercomputation were physically possible, there would be some universe governed by our laws that contains a hypercomputational process. If the laws are computable, deterministic and only require finite precision input data, we could simulate this universe accurately on a computer if we provided it with the initial state. This would allow us to simulate a hypercomputational process on a Turing machine, and that is impossible. Therefore hypercomputation is incompatible with those assumptions.

The assumptions of determinism and finite precision are crucial for _this_ argument because without them accurate simulation for an arbitrary length of time need not be possible. But there may be other arguments for the physical impossibility of hypercomputation that do not rely on these assumptions.

 I do think assumptions (1) and (2) by themselves are insufficient, and the Malament-Hogarth setup is supposed to be an existence proof of this insufficiency. The laws of GR are computable, yet they seem to allow hypercomputation (perhaps the M-H setup is incompatible with some _other_ fundamental law, as some of the posters are arguing, but that is irrelevant to this particular point).

ETA: It's also worth keeping in mind that non-deterministic, in this context, is not the same as probabilistic. If a spacetime is not globally hyperbolic, then field values on any spatial surface do not determine field values everywhere else. But this doesn't mean that the laws give you probabilities about what will happen outside the domain of dependence. The general relativistic laws are non-probabilistic.

> is there any chance it's possible to build a physical device that answers questions a Turing machine cannot answer?

I don't think computability is the right framework to think about this question. Mostly this is because, for somewhat silly reasons, there exists a Turing machine that answers any fixed finite sequence of questions. It's just the Turing machine which prints out the answers to those questions. "But which Turing machine is that?" Dunno, this is an existence proof. But the point is that you can't just say "you can't build a device that solves the halting problem" because, for any fixed finite set of Turing machines, you can trivially build such a device, you just can't recognize it once you've built it...

It follows that in the framework of computability, to distinguish a "real halting oracle" from a rock with stuff scribbled on it, you need to ask infinitely many questions. And that's pretty hard to do. 

So I think the correct framework for thinking about this problem is not computability theory but complexity theory. And here it genuinely is an open problem whether, for example, it's possible to build a physical computer capable of solving some problems efficiently that a classical computer can't (e.g. a quantum computer). Scott Aaronson has written about this subject; see, for example, [NP-complete problems and Physical Reality](http://arxiv.org/abs/quant-ph/0502072) as well as [Closed Timelike Curves Make Quantum and Classical Computing Equivalent](http://arxiv.org/abs/0808.2669). 

In the framework of complexity theory, one can now also ask the following question: if someone built a device and claimed that it could solve some problems more efficiently than our devices can, how do we efficiently verify that their answers are right? This question is addressed by, for example, the framework of [interactive proofs](http://en.wikipedia.org/wiki/Interactive%5Fproof%5Fsystem). As Scott Aaronson [says](http://www.scottaaronson.com/blog/?p=152), this allows us to make statements like the following:

> We now know that, if an alien with enormous computational powers came to Earth, it could prove to us whether White or Black has the winning strategy in chess. To be convinced of the proof, we would not have to trust the alien or its exotic technology, and we would not have to spend billions of years analyzing one move sequence after another. We’d simply have to engage in a short conversation with the alien about the sums of certain polynomials over finite fields.

**Edit:** I should clarify that when I said

> here it genuinely is an open problem whether, for example, it's possible to build a physical computer capable of solving some problems efficiently that a classical computer can't (e.g. a quantum computer).

there are actually two open problems here, one practical and one theoretical. The practical question is whether you can build quantum computers (and physics is relevant to this question). The theoretical question is whether a quantum computer, if you could build one, actually lets you solve more problems efficiently than you could with a classical computer; this is the question of whether [P = BQP](http://en.wikipedia.org/wiki/BQP). 

> I don't think computability is the right framework to think about this question. Mostly this is because, for somewhat silly reasons, there exists a Turing machine that answers any fixed finite sequence of questions. It's just the Turing machine which prints out the answers to those questions. "But which Turing machine is that?" Dunno, this is an existence proof. But the point is that you can't just say "you can't build a device that solves the halting problem" because, for any fixed finite set of Turing machines, you can trivially build such a device, you just can't recognize it once you've built it...
> 
> It follows that in the framework of computability, to distinguish a "real halting oracle" from a rock with stuff scribbled on it, you need to ask infinitely many questions. And that's pretty hard to do.

I think [Toby Ord](http://amirrorclear.net/academic/papers/many-forms.pdf) actually has a good response to this objection:

> It is worth responding, at this point, to a persistent argument that is made against the coherence of physical hypercomputation. It states that a machine must perform an infinite number of computations for it to count as hypercomputational. After all, for any function f on the integers, there is a Turing machine that computes f(n) for an arbitrarily large finite number of values of n. It is thus claimed either that we could not know that a prospective machine was a hypermachine after witnessing finitely many computations or that it simply would not be a hypermachine since its behaviour could be simulated by a Turing machine. Hypercomputation is thus claimed to be on shaky ground. However, it is easy to see that this argument cannot achieve what it hopes to since it does not just collapse hypercomputation to classical computation, but instead it collapses all computation on the integers down to that of finite state machines. This is because for any function f on the integers, there is also a finite state machine that computes f(n) on an arbitrarily large finite domain. Thus, as explained in Copeland \[10\], whatever force this argument is supposed to have with respect to hypercomputation, it must also have with respect to refuting the existence of classical (general recursive) computation. Since the latter is agreed to be on firm ground, it is difficult to see why this argument should count against the former.

Recall that a physical computer is technically a finite state machine (it doesn't have infinite memory). This is another reason I don't think Turing machines are a good formalism for talking about computation in the real world. 

> It is thus claimed either that we could not know that a prospective machine was a hypermachine after witnessing finitely many computations or that it simply would not be a hypermachine since its behaviour could be simulated by a Turing machine. Hypercomputation is thus claimed to be on shaky ground.

The former suggestion seems like the more important point here. While true that the hypercomputer's behavior can be simulated on a Turing machine, this is only true of the single answer given and received, not of the abstractly defined problem being solved. The hypercomputer still cannot be proven by a Turing machine to have knowledge of a fact that a Turing machine could not.

And so the words "shaky ground" are used loosely here. The argument doesn't refute the theoretic "existence" of recursive computation any more than it refutes the existence of theoretic hypercomputation. That finite state machines are the only realizable form of Turing machine is hardly a point in their generalized disfavor.

There's another issue also worth pointing out: The classical analog of BQP isn't P. The classical analog is [BPP](http://en.wikipedia.org/wiki/BPP%5F%28complexity/)). It is widely believed that P=BPP, but if P!= BPP then the relevant question in your context will be whether BPP=BQP.

> if you could build one, actually lets you solve more problems efficiently than you could with a classical computer; this is the question of whether P = BQP.

This isn't quite what this question asks. We know that some things are faster with a quantum computer than what can be one in the best case classical situation. [Grover's algorithm is one example](http://en.wikipedia.org/wiki/Grover%27s%5Falgorithm). The question of whether P=BQP is one formulation of that for yes and no questions. But even this isn't quite accurate. For example, it could be that quantum computers can do some extremely high degree polynomial speed-up even while P=BQP. But this is essentially a minor nitpick. 

> But the point is that you can't just say "you can't build a device that solves the halting problem" because, for any fixed finite set of Turing machines, you can trivially build such a device, you just can't recognize it once you've built it...

solving is not the same as providing the answer

Yes, but the distinction between the two isn't captured by computability theory (unless you are allowed to pose infinitely many problems). Also, if the universe is spatially infinite, it can solve the halting problem in a deeply silly way, namely there could be an infinite string of bits somewhere, each a fixed distance from the next, that just hardcodes the solution to the halting problem.

This is obviously unsatisfying, but part of the reason it's unsatisfying is that even if such an infinite string of bits existed (and even if we somehow verified that it was trustworthy), it would constitute a horribly inefficient algorithm for solving the halting problem: moving at constant speed, it would take time exponential in the length of the code for a Turing machine to go to the place in the universe where the bit determining whether that Turing machine halts is stored. But this is a complexity consideration, not a computability consideration. 

> unless you are allowed to pose infinitely many problems

Or one selected at random from an infinite class of problems.

> Also, if the universe is spatially infinite, it can solve the halting problem in a deeply silly way, namely there could be an infinite string of bits somewhere, each a fixed distance from the next, that just hardcodes the solution to the halting problem.

That's why both computability theory and complexity theory require algorithms to have finite sized sourcecode.

You've discovered for yourself that hypercomputation is a cottage industry of dubious and contrived articles that often seem to dress conceptual misunderstandings as computational models. Computability is not by itself a diseased discipline (to use a convenient phrase from the LW stock), but hypercomputation, I feel, is a diseased little subfield within it.

Your characterization of critiques of hypercomputation as too specific is, I think, a little unfair. Most (I hesitate to say all - haven't thought about this in many years) HC proposals I've seen fall into one of these two camps:

1. Miraculous access to infinite precision.
2. Miraculous access to infinite time.

Martin Davis's article, to which you link, seems to me to do a good job of doing away with all of the first category.

You ask if there's a general critique of hypercomputation that works against all proposals, along the lines, for example, of showing that it'd require infinite-precision measurements. I don't think that can work, because, after all, it's not inconceivable that the Church-Turing Thesis is false; I don't believe that there's agreement that it stands proved or even provable (some would disagree). Perhaps there's a plain-old-boring way to hypercompute without whimsical GR models or miraculous oracles, but just by doing something with normal and finite resources that the Turing machine model somehow overlooked; that would be hypercomputation, and I don't know how to rule that out.

Is there a general critique of most or all published "fancy" hypercomputation proposals, from both 1\. and 2\. above? I don't know of anything published (but again, it's been many years since I actively thought about and sought out this material). I have some thoughts that may persuade you partially, or maybe not. I'm sure they wouldn't persuade most HC enthusiasts. I wanted once to write them up for a short essay or article, but never did (at least so far). Here's a very short summary.

The idea is that we're seduced by HC ideas because we fail to define clearly three things:

* what is computation as a mathematical model
* what is computation as a physical process
* why do we trust the results of computation as a physical process

As a thought hypothesis, consider a Pentium CPU with a floating-point division bug (google for details if not familiar). The bug was discovered by a mathematician puzzled at weird-looking division results. Normally we trust without questioning that our computers perform division accurately. Most of us treat our computers or calculators as black boxes that somehow manage to compute the right results (almost nobody knows the actual division algorithm implemented inside the CPU). Yet for some reason, when the mathematician found a discrepancy between the CPU performing the division and, say, a verification by hand, and validated a discrepancy with a few repeats, they must have immediately understood that the CPU is at fault, rather than the familiar long division algorithm is at fault. The CPU normally divides much faster and much more accurately then we can by hand; why didn't it even occur to the mathematician that maybe it's a bug in the long division algorithm rather than the one in the CPU? The reason is that the mathematician doesn't actually trust the CPU; they trust the algorithm of dividing two numbers, and they trust, to a lesser degree, that the CPU accurately implements the algorithm, and they trust, to a lesser degree, that there are no physical faults, cosmic rays, etc. etc. screwing up the implementation.

This and similar thought experiments may convince you that when we have a physical device doing something, and then we interpret its results (e.g. photons coming from monitor surface to your eyes) in a particular way as a result of a computation, there're two different kinds of trust that we invest the process with: say, mathematical trust and physical trust. For mathematical trust to exist, there must be a mathematical model, an algorithm, which we may comprehend and make sense of completely mentally, and then physical trust is the degree to which we believe the physical device accurately implements that mathematical model. I propose that without the existence of this wholly mental mathematical model (often implicit existence that we take on faith) we're not actually justified in calling the whole thing "computation", and the bulk of the trust that we put in its results evaporates.

There seem to be some limitations on how this mental mathematical model might work; for example, some notions of discreteness and finite computational time seem required for us to comprehend the model. These may be limitations of our mind; but our notion of computation, I claim, is intrinsically linked with what our minds are capable of. If we can make explicit these bounds on how our mental mathematical models may look like, that, to me, seems our best hope of "proving" the Church-Turing Thesis.

All the hypercomputation proposals, both from category 1\. and 2\. above, break this correspondence between a comprehendable (in principle) mental mathematical model and a physical realization, and instead depend in one crucial way or another on some physical thing as a non-abstractable step in the process. Just as with infinite precision proposals you wouldn't actually know where to get those arbitrary-precision decimals of a noncomputable real number in your mind, with the infinite time proposals you wouldn't know how to perform an infinite Turing machine run in your mind. Therefore, I claim, though on the surface these hypothetical devices look just like CPUs and calculators, albeit very exotic ones, in reality they are very different, and should not be called computational devices, do not deserve the trust we put in computational devices. This lack of trust can also be demonstrated, usually, by thought experiments that involve verification or validation. E.g. say you have an exotic GR model that lets you do an infinite TM run in some place and send a signal back to you during the run if the machine stopped, etc. Say you didn't get a signal. _How do you know_ that the machine never stopped, as opposed to something going physically wrong with the machine, the signal getting lost on the way etc.? You may retort, but how do you know that there wasn't a cosmic ray in the CPU when it divided etc., but there's a difference. With the CPU there's a mental model which gets the bulk of your trust, and you only trust the atoms of matter insofar as they correspond to it. If the atoms should fail you, nevermind, you'll find other atoms that work better, the model is intact. With the GR hypercomputation, you have to trust _the signal ray itself_, trust the atoms rather than the bits in your mind. I don't think we'd be justified in doing that.

(Quantum computation is wholly exempt from this reasoning; from computability's point of view, it's just a nifty implementation trick to construct a physical device that executes some particular very well-defined mental algorithms in a massively parallel way, achieving a vast speedup).

> is there any chance it's possible to build a physical device that answers questions a Turing machine cannot answer?

Since any finite set is trivially computable, it only makes sense to talk about hypercomputation for infinite sets/functions. For example, a certain kind of infinite time Turing machine can solve the halting problem of every other finite time Turing machine.  
This would mean that to physically realize a hypercomputer the universe has to allow finite access to infinite quantity (e. g. an infinite precision measurable real value, an infinite time pocket universe, etc). There are highly idealized model that does such things in both newtonian mechanics and general relativity, but they are not applicable to our universe.  
Hypercomputation is a (set of) well defined mathematical model(s), so the question of its realizability is ultimately a physical one: at the present time knowledge we have about our universe rules out such models, but of course we cannot show that this continues to be valid in possible extensions.

When building the physical device, is the Turing Machine it is required to beat also required to have a potential physical instance in the observable universe?

What I mean is, if there are (A) atoms in the observable universe, and I think of a type of question that would provably take a Turing Machine at least (10A) atoms to answer, and then build a Non-Turing Machine that answers those questions in only 1 million atoms, then a Hypothetical Turing Machine could answer the question, but no Physical Turing Machine made of (10A) atoms could be found in the observable Universe.

However, I'm not sure if this falls into the bounds of the sexed up mistakes you are referring to above, or if it doesn't.

> Some of the ways to convince yourself that "hypercomputation" might be physically possible seem like obvious confusions, for example if you convince yourself that some physical quality is allowed to be any real number, and then notice that because some reals are non-computable, you say to yourself that if only we could measure such a non-computable quantity then we could answer questions no Turing machine could answer. Of course, the idea of doing such a measurement is physically implausible even if you could find a non-computable physical quantity in the first place.

So what you're claiming is that there is an absolute limit to the precision with which any physical constant can be measured.

> It seems like it might be possible to make such an argument; I've read that the laws of physics are consiered to be computable, but I don't have a good enough understanding of what that means to tell if it entails that hypercomputation is physically impossible.

The laws of physics **as we understand them** appear to be computable (baring issues with knowing constants to infinite precision), but our understanding of the laws is incomplete. Firstly no one has been able to reconcile GR and QM. Furthermore, how do we know our understanding of the laws of physics isn't merely an approximation to the true laws, like Newtonian mechanics is an approximation to relativity?

> The laws of physics as we understand them appear to be computable

Well, this is a pretty weak statement. If someone wrote down a version of the laws of physics that wasn't computable, you wouldn't be able to use it to compute any predictions, so no one would use such laws. 

> If someone wrote down a version of the laws of physics that wasn't computable, you wouldn't be able to use it to compute any predictions, so no one would use such laws.

I don't think that's entirely true. Consider a well-defined real number which is uncomputable yet approximations of it can be computed, such as Chaitin's omega; now imagine a laws of physics which uses omega somewhere in it (perhaps as a physical constant). The full laws are uncomputable due to the inclusion of omega, yet you could compute a finite prefix of omega and make your predictions with that. You could even show that the laws are not just that finite prefix by computing further digits into omega and demonstrating that additional digits yields additional predictive accuracy.

> The full laws are uncomputable due to the inclusion of omega, yet you could compute a finite prefix of omega

You can't compute a prefix of Chaitin's omega of any arbitrary length. You can compute prefixes only up to some finite length, and this length is itself uncomputable.

> this length is itself uncomputable.

From our perspective, the length which it is computable is going to be arbitrary, and until we hit it, at each digit we will confront the same epistemic problem: "is the prefix of omega that seems to be embedded in our particular physics a finite computable prefix of omega and so perfectly computable and so our physics is perfectly computable, or is this a genuine uncomputable constant buried in our physics?"

This has been discussed in the past as the 'oracle hypercomputation' problem: suppose you found a device which claimed to be an oracle for Turing machines halting, and you test it out and it seems to be accurate on the _n_ Turing machines you are able to run to the point where they either halt or loop their state. How much, if at all, do you credit its claim to be an oracle doing hypercomputation? Since, after all, it could just be a random number generator, and in 1 out of the 2^n possible outputs its predictions will be completely correct 'by chance', or it could be using heuristics or something. What is one's prior for hypercomputation/oracles being possible and how much does one update?

This was discussed on the advanced decision theory ML a while back, IIRC, and I don't think they came to any solid conclusion either way.

I see a problem with this: There doesn't seem to be a way to tell if omega itself is in the laws of physics or some finite precision approximation to omega. Given any set of finite observable phenomena and any finite amount of time there will be some finite precision approximation to any real number which is sufficient in the equations to explain all observations, assuming the models used are otherwise correct and otherwise computable. How would one tell if the universe uses the real value Pi or a finite precision version of Pi whose finiteness is epsilon greater then what is needed to calculate any observable value? 

> How would one tell if the universe uses the real value Pi or a finite precision version of Pi whose finiteness is epsilon greater then what is needed to calculate any observable value?

How does one know the laws of physics won't suddenly change tomorrow, i.e., how does one distinguish a universe governed by a certain set of laws with one governed by an approximation of the same laws that stops working on a certain day?

> How would one tell if the universe uses the real value Pi or a finite precision version of Pi whose finiteness is epsilon greater then what is needed to calculate any observable value?

You can't. However, if you somehow found an encoding of a physical constant that was highly compressible, such as 1.379\[50 digits\]0000000000000000, or some other sort of highly regular series, it would be strong evidence towards our universe being both computable and, indeed, _computed_. (No such constant has yet been found, but we haven't looked very hard yet)

Depending on what you mean by "constant"... The exponent in Coulomb's law is 2\. To about 13 decimal places. I would expect some of the similar constants in other formulas to be comparably compressible.

It's not hard to wright down hypothetical non-computable that can nonetheless be tested. Note in particular that while both QM and GR are both theoretically computable, actually computing anything beyond the absolute very simplest examples with either of them is beyond our ability.

It seems like you can go beyond Turing machines long as you're willing to take the output in the form of something a Turing machine cannot output. But "let's measure this physical system and then write down some finite-length numbers" is still numbers, something a Turing machine can do. Instead, a physical hypercomputer can have super-Turing precision at stuff like "take these input voltages and give me an output voltage."

What is special about voltage? 

It's one of those hypothesized-continuous quantities (it's one of those because position is quite possibly continuous, and voltage is a hypothesized-continuous function of position). This means that you can have _any_ voltage between 0 and 1\. If you want to input numbers into a Turing machine, though, they have to have finite Kolmogorov complexity. So there are voltages you can have that can't be described in finite time.

This is what I mean by "take an output in some form" - if you take an output in the form of a voltage, you can have more voltages than you have finite-length descriptions of voltages. Which means that the voltage itself has to be the output - not a description of the voltage, which would obviously be describable, and thus (barring some goedelian hijinks, perhaps) replicable by a turing machine.

In classical electro, voltage is a continuous function of position; agreed. It is not, however, clear to me that this is true in a QM formulation. If you consider the case of a hydrogen atom, for example, the possible energies of its electron are quantised; since those energies are binding energies due to the voltage of the proton, it is not clear to me that a voltage between two allowed energy states meaningfully exists. At any rate it seems that no physical machine could output such a voltage; what would this mean? And since a physical machine ultimately consists of atoms, and sums over quantised states are themselves quantised, well then. 

Let "voltage" be < k\*e^2/r^2 >, summed over pairs of different particles.

Your integral treats distance as unquantised; it is not clear that the true QM theory does this - Planck distance. Moreover, implemented as a physical machine, your atoms are going to be bound together somehow, those bonds will be quantised, and then the average distance is itself quantised because you are dealing with sums over states with a definite average interatomic distance - you can move the whole machine, but you can't move just a part of the machine with arbitrary precision, you have to go between specific combinations of quantised interatomic binding states. Finally, just because a theory can express some quantity mathematically doesn't mean that the quantity meaningfully exists in the modelled system; what are the physical consequences of having voltage be X rather than X+epsilon? If you (or any physical system you care to name) can't measure the difference then it's not clear to me in what sense your machine is "outputting" the voltage. 

So basically, what you're asking for is a finite-length procedure that will tell an irrational-number output from a finite-description-length output? The trouble is, there's no such procedure, as long as you can have a turing machine big enough to fool the finite-length procedure.

If you knew the size of the machine, though, you might be able to establish efficiency constraints and do a test, though.

As for the physics, I agree, fundamental quantization is possible, if untested. Hence why I said things like "hypothesized-continuous." Though once we start taking averages (the < > brackets), you can still have a superposition with any average - to get around that you'd need quantum amplitude to be quantized (possible).

> you can still have a superposition with any average

Ok, now the hypothesized-continuous quantity isn't so much voltage as quantum amplitude. Which actually is a rather better argument in the first place, so let's run with that! 

I would then ask, is there really a meaningful physical difference between the state A|1> + B|2>, and the state (A+epsilon)|1> + (B-epsilon)|2>? (Let's hope the ket notation makes it through the Markdown. Anyway.) Observe that the rest of the universe actually interacts with the underlying pure states |1> and |2>; the amplitudes only change the probabilities of outcomes (in Copenhagen) or the measure of worlds (in MW). For sufficiently small epsilon it does not seem to me that either of these changes is actually observable by any entity, conscious or otherwise. In that case, as I say, I do not quite understand what it means to say that a physical process has "computed" epsilon. Perhaps a round of Taboo is in order? 

So, what I think is that for some continuous output and any epsilon you care to name, one can construct a totally normal computer with resources 1/delta that can approximate the continuous output to within epsilon.

Proceeding from there, the more interesting question (and the most _observable_ question) is more like the computational complexity question - does delta shrink faster or slower than epsilon? If it shrinks sufficiently faster for some class of continuous outputs, this means we can build a real-number based computer that goes faster than a classical computer with the same resources.

In this sense, quantum computers are already hypercomputers for being able to factor numbers efficiently, but they're not quite what I mean. So let me amend that to a slightly stronger sense where the machine actually _can_ output something that would take infinite time to compute classically, we just only _care_ to within precision epsilon :P

Given the presence of various forms of noise, I'm not sure what it would mean to measure a voltage to kilobits worth of precision. At some point I start asking how you ensure that the noise from electrons tunneling into and out of your experimental apparatus is handled. I'm also not sure that there's even a theoretical sense in which you can make your machine cold enough to reduce the noise enough to get that sort of precision.

I understand what a nine-digit voltmeter looks like. And I can extrapolate based on that, assume some things about improved materials, temperature controls, reduced temperature, extended measurement times, and so on, and would be willing to believe that the next nine digits are "mere engineering". Maybe even the nine digits after that, and the next nine. But taking that to mean you can extend it out to infinity -- literally! -- seems like a logical and physical fallacy.

Fair enough. In the low-noise limit, a continuous computer actually has to become a type of quantum computer, where the output is just some continuously-valued quantum state.

But that's a doable thing, that we can actually do. Hm. Sort of.

This is a confusion about what a Turing machine represents. The method of output data isn't relevant here. The voltage is simply one way of representing numbers. 


