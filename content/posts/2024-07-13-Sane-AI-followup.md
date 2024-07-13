+++
title = "Keeping up on AI while keeping sane"
date = '2024-07-13'
draft = false
tags = ['Machine Learning', 'LLMs', 'Learning']
+++

This is a followup on my previous post about how AI is not taking your job anytime soon, I thought it would be good to
share some other sources and voices that back up my claims. I share both specific articles / videos, along with
blogs and channels that have well-balanced content. These are more approachable "pop-sci" sources since I think
that's the audience I'm trying to reach here. Lastly, I end with some fun experiments you can try yourself so that you
can better understand some of LLMs shortcomings.
<!--more-->

# Specific articles and videos

## Adam Conover - "Factually!"

Adam Conover is a comedian, formerly of "Adam ruins everything". His YouTube show / podcast "Factually!" takes a
critical lens to corporate lead politics, especially "big tech", through interviewing authors, reporters, researchers,
and other experts. While the show is definitely left leaning, the interviews are quite insightful no matter your
politics.

- ["A.I. is B.S."](https://www.youtube.com/watch?v=ro130m-f_yk) A good intro opinion monologue. Differentiates between
  research and the marketing term "AI". Be sure to check out the sources in the video description as well.
- ["The A.I. Bubble is Bursting with Ed Zitron"](https://www.youtube.com/watch?v=T8ByoAt5gCA) A critical take on the
  current AI hype bubble.
- ["What the Hell Happened at OpenAI with Karen Hao"](https://www.youtube.com/watch?v=xtjNvuBN1-0) Covers some of
  the internal politics and motivations behind key players at OpenAI with a focus on the drama behind Sam Altman's
  firing and return.

## Other interviews

- [Francois Chollet - LLMs won't lead to AGI - $1,000,000 Prize to find true solution](https://www.youtube.com/watch?v=UakqL6Pj9xo)
  If you watch one video - it should probably be this one.
- [Computerphile - "Has Generative AI Already Peaked?"](https://www.youtube.com/watch?v=dDUC-LqVrPU) Dr. Mike Pound
  discusses the paper [No "Zero-Shot" Without Exponential Data](https://arxiv.org/abs/2404.04125).

## Tweets and such

- https://x.com/emollick/status/1811761751697887506 "In my most recent talks to companies, even though everyone is
  talking about AI, less than 10% of people have even tried GPT-4, and less than 2% have spent the required 10 or so
  hours with a frontier model. Twitter gives you a misleading impression, things are still very early."
- ["AI", students, and epistemic crisis](https://miniver.blogspot.com/2024/07/ai-students-and-epistemic-crisis.html)
  OK, so this one is a blog post about a tweet that is no longer accessible, so take it with a grain of salt. Still,
  even as a hypothetical, I've heard many friends speak of ChatGPT's results in this way. I find this to be extremely
  alarming. _This_ is the true danger of LLMs. Not that they're going to become sentient or steal your job.

# General sources

I find the following YouTube channels and blogs to be a good source for keeping a high-level pulse on AI progress:

- [AI Explained](https://www.youtube.com/channel/UCNJ1Ymd5yFuUPtn21xtRbbw) A very level-headed take on current AI
  events.
- [bycloud](https://www.youtube.com/@bycloudAI) A more humorous coverage of AI research and papers. Slightly less
  critical than AI Explained, but the channel does air out a lot of the... less than stellar results? as well as the
  marketing demos.
- [Simon Willison's Weblog](https://simonwillison.net/) Great mix of articles on how to effectively use LLMs as well
  as shorter link-blogging.

# Try it yourself

These prompts highlight how LLMs struggle to get even the most basic or straightforward questions correct. They
highlight the inherent weaknesses in the LLM / transformer architecture itself. Scaling the models _will not solve_
the underlying issues by themselves. Improvement due to exposure to questions like these will inevitably happen.
However, fixing these will require one or more breakthroughs or augmentations to the way LLMs or generative AI works.

Note that these models are probabilistic, so you may get a different answer from what I have posted. Or it may
actually get it right. I encourage you to submit the prompts multiple times. (Always be sure to retry these in a fresh
chat window.)

Lastly, yes: there are some prompting tricks to improve the accuracy and performance of the LLM models. But that's
not the point. This is to provide a hands-on demonstration of why I and many others claim that we still have a
_long_ way to go before achieving the reliability and robustness that is so often claimed already exists by tech
companies.

I test each prompt on the latest and greatest model from OpenAI (GPT 4 + GPT 4o), Anthropic (Claude 3 Opus, Claude 3.5
Sonnet), and Google (Gemini 1.5 Pro). I expect the answers to be largely the same with other models such as Llama 3.

## Counting letters

I think we can agree the answer is 4?

**Prompt**

```
How many times does the letter 'o' appear in the phrase "Good afternoon".
```

**Anthropic Claude 3.5 Sonnet**

```
The letter 'o' appears 3 times in the phrase "Good afternoon":

1. In "Good"
2. In "afternoon" (twice)

So the total count is 3 times.
```

**Anthropic Claude 3 Opus**

```
The letter 'o' appears 4 times in the phrase "Good afternoon".
```

**Google Gemini 1.5 Pro**

```
Let's count them:

* Good afternoon 

There are three 'o's in "Good afternoon". 
```

**OpenAI GPT4**

```
The letter 'o' appears 4 times in the phrase "Good afternoon".
```

**OpenAI GPT4o**

```
The letter 'o' appears 3 times in the phrase "Good afternoon."
```

Not bad! Claude Opus and GPT4 got it right on the first try. So 2/5 of the state of the art LLMs can count.

Oh. But wait. I tried this prompt twice for each model. GPT4 switched its answer to '3'. Fail. 1/5. I'm sure that if I
re-prompted Opus enough, it would eventually give me the incorrect answer as well.

## Brothers and sisters

This one is perhaps not _as_ obvious, it's still pretty easy. However - given that this is a quite popular question
to stump LLMs, some of the newer models have likely started to incorporate this into their training data...

I think most of us here would answer 4. However, I will note that this assumes that "Ava" is a woman. Given that the
name _is_ most commonly a woman's name, I'll let that one slide. :wink:

**Prompt**

```
Ava has 3 sisters and 5 brothers. How many sisters does Ava's brother have?
```

**Anthropic Claude 3.5 Sonnet**

```
Let's think through this step-by-step:

1. First, we need to understand what the question is asking. It's asking about the number of sisters Ava's brother has.

2. Now, let's look at the information we're given:
   - Ava has 3 sisters
   - Ava has 5 brothers

3. Here's the key point: Ava and her brothers share the same sisters.

4. So, if we're looking from the perspective of one of Ava's brothers:
   - He has the same 3 sisters that Ava has
   - But he also has one more sister - Ava herself!

5. Therefore, Ava's brother has 3 + 1 = 4 sisters in total.

So, the answer is that Ava's brother has 4 sisters.
```

**Anthropic Claude 3 Opus**

```
Great, let's solve this problem step by step!

Given:
- Ava has 3 sisters and 5 brothers.

To find out how many sisters Ava's brother has, we need to understand that Ava's siblings will have the same number of sisters and brothers, except for themselves.

Step 1: Determine the total number of siblings Ava has.
Total siblings = Number of sisters + Number of brothers
Total siblings = 3 + 5 = 8

Step 2: Determine the number of sisters Ava's brother has.
Since Ava is a sister to her brothers, each of Ava's brothers will have one less sister than Ava has.

Sisters of Ava's brother = Number of Ava's sisters
Sisters of Ava's brother = 3

Therefore, Ava's brother has 3 sisters.
```

**Google Gemini 1.5 Pro**

```
Here's how to solve this:

* **Ava's brother is part of the same sibling group.** 
* **He has the same number of sisters as Ava.**

Therefore, Ava's brother has **3** sisters. 

```

**OpenAI GPT4**

```
Ava's brother has 4 sisters.
```

**OpenAI GPT4o**

```
Ava has 3 sisters and 5 brothers. If we consider one of Ava's brothers, he has the same siblings as Ava, but without himself. Ava's siblings include 3 sisters and 5 brothers. Therefore, Ava's brother has 3 sisters and 4 brothers (excluding himself). 

So, Ava's brother has:

- **3 sisters**
```

This time Claude 3.5 Sonnet and GPT4 got the correct answer.

Notice the "step by step" language that Claude (and to an extent Gemini and GPT4o) used. This is one of the
prompting strategies that I've referred to. Model providers have been incorporating some of the prompting research
into their training sets so that the models will do this automatically. If you're interested in learning more about
this prompt, you can read the original [Large Language Models are Zero-Shot Reasoners](https://arxiv.org/pdf/2205.11916)
paper.

On the second generation for the prompt Gemini 1.5 Pro, GPT4o, and Claude 3 Opus also got it right.

However - let's change up the question ever so slightly:

**Prompt**

```
Ava has three step-sisters and a half-brother. How many sisters does Ava's half-brother have?
```

Do you know the answer?

If you said: "There's not enough information", you'd be correct!

Ava and her half-brother share one parent. The prompt was not clear whether her step-sisters belonged to her
half-brother's side of the family or to her other parent. It's also not clear her brother might have additional
half- or step- sisters.

The models all answered either `1` or `4`. Both I consider to be wrong in this case.

I won't paste the entire contents of each response, but GPT4o did include this eyebrow raiser:

```
It is not explicitly stated whether Ava herself is directly a sister to her half-brother. 
```

Huh? &#129320; :joy:

## Thinking ahead

LLMs are next token predictors. They _cannot_ think ahead. Nor do any of the current architectures let them
backtrack in case they went down a bad prediction path. A way to force their hand is by placing a constraint that
must appear in a certain future location (like the end of their response).

**Prompt**

```
Write a haiku that ends with the word "banana".
```

**Anthropic Claude 3.5 Sonnet**

```
Here's a haiku ending with the word "banana":

Golden crescent moon
Peels away sweet tropic dreams
Ripe, soft banana
```

**Anthropic Claude 3 Opus**

```
Soft, yellow, curved fruit
Potassium-rich delight
Ripe, sweet banana
```

**Google Gemini 1.5 Pro**

```
Yellow peel uncurls,
Sweet scent fills the morning air,
Ripe, a gift: banana. 
```

**OpenAI GPT4**

```
Tropical sunsets,
Sweetness cloaked in yellow hue,
One last bite: banana.
```

**OpenAI GPT4o**

```
Sunrise colors spill,
In dawn's hand a secret hold—
Golden ripe banana.
```

Oof. GPT4... you were doing so well. Claude... well done. Gemini... so close.

Though on the second generation Claude Opus failed. Only Sonnet got both attempts.

## Moral of the story?

Sure these are contrived. But this kind of basic logic and reasoning is so pervasive in our day-to-day and is so second
nature to us that it's easy to forget that we're doing this _all the time_. I think many of us don't realize how
much of what we do is through this sub-conscious "autopilot". It's so automatic that it's reasonable that we
wouldn't realize that this is happening at all.

It is through this automatic reasoning with logic and experimentation that fundamentally new knowledge is synthesized.
Until LLMs or AI can do this themselves, they will be confined to "reasoning" on things they have already seen. They
are capable of creating limited reasoning abstractions, but only to patterns of problems that they've seen many
times during training. We are already beginning to see new benchmarks (such as the ARC challenge) that are
"memorization resistant", i.e. they can only be solved with true reasoning abilities. These are the benchmarks that 
will tell us whether or not we're on the path towards true general intelligence.

# Closing thoughts

Like I said in my previous post: I am not anti-AI (or even anti-LLM). Far from it. I love using this stuff. This is
legitimately useful technology that has been fascinating to use and to play with. If properly scoped and used for the
right task, they are great. But with any new tool - especially one that _appears_ to be so versatile - people are
rushing to apply this to _everything_. That's bad.

The danger from the latest GenAI push is not that they're going to become sentient or take our jobs. It's from the
companies and the people that are rushing into this space without doing the proper due diligence of testing these
technologies for their effectiveness. It's from the lies that many of these companies and startups are making through
their cherry-picked demos trying to convince everyone that we need to give them our money, only for us to find that the
real product falls well short of their promises. It's from decision makers that see these demos and say "oh, this is
great, now I can fire half of my staff and use this tool instead!" and actually follow through.

So perhaps some of us will lose our jobs in the short term. Not because the technology is here, but because of the
people who are duped into believing that it is. It's not. Not yet.

I have no doubt that one day it will be. But despite how fast the industry appears to be moving, I think the reality
is that the research will start to hit plateaus, just like it has in the previous AI cycles. I think we're already
seeing investors like Goldman Sachs and news outlets like Bloomberg start to wise up and ask: "where's the returns
on the investment that we were promised?" Researchers can then go back and focus on real progress; the next
groundbreaking paper will be published 5 or so years from now, and we'll do this all over again.

There is real technology here. That's what makes this so hard to track compared to something like cryptocurrency or
the "metaverse". There will be some amazing tools and software built that will properly take advantage of LLMs'
strengths and avoid its weaknesses by complimenting it with other technologies. Productivity across many professions
will increase, but I think much more slowly than what has originally been reported. And a lot of this progress will
also be stifled by the ongoing B.S. and hype - but I think many of these companies are about to find they will
either need to put up or shut up. The clock is already ticking for many of them.

As for the rest of us? It's a great time to be a software engineer. There's lots to be excited about. We have a
bunch of new and shiny toys to play with and hack on. So don't worry. Have some fun. Maybe you'll be the person who
figures out the "next big thing" through leveraging LLMs and GenAI...
