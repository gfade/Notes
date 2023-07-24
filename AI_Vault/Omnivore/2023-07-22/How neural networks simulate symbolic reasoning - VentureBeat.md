---
id: cf55fcbe-fdeb-48d0-8eae-b3f177db2bdf
---

# How neural networks simulate symbolic reasoning | VentureBeat
#Omnivore

[Read on Omnivore](https://omnivore.app/me/https-venturebeat-com-ai-how-neural-networks-simulate-symbolic-r-1897dac5892)
[Read Original](https://venturebeat.com/ai/how-neural-networks-simulate-symbolic-reasoning)

December 10, 2021 9:40 AM 

![An image of a blue and purple neural network waveform.](https://proxy-prod.omnivore-image-cache.app/750x392,s1z72U5FpSqfTXLJjixvLiSPF2JU8UJ8POeuieikD4BA/https://venturebeat.com/wp-content/uploads/2021/10/shutterstock_1703415496-1.jpg?fit=750%2C392&strip=all)

_Image Credit: Yurchanka Siarhei // Shutterstock_

**_Head over to our on-demand library to view sessions from VB Transform 2023\. [Register Here](https://events.venturebeat.com/transform-2023/?utm%5Fsource=vb&utm%5Fmedium=Boiler&utm%5Fcontent=landingpage&utm%5Fcampaign=T23%5FBoiler)_**

---

Researchers at the University of Texas have discovered a new way for [neural networks](https://venturebeat.com/2021/05/25/the-business-value-of-neural-networks/) to simulate symbolic reasoning. This discovery sparks an exciting path toward uniting deep learning and [symbolic reasoning AI.](https://venturebeat.com/2021/04/02/why-ai-cant-solve-unknown-problems/)

In the new approach, each neuron has a specialized function that relates to specific concepts. “It opens the black box of standard deep learning models while also being able to handle more complex problems than what symbolic AI has typically handled,” Paul Blazek, University of Texas Southwestern Medical Center researcher and one of the authors of the [_Nature_ paper](https://www.nature.com/articles/s43588-021-00132-w), told VentureBeat.

This work complements previous research on neurosymbolic methods such as [MIT’s Clevrer](https://venturebeat.com/2020/04/28/mit-researchers-release-clevrer-to-advance-visual-reasoning-and-neurosymbolic-ai/), which has shown some promise in predicting and explaining counterfactual possibilities more effectively than neural networks. Additionally, DeepMind researchers previously [elaborated](https://venturebeat.com/2020/12/21/deepmind-researchers-claim-neural-networks-can-outperform-neurosymbolic-models-on-visual-tasks/) on another neural network approach that outperformed state-of-the-art neurosymbolic approaches.

## Essence neural networks mimic human reasoning

The team at the University of Texas coined the term, “essence neural network” (ENN) to characterize its approach, and it represents a way of building neural networks rather than a specific architecture. For example, the team has implemented this approach with popular architectures such as convolutional neural net and recurrent neural net (RNN) architectures.

### Event

VB Transform 2023 On-Demand

Did you miss a session from VB Transform 2023? Register to access the on-demand library for all of our featured sessions.

[ Register Now ](https://avolio.swapcard.com/Transform2023/registrations/Start?utm%5Fsource=vb&utm%5Fmedium=incontent&utm%5Fcontent=landingpage&utm%5Fcampaign=T23%5Fincontent) 

The big difference is that they did away with backpropagation, which is a cornerstone of many AI processes. “Backpropagation famously opened deep neural networks to efficient training using gradient descent optimization methods, but this is not generally how the human mind works,” Blazek said. ENNs don’t use backpropagation or gradient descent. Rather, ENNs mimic the human reasoning process, learn the structure of concepts from data, and then construct the neural network accordingly.

Blazek said the new technique could have practical commercial applications in the next few years. For example, the team has demonstrated a few ENN applications to automatically discover algorithms and generate novel computer code. “Standard deep learning took several decades of development to get where it is now, but ENNs will be able to take shortcuts by learning from what has worked with deep learning thus far,” he said.

## Promising applications of the new technique include the following:

1. **Cognitive science**: The researchers designed ENNs as a proof-of-principle for their new neurocognitive theory. It integrates ideas from the philosophy of mind, psychology, neuroscience, and artificial intelligence to explore how the human mind processes information. The theoretical framework could prove beneficial in exploring various theories and models from all these fields.
2. **Algorithm discovery**: The researchers found that ENNs can discover new algorithms, similarly to how people can.
3. **High-stakes applications**: The research establishes basic building blocks for explainable deep learning systems that can be better understood before deployment and _post hoc_ analysis.
4. **Robust AI:** There has been great concern about adversarial attacks against black-box AI systems. ENNs are naturally more robust to adversarial attacks, particularly for symbolic reasoning use-cases.
5. **Machine teaching with limited data**: An ENN can train on limited, idealistic data and then generalize to much more complex examples that it has never seen.

## Working backward from biology to understand the brain

In contrast to most AI research, the researchers approached the problem from a biological perspective. “The original purpose of our work was to understand how [the neuronal structure of the brain](https://venturebeat.com/2021/06/03/a-simple-model-of-the-brain-provides-new-directions-for-ai-research/) processes information,” Blazek said.

The team ultimately proposed a generalized framework for understanding how the brain processes information and encodes cognitive processes. The core idea is that each neuron makes a specialized distinction, either signifying a specific concept or differentiating between two opposing concepts. In other words, one type of neuron makes the distinction “like A” versus “not like A,” and the other kind of neuron makes the distinction “more like A” versus “more like B.”.

These neurons are arranged in an appropriate hierarchy to integrate these distinctions and arrive at more sophisticated conclusions. There are many ways to design the specialized distinction made by each neuron and to arrange the neurons to make complex decisions.

This theory of understanding neural information processing agrees with various theories and observations from philosophy of mind, psychology, and neuroscience. “The surprising thing about this framework is that the neurons reason about ideas in the exact same way that philosophers have always described our reasoning process,” Blazek said.

**VentureBeat's mission** is to be a digital town square for technical decision-makers to gain knowledge about transformative enterprise technology and transact. [Discover our Briefings.](https://info.venturebeat.com/website-preference-center.html?utm%5Fsource=VBsite&utm%5Fmedium=bottomBoilerplate)


