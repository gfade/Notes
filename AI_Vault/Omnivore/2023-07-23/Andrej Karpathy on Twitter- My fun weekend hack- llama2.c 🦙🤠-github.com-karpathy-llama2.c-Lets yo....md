---
id: 69322ac2-67df-4307-acdf-37cb0bd78122
---

# Andrej Karpathy on Twitter: My fun weekend hack: llama2.c 🦙🤠
github.com/karpathy/llama2.c
Lets you train a baby Llama 2 model...
#Omnivore

[Read on Omnivore](https://omnivore.app/me/https-twitter-com-karpathy-status-1683143097604243456-18985dc4f71)
[Read Original](https://twitter.com/karpathy/status/1683143097604243456)

My fun weekend hack: llama2.c 🦙🤠[github.com/karpathy/llama2.c](https://github.com/karpathy/llama2.c)Lets you train a baby Llama 2 model in PyTorch, then inference it with one 500-line file with no dependencies, in pure C. My pretrained model (on TinyStories) samples stories in fp32 at 18 tok/s on my MacBook Air M1 CPU.

[ ![](https://proxy-prod.omnivore-image-cache.app/0x0,sFW4PURLxXCm4ovT84nWEgHWgP7D_hAtNbEoDRq0Y6Hk/https://pbs.twimg.com/media/F1u1ckUaIAAalF3.jpg?name=small&format=webp) ](https://pbs.twimg.com/media/F1u1ckUaIAAalF3.jpg?name=small&format=webp)

The inspiration for the project is of course the amazing llama.cpp. The training code is a hacked up nanoGPT modified to train Llama 2 architecture models. The inference code run.c is here: [github.com/karpathy/llama2.c…](https://github.com/karpathy/llama2.c/blob/master/run.c) Thank you GPT-4 for help with my very rusty C <3

[ ![](https://proxy-prod.omnivore-image-cache.app/0x0,sD6zudLhocmuoFBDyHKRqYUpmjs_H_bG_RavcG33SWho/https://pbs.twimg.com/media/F1u3NhzaIAA98uE.jpg?name=small&format=webp) ](https://pbs.twimg.com/media/F1u3NhzaIAA98uE.jpg?name=small&format=webp)

It was surprising to me that you can inference these smaller (O(\~10MB)) models at interactive rates in fp32, in pure single-threaded C on the CPU. Ofc I haven't tried with even the smallest Meta LLama2 released checkpoint (7B), I expect it's too slow.

[ ![](https://proxy-prod.omnivore-image-cache.app/0x0,sMjTM2pKMYyPybiWqS_wdSiGjb18Gw-NYbrXyzu6j_7A/https://pbs.twimg.com/media/F1u5sObacAAgZNz.jpg?name=small&format=webp) ](https://pbs.twimg.com/media/F1u5sObacAAgZNz.jpg?name=small&format=webp)

Still, in narrow domains (e.g. stories) one can get away with surprisingly small Transformers doing interesting things, so this simple pure C implementation might be useful and portable.

Update 1: so compiling with -O3 increases the tok/s from 18 to 98 on my MacBook Air M1\. I didn't expect that to help as much. Sounds like I have to train a bigger model now.

Update 2: compiling also with -funsafe-math-optimizations increases tok/s to 315 tok/s! So we are 17.5X faster just by including a few more characters in the gcc command. Cue the "got any more of them gcc flags" meme. Also \~8% speedup from a fused softmax that -O3 doesn't catch.

Update 3: also included -Ofast and -ffast-math and now I'm up to 534 tok/s. This is getting comical... 😅

 — [karpathy](https://twitter.com/karpathy) Andrej Karpathy [July 23, 2023, 3:52 PM UTC](https://twitter.com/karpathy/status/1683143097604243456) 


