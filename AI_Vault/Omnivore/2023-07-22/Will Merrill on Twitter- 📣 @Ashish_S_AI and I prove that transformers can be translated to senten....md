---
id: cda74c12-51d0-4f53-8891-ea2c2fe3c13b
---

# Will Merrill on Twitter: 📣 @Ashish_S_AI and I prove that transformers can be translated to sentences in first-order logic ...
#Omnivore

[Read on Omnivore](https://omnivore.app/me/https-twitter-com-lambdaviking-status-1662127858138095622-1897da330af)
[Read Original](https://twitter.com/lambdaviking/status/1662127858138095622)

📣 [@Ashish\_S\_AI](https://twitter.com/Ashish%5FS%5FAI) and I prove that transformers can be translated to sentences in first-order logic with majority-vote quantifiers (FOM). FOM is a symbolic language that can capture computation inside transformers![arxiv.org/abs/2210.02671](http://arxiv.org/abs/2210.02671)

[ ![](https://proxy-prod.omnivore-image-cache.app/0x0,sPWUQ1igc8c1By0rt5T_GhJNPak5Yat0FAW8_ItgB4iI/https://pbs.twimg.com/media/FxEQQJWaEAEPDEo.png?name=small&format=webp) ](https://pbs.twimg.com/media/FxEQQJWaEAEPDEo.png?name=small&format=webp)

This result acts as an upper bound: transformers can't solve problems that can't be defined in FOM. This reveals some new problems transformers can't solve and provides a handy intuitive test for seeing whether a transformer can do something: try to define the problem in FOM.

We also see natural implications of this work for understanding algorithms inside transformers ("mechanistic interpretability"). RASP/TRACR are languages for \*compiling into\* transformers. In contrast, any transformer can be \*translated\* to an FOM sentence.

Another contribution: we prove transformers need >loglogn precision to have full expressive power over contexts of length n. With less precision, they cannot implement uniform attention! We hope this result can guide the development of long-context, low-precision LMs.

Bibliographic notes: This paper is a substantially revised version of an earlier preprint. The revisions were inspired by [@davidweichiang](https://twitter.com/davidweichiang) et al.'s related paper:[arxiv.org/abs/2301.10743](https://arxiv.org/abs/2301.10743)

And, copying link again for our paper since the arXiv preview didn't render above:[arxiv.org/abs/2210.02671](http://arxiv.org/abs/2210.02671)

 — [lambdaviking](https://twitter.com/lambdaviking) Will Merrill [May 26, 2023, 4:05 PM UTC](https://twitter.com/lambdaviking/status/1662127858138095622) 


