---
id: ceccd519-3cfc-431c-bbdf-92a46cfc9916
---

# Interpretability — LessWrong
#Omnivore

[Read on Omnivore](https://omnivore.app/me/https-www-lesswrong-com-posts-cz-z-6-fch-4-j-spw-cpu-6-c-interpr-18985d9c248)
[Read Original](https://www.lesswrong.com/posts/CzZ6Fch4JSpwCpu6C/interpretability)

Crossposted from the [AI Alignment Forum](https://alignmentforum.org/posts/CzZ6Fch4JSpwCpu6C/interpretability). May contain more technical jargon than usual.

_Chris Olah wrote the following topic prompt for the Open Phil 2021 request for proposals on the alignment of AI systems. We (Asya Bergal and Nick Beckstead) are running the Open Phil RFP and are posting each section as a sequence on the Alignment Forum. Although Chris wrote this document, we didn’t want to commit him to being responsible for responding to comments on it by posting it._

_Summary: We would like to see research building towards the ability to "reverse engineer" trained neural networks into human-understandable algorithms, enabling auditors to catch unanticipated safety problems in these models._

\--

Potential safety failures of neural networks might be thought of as falling into two broad categories: known safety problems and unknown safety problems. A known safety problem is one which can be easily anticipated in advance of deploying a model or easily observed in the model's behavior. Such safety failures can be easily caught with testing, and it seems reasonable to hope that they will be fixed with human feedback. But it seems like there’s much less of a clear story for how we’ll resolve unknown safety problems -- the things we didn’t think to test for and wouldn’t obviously give feedback to fix.

Even if we’re able to anticipate certain safety problems, we may not know if we’re sufficiently disincentivizing them. A model might behave well on the training distribution, then unexpectedly exhibit some safety failure in a context it wasn’t trained in. In the extreme, a model might make a “treacherous turn”[\[1\]](#fn-JZCyxqHavaanGeQar-1) \-- it may use its understanding of the training setup to deliberately behave well only during training, then pursue different goals once it knows it’s outside of the training distribution.

In traditional software engineering, our ability to mitigate unanticipated safety problems largely flows from our ability to understand and carefully reason about code. While testing may catch various kinds of easy to observe or anticipated problems, we rely on code reviews, careful engineering, and even systematic verification to avoid other problems. These approaches are only possible because we can understand code for normal computer programs, something we don’t, by default, get with neural networks.

Neural network parameters can be seen as the assembly instructions of a complex computer program. If it was possible to reverse engineer the parameters of trained neural networks into human-understandable algorithms, it may enable us to catch safety problems the same way we are able to in code.

Recent research has shown that it is possible to reverse engineer modern neural networks into human understandable computer programs, at least on a small scale. The [Circuits Thread](https://distill.pub/2020/circuits/) on Distill contains many examples of reading human understandable algorithms off the weights of neural networks.

There’s also some evidence that this kind of analysis can reveal unanticipated problems and concerns. An [analysis of CLIP](https://distill.pub/2021/multimodal-neurons/) found that the model had neurons related to race, gender, age, religions, LGBT status, mental health, physical disability, pregnancy, and parental status. We can also mechanistically observe concerning uses of these protected attributes, such as an Asian culture neuron increasing the probability of “I feel pressured” or an LGBT neuron increasing the probability of “I feel accepted.” Although there is significant attention to bias in machine learning, it tends to be focused on a couple categories such as race and gender. Surfacing that a model represents other protected attributes is a proof of concept that mechanistic interpretability can surface unanticipated concerns in state of the art models.

We would like to see more research aimed at mechanistically understanding neural networks, at seriously reverse engineering trained models into understandable programs. While we think it’s most likely this will take the form of work in a similar vein to Circuits, we’re also open to other ideas. Research projects should meet the following desiderata:

* Research should map neural network parameters to human understandable algorithms.
* We prefer rigorous understanding of a narrow aspect of a model to less rigorous understanding of entire models.
* Methods should be able to discover unknown and unanticipated algorithms. They should not be based on a priori assumptions about what computation exists in neural networks.
* Methods should be possible to apply to standard, widely used neural networks.
* Methods should have a plausible path to giving a full mechanistic understanding of neural networks.
* Methods should plausibly scale to completely understanding with enough human effort. For example, they shouldn’t explode exponentially as model size or the complexity of the computation being studied increases.

At this stage, we’re interested in work that generically makes progress towards mechanistically understanding neural networks, but it’s worth noting that there are specific questions which are of particular interest from a safety perspective. For example:

* What controls whether a language model generates true or false statements?
* To what extent does the model represent social interaction or mental state? (For example, to what extent does GPT-3 model the mental state, emotions and beliefs of different participants in a dialog?)
* Is the model deliberately deceiving users? (Formalizing exactly what this means would be part of the challenge. One version might be that the model internally represents that a statement is false and produces it anyways. A stronger might be that the model has a model of there being another participant in the dialog which it is aiming to persuade of a falsehood.)
* What is going on in meta-learning? (One of the most impressive properties of modern language models is their in-context meta-learning. Some plausible mechanisms for meta-learning -- notably, [mesa-optimization](https://www.lesswrong.com/posts/FkgsxrGf3QxhfLWHG/risks-from-learned-optimization-introduction) \-- would have significant safety implications. If we understood meta-learning, we might either exclude these mechanisms or recognize them and raise concern.)
* How do large language models store factual knowledge? (It might be useful to access a model’s knowledge without having to rely on it to be truthful.)

Work that addresses one of these would be of particular interest.

The following sections will describe some more specific research directions we think are promising.

## Aspirational Goal: Fully Understand a Neural Network

A useful aspirational goal in this work is to fully reverse engineer any modern neural network, such as an ImageNet classifier or modern language model. There are a number of ways you could potentially operationalize “fully reverse engineer”:

* One has a theory of what every neuron (or feature in another basis) does, and can provide a “proof by induction” that this is correct. That is, show that for each neuron, if one takes the theories of every neuron in the previous layer as a given, the resulting computation by the weights produces the next hypothesized feature. (One advantage of this definition is that, if a model met it, the same process could be used to verify certain types of safety claims.)
* One has a theory that can explain every parameter in the model. For example, for the weights connecting InceptionV1 mixed4b:373 (a wheel detector) to mixed4c:447 (a car detector) _must be positive at the bottom and not elsewhere_ because cars have wheels at the bottom. By itself, that would be an explanation with high explanatory power in the Piercian sense, but ideally such a theory might be able to predict parameters without observing them (this is tricky, because not observing parameters makes it harder to develop the theory), or predict the effects of changing parameters (in some cases, parameters have simple effects on model behavior if modified which follow naturally from understanding circuits, but unfortunately this often isn’t the case even when one fully understands something).
* One can reproduce the network with handwritten weights, without consulting the original, simply by understanding the theory of how it works.

(It’s worth noting that all these can also be applied to _parts of a model_ in addition to the full thing, and in fact have all roughly been achieved for [curve circuits](https://distill.pub/2020/circuits/curve-circuits/).)

At the moment, no one fully understands any non-trivial neural network. Demonstrating that it’s possible to do so is both a natural milestone, and might make society much more willing to invest in this kind of reverse engineering. This goal is aspirational, but a successful project should somehow advance us towards this goal.

We’re open to a range of possibilities as to how it could happen, as long as it’s a genuine milestone towards understanding powerful models. For example, this could be achieved by simply reverse engineering existing models, but a model engineered to be interpretable in some way also seems like fair game, provided it’s equally performant and easy to train. (At the moment, InceptionV1 is by far the closest thing we have to a fully reverse engineered model, about 30% reverse engineered as measured by neuron count. But reverse engineering another model would be equally useful as a milestone.)

Note that even if we are able to fully understand a modern neural network, we are far from our ultimate, even more ambitious goal: a general method for understanding neural networks of arbitrary size and sophistication.

## Research Direction: Discovering Features and Circuits

In the Circuits approach, neural networks are composed of features and circuits. Characterizing features and circuits is the most direct way to move us towards fully understanding neural networks. Examples of doing this kind of work can be found in the Circuits thread (see especially [Curve Detectors](https://distill.pub/2020/circuits/curve-detectors), [Curve Circuits](https://distill.pub/2020/circuits/curve-circuits), and [High-Low Frequency Detectors](https://distill.pub/2020/circuits/frequency-edges); see also [Visualizing Weights](https://distill.pub/2020/circuits/visualizing-weights/) for more detailed discussion of methods for studying circuits).

There are several reasons why it might be useful to study specific features and circuits, especially as a starter project:

* Studying new features and circuits is comparatively low research risk. One can reliably find new interesting features, study the circuits that implement them, and have a fairly interesting result. This makes it a pretty natural entry point for someone starting to work on mechanistic interpretability.
* A major risk of interpretability research seems to be becoming untethered and describing things that don’t really map to what’s going on in the model. Ultimately, being able to describe other research in terms of circuits is a very helpful epistemic check, and getting practice working with circuits is helpful for working up to this.
* Every feature or circuit we understand advances us towards understanding a neural network. If we do enough of this kind of work on a specific network like InceptionV1, and it is possible for humans to understand every neuron/feature in a neural network, we will eventually achieve full understanding. (The assumption that humans can understand every feature is doing a lot of work here, but if true gives you a relatively straightforward path to the inductive definition of full understanding.) It also gives us a foothold for understanding other features in that model, since it’s often easier to understand features once you understand features they’re connected to.
* Because features and circuits are often universal, recurring across many models, every circuit and feature we find gives us a foothold into understanding future models, making it easier and faster to study them. It also makes it easier to study similarities and differences between models, opening up space to study a kind of comparative anatomy of neural networks.

Results on new features and circuits are especially interesting if:

* You find they are universal, forming in many different models.
* They are unique to especially large or sophisticated models, and seem linked to new kinds of capabilities (like the multimodal neurons found in CLIP).

## Research Direction: Scaling Circuits to Larger Models

The main weakness of the circuits approach is that, by focusing on small scale structure, it may not be able to scale to understanding large scale models. [Curve Circuits](https://distill.pub/2020/circuits/curve-circuits/) is the largest example of reverse engineering a circuit to date, at \~50K parameters. This is many orders of magnitude smaller than modern language models. How might we bridge the gap?

One promising direction is to find additional structure which greatly simplifies mechanistically understanding neural networks, or at least simplifies understanding the safety relevant features. The circuits thread describes two such types of structure: “motifs” (recurring patterns in circuits, such as [equivariance](https://distill.pub/2020/circuits/equivariance/)) and “structural phenomena” (large scale patterns in how neural networks are organized, such as [branch specialization](https://distill.pub/2020/circuits/branch-specialization/)).

Equivariance can simplify circuits in early vision by as much as a factor of 50x, so there’s precedence for discovering structure that can give order of magnitude simplifications of neural networks. Similarly, one could imagine a world where something similar to work on branch specialization or research on modularity, can break neural networks into components, where only some of the components are necessary to audit for safety, massively reducing the work needed to ensure models are safe.

Research projects in this category would ideally:

* Demonstrate that the structure they study can simplify understanding features and circuits.
* Avoid making strong a priori assumptions about what structure exists in a neural network.
* Have an argument for how this kind of structure studied could have a large simplifying effect on mechanistically understanding large models, of the kind that could contribute to bridging an order of magnitude gap.

Concrete examples:

* Understanding the natural equivariance to simple transformations like rotation, scale and hue dramatically simplify the study of early vision in conv nets. Are there other kinds of equivariance that might simplify late vision? What about language models?  
A fictional example of what a big success for this approach might look like is “It turns out large language models can mostly be understood in terms of a couple large families of neurons. One family stores factual knowledge with neurons parameterized by variables A, B, and C; the other major types of neurons are …”
* A number of papers (eg. [Filan et al. 2021](https://arxiv.org/pdf/2103.03386.pdf)) have been written about modularity in neural networks. Can we understand how these structures relate to the computation being performed in neural networks ([branch specialization](https://distill.pub/2020/circuits/branch-specialization/) takes preliminary steps in this direction for the special case of architecturally enforced branches)? How well do various notions of modularity organize and simplify the features and circuits in neural networks? Are there other notions that better leverage the graph structure of neural networks to organize them? Can this work be used to isolate parts of a neural network relevant to particular safety questions (see “Specific Questions of Interest” above) and target them?  
A fictional example of what a big success for this approach might look like is “We found a subgraph of neurons which is responsible for social reasoning and it’s only 0.1% of the model. If the model was deliberately trying to mislead us, it would turn up here.”

In addition to these approaches, we’re excited about other approaches to scaling interpretability to much larger models. These approaches should fit the general desiderata listed in the introduction, and have a clear story for why their success would enable significantly better scaling. They should also consider how feasible the approach is to study right now; for example, using large numbers of humans, or integrating with some alignment scheme that provides automation, might ultimately be crucial for scaling interpretability but challenging to study now.

## Research Direction: Resolving Polysemanticity

Another major challenge to circuits is [polysemanticity](https://distill.pub/2020/circuits/zoom-in/#claim-1-polysemantic), where some neurons respond to multiple unrelated features. One theory is that polysemanticity occurs because models would ideally represent more features than they have neurons, and exploit the fact that high dimensional spaces can have many “almost orthogonal” directions to store these features in “[superposition](https://distill.pub/2020/circuits/zoom-in/#claim-2-superposition)” across neurons. Polysemanticity seems related to questions about disentangling representations.

Polysemanticity makes circuits much harder to study and audit, and increases the risk that analysis will miss important structures. For example, imagine one is trying to audit a model for potential bias issues (we see bias as a proxy for a much broader class of safety concerns, but can be studied in models that exist today). If one was to find a circuit where a “female” neuron excites a “nurse” neuron but inhibits a “doctor” neuron, auditors would likely conclude that was an example of bias. But if a “wheel/female/tree” neuron excites a “car/nurse/waterfall” neuron, and there are a number of other neurons which seem to have overlapping features, it’s less clear what to make of it.

* Is there any way to quantify polysematnicity in an automated manner, without relying on human evaluation or a priori assumptions about what features exist?
* If polysemanticity arises because neural networks are trying to represent too many features, and the features are in superposition, one might think of it as a larger model where the neurons and circuits have been “folded over themselves”. Can we “unfold” neural networks into non-polysemantic versions?
* Do neural networks become less polysemantic as we make them large? What about as we train them on more varied data? Or on harder datasets?
* Is there some way to train neural networks which are less polysemantic? (For example, does making models have sparser activations or sparser weights help?)

## Other Directions

This list is far from comprehensive. There are many other questions we’d be interested to see proposals related to. To give a few examples:

* **More easily interpretable models** \- Can we make architectural or training decisions that make features and circuits easier to understand, while preserving the expressivity of models? (Note that designing a model where an individual operation is easier to reason about won’t necessarily mean that circuits or the overall model are easier to understand, since most of the complexity in neural network-like architectures comes from composition of repeated structures.)
* **What occurs at model phase changes?** \- If one looks at the performance of particular tasks, such as arithmetic on numbers of a certain size, across model sizes, one often observes points where larger models discontinuously become better at a task. Discontinuous changes like this are interesting from a safety perspective, since it seems like they could cause a larger model to unexpectedly have safety issues a smaller model did not. What mechanistically occurs in the relevant circuits at these phase changes? Can we automatically detect these phase changes, without knowing what particular behavior might discontinuously change in advance?
* **Model Diffing** \- In practice, we are studying a progression of neural networks of increasing size and sophistication. Universality suggests that the structures we discover in small models will often exist in large models. Can we take this a step further and provide a diff -- analogous to the diff one might get when doing a code review -- of the mechanistic differences between two models, so that we only need to analyze that diff for safety problems?
* **Quadratic Circuits** \- In transformer models, dot products between keys and queries mean that some circuits have a quadratic form. Similarly, contrastive models have dot products between the representations of both encoders, creating quadratic circuits. Are there any special considerations for reasoning about these circuits?

We expect there are many other promising ideas we haven’t listed or considered. We would be excited to receive proposals for other interpretability projects that could help us catch unanticipated safety problems or guarantee good behavior in unusual contexts, if they meet the desiderata in the introduction. Proposals related to scaling mechanistic interpretability to larger models are of particular interest.

## Resources

Several of the Circuits articles provide colab notebooks reproducing the results in the article, which may be helpful references if one wants to do Circuits research on vision models. In particular, [Visualizing Weights](https://distill.pub/2020/circuits/visualizing-weights/) focuses on demonstrating and explaining some of the fundamental techniques. If one wants to study multimodal neurons, OpenAI has [some code](https://github.com/openai/CLIP-featurevis) that may be helpful.

---

1. Nick Bostrom describes this failure mode in Superintelligence, p. 117: “…one idea for how to ensure superintelligence safety… is that we validate the safety of a superintelligent AI empirically by observing its behavior while it is in a controlled, limited environment (a “sandbox”) and that we only let the AI out of the box if we see it behaving in a friendly, cooperative, responsible manner. The flaw in this idea is that behaving nicely while in the box is a convergent instrumental goal for friendly and unfriendly AIs alike. An unfriendly AI of sufficient intelligence realizes that its unfriendly final goals will be best realized if it behaves in a friendly manner initially, so that it will be let out of the box. It will only start behaving in a way that reveals its unfriendly nature when it no longer matters whether we find out; that is, when the AI is strong enough that human opposition is ineffectual.” Additional discussions of the possibility of such failure modes can be found in Hubinger et al.’s [Risks from Learned Optimization in in Advanced Machine Learning Systems](https://arxiv.org/abs/1906.01820) (section 4, “Deceptive Alignment”) and Luke Muelhauser’s post, [“Treacherous turns in the wild”](http://lukemuehlhauser.com/treacherous-turns-in-the-wild/#more-6202). [↩︎](#fnref-JZCyxqHavaanGeQar-1)


