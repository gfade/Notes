---
id: a3cbc3f3-238a-40d1-ba57-ab3152620072
---

# Concrete Steps to Get Started in Transformer Mechanistic Interpretability — Neel Nanda
#Omnivore

[Read on Omnivore](https://omnivore.app/me/https-www-neelnanda-io-mechanistic-interpretability-getting-star-1897da22ee1)
[Read Original](https://www.neelnanda.io/mechanistic-interpretability/getting-started)

**_Disclaimer_**_: This post mostly links to resources I've made. I feel somewhat bad about this, sorry! Transformer MI is a pretty young and small field and there just aren't many people making educational resources tailored to it._ [_Some_](https://www.neelnanda.io/mechanistic-interpretability/prereqs)[_links_](https://www.neelnanda.io/mechanistic-interpretability/favourite-papers) _are to collations of other people's work, and I link to more in the appendix._

## Introduction

_Feel free to just skip the intro and read the concrete steps_

The point of this post is to give concrete steps for how to get a decent level of baseline knowledge for transformer mechanistic interpretability (MI). I try to give concrete, actionable, goal-oriented advice that I think is enough to get decent outcomes - please take this as a starting point and deviate if something feels a better fit to your background and precise goals!

A core belief I have about learning mechanistic interpretability is that **you should spend at least a third of your time writing code** and playing around with model internals, not just reading papers. MI has _great_ feedback loops, and a large component of the skillset is the practical, empirical skill of being able to write and run experiments easily. Unlike normal machine learning, once you have the basics of MI down, you should be able to run simple experiments on small models within minutes, not hours or days. Further, because the feedback loops are so tight, I don’t think there’s a sharp boundary between reading and doing research. If you want to deeply engage with a paper, you should be playing with the model studied, and testing the paper’s basic claims. 

The intended audience is for people new-ish to Mechanistic Interpretability but who know they wantto learn about it - if you have no idea what MI is, check out [this Mech Interp Explainer](https://www.neelnanda.io/glossary), [Circuits: Zoom In](https://distill.pub/2020/circuits/zoom-in/) or [Chris Olah’s overview post](https://www.lesswrong.com/posts/CzZ6Fch4JSpwCpu6C/interpretability).

## Defining “Decent Baseline”

Here’s an outline of what I mean when I say “a decent level of baseline knowledge”

* A good grounding in the key concepts of machine learning and mechanistic interpretability
* An intuition for how a transformer _actually_ works on a mechanical level - what the moving parts are, how it all fits together, and how to reason about the overall system
* Familiarity with tooling, such that you can easily spin up a model and run quick and dirty experiments.
* A rough map of the literature, what’s known in the field, and big categories of open problems - not necessarily a deep knowledge, but hopefully enough to get a sense for techniques used, and where you _could_ go and read a relevant paper if you want to.
* A sense of basic techniques, what compelling evidence about model internals looks like, and how to get started when poking around at a model.

## Getting the Fundamentals

_A set of goal oriented steps that I think are important for getting the fundamental skills. If you feel comfortable meeting the success criteria of a step, feel free to skip it._

Callum McDougall has made [a great set of tutorials for mechanistic interpretability and TransformerLens](https://arena-ch1-transformers.streamlit.app/), with exercises, solutions and beautiful diagrams. This section is in large part an annotated guide to those!

1. **Learn general Machine Learning prerequisites:** There's a certain baseline level of understanding about ML in general that's important context. It's also important to be familiar with an ML framework like PyTorch to actually write code, and to help ground your knowledge.
   * **Resource:** Read[ the Barebones Guide to Mechanistic Interpretability Prerequisites](https://www.neelnanda.io/mechanistic-interpretability/prereqs), and learn the pre-reqs you're missing (see step 2 for more on transformers)
      * **Bonus:** Read the [machine learning section of the mechanistic interpretability explainer](https://dynalist.io/d/n2ZWtnoYHrU1s4vnFSAQ519J#z=FU%5FmI4vJX1gBv3X70upDyjnn), and get your head around most of the ideas
      * **Bonus: Request the** [**ML for Alignment Bootcamp curriculum**](https://airtable.com/shrOOfZIZC4zZtAIr) **and do the first 4 days - this is the best source for really learning ML I’ve come across, though will take a lot of effort!**
   * **Success criteria:** Write and train an MLP in PyTorch to solve MNIST
      * I have deliberately set this success criteria to emphasise that your goal here is to get enough intuition and context that you can learn more. The goal here is _not_ to get a deep knowledge, or to understand all of the sub-fields - ML contains a ton of niches, and this is not on the critical path to exploring MI!
   * **Tips:**
      * Try PyTorch over other frameworks (Jax, Tensorflow, etc) if you’re doing MI. It is best to [Einops](https://einops.rocks/1-einops-basics/) and [einsum](https://rockt.github.io/2018/04/30/einsum) for tensor manipulation - if you don’t use these you’ll introduce a _lot_ of subtle bugs.
      * It's very easy to overestimate how much you need to learn general pre-reqs - when in doubt, move on to MI, and go back when you notice something missing!
2. **Deeply understand transformers:** A key skill in MI is to have a gears-level model in your head of the transformer - what the parameters and activations are and mean, what are all of the moving parts and how do they fit together. You want to build some intuition for what kinds of algorithms a transformer can/cannot implement.
   * **Resource:** Callum McDougall’s [Transformer from Scratch tutorial](https://arena-ch1-transformers.streamlit.app/[1.1]%5FTransformer%5Ffrom%5FScratch) (which links to various further resources)
      * **Bonus**: [Accompanying video tutorials](https://neelnanda.io/transformer-tutorial)
   * **Success criteria:** Write your own GPT-2 in [the template notebook](https://colab.research.google.com/drive/1Zl3zSdli%5FepSfaoQ%5FHeBCuE6dkGWTowd) (no copying and pasting! The notebook comes with tests)
   * **Bonus:** Understanding [A Mathematical Framework for Transformer Circuits](https://transformer-circuits.pub/2021/framework/index.html) (first half, before two layer models). This should significantly refine your intuitions on how a transformer works as a mathematical object
      * **Resource:** Watch [this walkthrough video](https://www.youtube.com/watch?v=KV5gbOmHbjU) on it
         * **Bonus:** Check out the[ explainer section](https://dynalist.io/d/n2ZWtnoYHrU1s4vnFSAQ519J#z=aGu9fP1EG3hiVdq169cMOJId) and [the paper](https://transformer-circuits.pub/2021/framework/index.html)
      * **Success Criteria:** Feel comfortable with each definition in [the explainer section ](https://dynalist.io/d/n2ZWtnoYHrU1s4vnFSAQ519J#z=aGu9fP1EG3hiVdq169cMOJId)
         * **Bonus:** Write a summary!
3. **Familiarise yourself with Mechanistic Interpretability (MI) Tooling and basics:** You want to be able to easily write and run experiments as you learn and explore MI, so it's worth some up front investment to learn what's out there. The goal here is familiarity with the basics, _not_ deep expertise - the best way to really learn tooling is by using it in practice to solve problems that you care about.
   * **Resource**: [Callum McDougall’s tutorials for TransformerLens + Induction Heads](https://arena-ch1-transformers.streamlit.app/[1.2]%5FIntro%5Fto%5FMech%5FInterp)
      * If you’re new to ML coding, I recommend doing your work in a [Colab Notebook](https://colab.research.google.com/) (with a GPU) unless you’re confident you know what you’re doing. You don’t want to be wasting time setting up infrastructure!
   * **Success criteria:** Work your way through the tutorial, compare your work to the answers, and check you understand 80% of the solutions
      * A core goal here is to learn how to use the[ TransformerLens](https://github.com/neelnanda-io/TransformerLens/) library for doing mechanistic interpretability of GPT-style language models.
         * **Bonus**: Use TransformerLens to load GPT-2 Small in a Colab notebook, run the model, and visualise the activations.
   * **Bonus: Data visualization**: A core skill in MI is being good at visualizing data. Neural networks are high dimensional objects, and you need to be able to understand what's going on! My research workflow looks like running an experiment, visualizing the data, staring at the data, being confused, forming more hypotheses, and iterating. Plot data often, and in a diversity of ways.
      * Familiarise yourself with a plotting library. My personal favourite is [Plotly](https://plotly.com/python/getting-started/), but [Matplotlib](https://matplotlib.org/stable/tutorials/index.html), [Bokeh](https://docs.bokeh.org/en/latest/docs/first%5Fsteps.html#first-steps) and [Holoview](https://holoviews.org/) are other options.
         * Some concrete goals: Be able to plot several loss curves on the same plot, make a scatter plot, and display a matrix (imshow), and add axis labels, titles, and line labels.
         * Callum McDougall has [a great Plotly intro](https://www.perfectlynormal.co.uk/blog-plotly-widgets)
         * Matplotlib is the most popular and easiest to google/use ChatGPT or Copilot for. But personally I find it really annoying, unintuitive and limiting.
      * Play around with [Alan Cooney's CircuitsVis](https://github.com/alan-cooney/CircuitsVis) library, which lets you pass in tensors to an interactive visualization and show it in a Jupyter notebook. See the [existing visualizations here](https://alan-cooney.github.io/CircuitsVis)
         * You can write your own visualizations in React, but it's higher effort
   * **Bonus: Other tutorials on mechanistic interpretability, to dig more into things. Just pick any of these that sound interesting, and move on if none of them feel shiny:**
      * [Exploratory Analysis Demo](https://neelnanda.io/exploratory-analysis-demo) (incl [updated version with exercises](https://arena-ch1-transformers.streamlit.app/[1.3]%5FIndirect%5FObject%5FIdentification)), a tutorial for applying standard techniques like activation patching, direct logit attribution and ablations on GPT-2, based on the [interpretability in the wild](https://arxiv.org/abs/2211.00593) paper
      * Callum’s [Interpretability on an Algorithmic Model](https://arena-ch1-transformers.streamlit.app/[1.4]%5FInterp%5Fon%5FAlgorithmic%5FModel) tutorial, investigating how a model balances parentheses
      * [A walkthrough of reverse-engineering modular addition](https://www.youtube.com/watch?v=ob4vuiqG2Go&list=PL7m7hLIqA0hqsReJ0NYhyN3xiFQW9ko1h&index=2), about [my grokking work](https://arxiv.org/pdf/2301.05217.pdf)
4. (Optional) **Learn key concepts in MI**: Get your head around basic concepts in MI, and get an overview of the field. The goal of this step is a whirlwind overview, _not_ to get a deep and perfect knowledge of everything!
   * **Resource**:[ A Comprehensive Mechanistic Interpretability Explainer & Glossary](https://www.neelnanda.io/glossary)
   * **Success criteria**: Read through the whole explainer, and be able to follow the gist of most of it.
      * Feel free to skip or skim sections or definitions that you don’t follow or find interesting.
      * **Concrete goal**: Be able to look at each section in the table of contents, and for 80% have a rough intuition for what that section is about, why you might care about it, and what you should go back to that section for

## Paths for Further Exploration

A slightly less concrete collection of different strategies to further explore the field. **These are different options, not a list to follow in order**. Read all of them, notice if one jumps out at you, and dive into that. If nothing jumps out, start with the “exploring and building on a paper” route. If you spend several weeks in one of these modes and feel stuck, you should zoom out and try one of the other modes for a few days! Further, it’s useful to read through all of the sections, the tips and resources in one often transfer!

### Explore and Build On A Paper

Find a paper you’re excited about and try to really deeply engage with it, this means both running experiments _and_ understanding the ideas, and ultimately trying to replicate (most of) it. And if this goes well, it can naturally transition into building on the paper’s ideas, exploring confusions and dangling threads, and into interesting original research.

* **Resources:**
   * **Resources to find + engage with papers:** [An Extremely Opinionated Annotated List of my Favourite Interpretability Papers](https://www.neelnanda.io/mechanistic-interpretability/favourite-papers),[ Mechanistic Interpretability Explainer](https://www.neelnanda.io/glossary)[ ](https://www.neelnanda.io/mechanistic-interpretability/favourite-papers)and [my various paper walkthroughs](https://www.youtube.com/@neelnanda2469)
   * **Resources to write code**: TransformerLens[ Exploratory Analysis Demo](https://www.neelnanda.io/exploratory-analysis-demo) ([expanded version](https://arena-ch1-transformers.streamlit.app/[1.3]%5FIndirect%5FObject%5FIdentification))
      1. The TransformerLens[ Main Demo](https://www.neelnanda.io/transformer-lens-demo), [intro to mech interp tutorial](https://arena-ch1-transformers.streamlit.app/[1.2]%5FIntro%5Fto%5FMech%5FInterp), and [the techniques section of the explainer](https://dynalist.io/d/n2ZWtnoYHrU1s4vnFSAQ519J#z=M3vTmlndMJTgnL1-t1IAsTaR).
      2. Again, code in a Colab notebook, unless you’re confident you know what you’re doing.
* First, find a paper that excites you. Try reading [this list](https://www.neelnanda.io/mechanistic-interpretability/favourite-papers) or watching [these walkthroughs](https://www.youtube.com/@neelnanda2469), or reading paper introductions. Once you’ve found one you’re excited about, go on a deep dive and read it closely.
* **Code:** As you read the paper, load in the relevant model, and replicate and explore the paper's claims as you read. Don’t stress about being perfect, but try to get the gist.
   * Copy liberally from the tutorials above
   * A key thing to track is what techniques they/you are using, and _why_ we would expect that technique to tell us anything useful. Where would the technique break?
   * Which of their claims feel most suspicious to you?
* **Understand:** Write up a summary of the key ideas, claims and limitations. Make sure you deeply understand what techniques the paper used, and _why_ those techniques have told you anything real about the underlying model(s)
* Good questions to ask as you read:
   * What are the techniques and evidence used in the paper? How do they distinguish between true and false beliefs about the model? Can you see any flaws? What forms of evidence feel stronger vs weaker?
   * What parts of their techniques and results seem model/task specific? What do you predict will generalise?
   * Which parts of the paper feel most cherry-picked?
   * What are the limitations and flaws of the paper?
* Notice what things you’re confused about at the end. Try to figure these out, or ask someone for help (in a pinch, you can always try emailing the authors!)
* **Extend:** There’s a fairly smooth continuum between deeply engaging with a paper and doing original research. What follow-on questions interest you? How can you build on the paper?
   * Check out the tips in the next section for doing good MI research!
   * Keep building on your experiments - can you fully replicate the paper?
   * Investigate any dangling threads you’re curious or confused about. What questions did the paper leave unanswered?
      1. A good default is checking how much the paper’s claims transfer to other models.
   * Read the section of [Concrete Open Problems](https://neelnanda.io/concrete-open-problems) relevant to that paper, and if any problem excites you, go and try to work on it!

### Work on a Concrete Problem

Find a problem in MI that you’re excited about, and go and try to solve it! Note: A good explicit goal is learning and having fun, rather than doing important research. Doing important original research is just really hard, especially as a first project without significant mentorship! **Note:** I expect this to be a less gentle introduction than the other two paths, only do this one first if it feels actively exciting to you! Check out [this blog post](https://www.alignmentforum.org/posts/TAz44Lb9n9yf52pv8/othello-gpt-reflections-on-the-research-process) and [this walkthrough](https://www.youtube.com/watch?v=yo4QvDn-vsU) for accounts of what the actual mech interp research process can look like.

* **Resources**: [200 Concrete Open Problems in Mechanistic Interpretability](https://www.neelnanda.io/concrete-open-problems)
   * **Resources to write code**: TransformerLens[ Exploratory Analysis Demo](https://www.neelnanda.io/exploratory-analysis-demo) ([expanded version](https://arena-ch1-transformers.streamlit.app/[1.3]%5FIndirect%5FObject%5FIdentification))
      1. The TransformerLens[ Main Demo](https://www.neelnanda.io/transformer-lens-demo), [intro to mech interp tutorial](https://arena-ch1-transformers.streamlit.app/[1.2]%5FIntro%5Fto%5FMech%5FInterp), and [the techniques section of the explainer](https://dynalist.io/d/n2ZWtnoYHrU1s4vnFSAQ519J#z=M3vTmlndMJTgnL1-t1IAsTaR).
   * TransformerLens[ Exploratory Analysis Demo](https://www.neelnanda.io/exploratory-analysis-demo) and [the techniques section of the explainer](https://dynalist.io/d/n2ZWtnoYHrU1s4vnFSAQ519J#z=M3vTmlndMJTgnL1-t1IAsTaR).
   * The [TransformerLens](https://github.com/neelnanda-io/TransformerLens) library and the [Main Demo](https://www.neelnanda.io/transformer-lens-demo).
   * Work in a Colab notebook by default!
* The two most important things here are to find a problem you’re excited about, and to have a sense of the basic techniques you’d use to get a foothold on it. Concretely, try skimming through the [200 Concrete Open Problems](https://www.neelnanda.io/concrete-open-problems) sequence and choosing a section that excites you, and then reading the problems in that section and choosing a problem that excites you.
   * Coding is _much_ easier if you’re starting from and editing existing code. Try using [Exploratory Analysis Demo](https://www.neelnanda.io/exploratory-analysis-demo) as a base.
   * Orient your learning around solving the problem, but still spend time learning things! Read the papers that seem most relevant, learn how to use the relevant infrastructure and techniques, etc.
   * If you get consistently stuck, or feel confused and like you’re floundering, go and read around more!
* **Problem choice:**
   * It’s easy to be overwhelmed by the number of problems. If so, go try the deeply engaging with a paper path
   * Ditto, it’s easy to just not be excited by any of the problems. If so, go try the deeply engaging with a paper path! It’s much easier to be excited about a problem when you have more context and can see whyit’d be interesting and how you might make progress.
   * It’s also easy to be a perfectionist and stress about choosing the _best_ problem. This is not the right thing to optimise for here! Pick a problem you’re excited about, and you can always pivot if it turns out to be too hard or too boring or too easy.
   * One angle is to pick your _five_ favourite problems, try each for 1-2 days, and pick your favourite at the end. Aim for hackathon vibes, of being willing to do unprincipled and hacky things, trying to make progress, and seeing whether anything interesting happens.
      * This works best on ones that don’t need major infrastructure set up - but those are a bad fit for your first problem anyway!
* **Tips:**
   * A common mistake is being too ambitious. I recommend choosing a problem from the sequence that’s rated A or B! In particular, when you’re new to a field, your intuition for “this should be easy” will be wildly, wildly miscalibrated. Pick a problem that feels like it should be really easy - if it actually is, then move on to a harder one!
      * **Key lesson:** Research is _always_ harder than you think (even after accounting for this fact)
      * Note that many people need the equal but opposite advice! You _can_ get started on doing research without being really smart, an expert in the field, or having years of experience.
   * Start by working with smaller models! There’s a lot of interesting things to learn from reverse engineering smaller models (anything from a one layer transformer to 2B parameters), but a common mistake is going for the sexiest (ie largest) models. Infrastructure for models too big to fit in one GPU is a massive, massive pain, and you can iterate much faster on smaller models.
      * GPT-J (6B parameters) or LLaMA 7B is a pain but the largest that is reasonable, anything bigger than that is completely not worth the effort.
      * This advice applies 3x for anything that involves fine-tuning (let alone pre-training!) a model of more than 300M parameters (GPT-2 Medium sized)
   * _Aggressively_ red-team your hypotheses. The most common mistake in junior MI researchers is coming up with an elaborate explanation for a seemingly complex behaviour and missing a simple explanation for the behaviour. Or using some high-power techniques (which take a lot of time and effort to set up!) without noticing plausible ways that those techniques could break or be misleading.
      * Familiarise yourself with the results in tiny models in [A Mathematical Framework](https://dynalist.io/d/n2ZWtnoYHrU1s4vnFSAQ519J#z=aGu9fP1EG3hiVdq169cMOJId) \- skip trigrams, bigrams, copying, induction. _Always_ check whether the behaviour could be done with some combination of these.
      * Look for evidence to falsify your hypothesis about the model behaviour, not just confirm it. Try a lot of minor edits to the model’s prompt, and see which ones do and do not break the behaviour.
   * On the flip-side, be willing to _use_ janky and non-rigorous techniques, just don’t _rely_ on them. These can be key inputs into hypothesis formation and exploration, and if a lot of non-rigorous techniques point in the same direction (and aren’t all flawed in the same way) that can be pretty strong evidence! But it’s important to also red-team this and to not blindly trust them.
   * Jump in and get your hands dirty! A common mistake is to spend days to weeks setting up epic infrastructure, or writing a perfect, sophisticated project proposal. Jump in with some quick experiments, trying to get some feedback from reality, and iterating, before you heavily invest.
      * Research is all about tight feedback loops! The vibe should be closer to a weekend hackathon, rather than a 2 month internship.
      * Building yourself good infrastructure is important, but it’s often done best if you’ve done things the hacky way first, and can identify what features do/do not matter

### Read Around the Field (Ie Do a Lit Review)

Go and read around the field. Familiarise yourself with the existing (not that many!) papers in MI, try to understand what’s going on, big categories of open problems, what we do and do not know. Focus on **writing code as you read** and **aim to** **deeply understand a few important papers** rather than skimming many. See Stephen Caspar’s [advice on deep dives](https://www.lesswrong.com/posts/B3z8PMqor3rivzgAv/deep-dives-my-advice-for-pursuing-work-in-research).

* **Resources**: [An Extremely Opinionated Annotated List of my Favourite Interpretability Papers](https://www.neelnanda.io/mechanistic-interpretability/favourite-papers)
   * [The Mech Interp Explainer](https://www.neelnanda.io/glossary) is a good reference for terms
   * [Video walkthroughs](https://www.youtube.com/@neelnanda2469) of A Mathematical Framework, Induction Heads, and Interpretability in the Wild, I recommend watching them before digging too deep into the papers.
   * Read the intro to each section in the [Concrete Open Problems](https://neelnanda.io/concrete-open-problems) sequence, to get a sense of the types of open problem and motivation/background.
* **Recommendation:** It’s easy to read passively, or without fully understanding. Aim for deep engagement, even at the cost of being slower.
   * Good questions to ask as you read:
      * What are the techniques and evidence used in the paper? How do they distinguish between true and false beliefs about the model? Can you see any flaws? What forms of evidence feel stronger vs weaker?
      * What parts of their techniques and results seem model/task specific? What do you predict will generalise?
      * Which parts of the paper feel most cherry-picked?
      * What are the limitations and flaws of the paper?
   * Write code and playing around with the models in question as you read! See the deeply engaging with the paper section for tips.
* **Output:** Try to produce some concrete output for the papers you really like - this forces you to engage much more deeply
   * A blog post on the paper
      * Try aiming for an [Alignment Newsletter](https://rohinshah.com/alignment-newsletter/)\-style summary
   * Explain the paper (in detail!) to a friend
   * Give a talk on them to a reading group/some friends.
   * A Colab notebook replicating some key claims

## Appendix

### Advice on compute

* Rules of thumb - to use and analyse a model up to GPT-2 Medium size, this is easy enough to do in a free colab notebook. If you getting CUDA Out of Memory issues, you want to upgrade to a better notebook.
   * I weakly recommend Colab Pro or [Paperspace Gradient](https://www.paperspace.com/gradient) (a version of colab that gives you a virtual machine behind the notebook, I recommend the $8/month pro plan)
* If you need to do anything that involves running code for >1 hour, or things are super slow, you probably want a dedicated virtual machine. Anything involving training a language model, or running inference for the model on >100M tokens of text will be a pain and require serious compute
   * Try [Paperspace Core](https://www.paperspace.com/core), but it’s pricier

### Other Resources

_See Apart’s_ [_Interpretability Playground_](https://alignmentjam.com/interpretability-playground) _for a longer list, and_ [_a compilation of my various projects here_](https://docs.google.com/document/d/1H%5FTvqkR5jvrETn5ea8YekuFY8ZFOtg4wGWHEWZCOVpo/edit)

* **Tooling**:
   * Nostalgebraist’s [transformer-utils library](https://github.com/nostalgebraist/transformer-utils)
   * Google PAIR’s [Learning Interpretability Tool](https://pair-code.github.io/lit/tutorials/tour/) (LIT)
   * Google PAIR’s [What-If Tool](https://pair-code.github.io/what-if-tool/explore/)
   * Jesse Vig’s [BERTViz](https://github.com/jessevig/bertviz)
   * [LOOM](https://github.com/socketteer/loom/)
* A [real-time research recording](https://www.youtube.com/watch?v=yo4QvDn-vsU) of me reverse engineering a model trained to re-derive its positional embeddings
* [Interpretability-Friendly Models](https://dynalist.io/d/n2ZWtnoYHrU1s4vnFSAQ519J#z=NCJ6zH%5FOkw%5FmUYAwGnMKsj2m) that I’ve trained
* Catherine Olsson on [Getting Started with Mechanistic Interpretability](https://www.youtube.com/watch?v=ll0oduwDEwI)
* Jay Alammar’s [Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)
* Andrej Karpathy’s [MinGPT](https://github.com/karpathy/minGPT)
* [Videos on Transformer Circuits](https://www.youtube.com/watch?list=PLoyGOS2WIonajhAVqKUgEMNmeq3nEeM51&v=V3NQaDR3xI4) from the Anthropic Interpretability team

$\\setCounter{0}$


