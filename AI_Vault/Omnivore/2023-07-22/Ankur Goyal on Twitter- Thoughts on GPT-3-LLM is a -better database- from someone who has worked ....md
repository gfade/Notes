---
id: 1a129d1e-21b3-49c8-aa60-17fe86b9bd1e
---

# Ankur Goyal on Twitter: Thoughts on GPT-3/LLM is a "better database" from someone who has worked on relational databases ...
#Omnivore

[Read on Omnivore](https://omnivore.app/me/https-twitter-com-ankrgyl-status-1584776019130871808-1897da7c160)
[Read Original](https://twitter.com/ankrgyl/status/1584776019130871808)

Thoughts on GPT-3/LLM is a "better database" from someone who has worked on relational databases for over a decade and AI for half. tl;dr I think they have the potential to be (1/n)

First, a quick example. Let's query some knowledge about the S&P 500\. Assuming you had growth rates saved in a database, this would be a SQL query like: > SELECT "year" FROM sp\_growth ORDER BY "growth\_rate" DESC LIMIT 1

[ ![](https://proxy-prod.omnivore-image-cache.app/0x0,soXZyJRy1oP1UsfzxktGeSLtwwSl_ZOiYcv8aN2DSvWI/https://pbs.twimg.com/media/Ff45ksAVQAEmV9h.jpg?name=small&format=webp) ](https://pbs.twimg.com/media/Ff45ksAVQAEmV9h.jpg?name=small&format=webp)

One way of thinking about this pattern is "LLMs are an index". This is limiting b/c LLMs support unstructured data, but let's start here. Indexes are measured by query perf, storage size, and update cost.

LLM queries are remarkably fast (constant time) for almost any query (w/ tunable cost via max length). The tradeoff of course is accuracy, since you cannot guarantee correctness. Note in my prompt I asked for citations. Verifying truthfulness is an active area of research.

Storage size/compression also exciting. [@EMostaque](https://twitter.com/EMostaque) has a great line about Stable Diffusion is Pied Piper because of how efficiently it compresses \~5B images into \~4GB of weights. Columnar compression is usually 4-10x, not 1000x.

However, data loading is very, very difficult. Database indexes incrementally update w/ new data. With LLMs, you need to fine tune a model with both a representative set of input questions and the underlying data jointly.

Memory transformers ([arxiv.org/abs/2006.11527](https://arxiv.org/abs/2006.11527)) are one attempt at solving for this. Generally speaking, I think splitting out the data from the reasoning capabilities will be a requirement for this use case.

I'm personally very optimistic about this intersection. Imagine a database that can answer SQL queries, natural language questions, or a combination of both! Lots of challenges to solve around accuracy & perf, but the basic pieces are all there.

Thanks [@sivil\_taram](https://twitter.com/sivil%5Ftaram) for brainstorming these ideas with me 🙏

 — [ankrgyl](https://twitter.com/ankrgyl) Ankur Goyal [October 25, 2022, 5:16 AM UTC](https://twitter.com/ankrgyl/status/1584776019130871808) 


