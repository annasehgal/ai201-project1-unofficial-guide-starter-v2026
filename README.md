# The Unofficial Guide

Anna Sehgal, Corpus: City Guides

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

This project is a retrieval augmented system that lets users ask questions about travel, eating, and places to visit from the `city_guides` corpus. The system processes 14 city and regional guides, divides them into topic-based chunks with a heading for each topic, and uses embeddings to find the chunks that are relevant to the question asked. A relevance cutoff helps prevent the system from answering out-of-scope questions that are not covered in the corpus through a refusal. It only answers questions based on the information present in the selected corpus, which is picked in `config.py`, with test questions in `questions.py` related to the selected corpus. It uses chunks of up to 500 characters with no overlap and gives a short response based on the retrieved information, including the source document so the user knows where the information came from.

## Chunking Strategy

**Chunk size:** 500 characters
**Overlap:** 0 characters

I chose 500 characters because my city guides contain distinct labeled sections covering specific topics. Each section in the documents contains about 450 words, so 500 characters felt like a reasonable size to capture enough context for a chunk to answer a question while keeping different topics from being combined into one large chunk. I chose 0 overlap because the guides are already organized into topic-based sections, so repeating text between chunks is not necessary.

## Sample Chunks

**Chunk 1** — source: `guide_accessibility.md#0 ` — produced by: `chunker.py::split_documents`

```
# Getting around the region with limited mobility

An honest assessment rather than a promotional one. Some of these places are
difficult and it is better to know in advance.
```

**Chunk 2** — source: `guide_corry_vale.md#4` — produced by: `chunker.py::split_documents`

```
## What to see

The valley itself is the attraction. The footpath network is dense and well marked, and a circuit taking in three of the four villages is about nine miles with 500 metres of ascent. The chapel in the second village is 12th century and always unlocked.
```

**Chunk 3** — source: `guide_givens_mill.md#4 ` — produced by: `chunker.py::split_documents`

```
## What to see

The mill runs tours on the hour from 11 to 3 and the machinery is operating during them, which is loud and much more impressive than a static exhibit. The church has a Saxon doorway. The river walk downstream reaches Brightwater in about three hours.
```

**Chunk 4** — source: `guide_marchwood.md#3` — produced by: `chunker.py::split_documents`

```
## Eat and drink

The best eating is in the Northgate district, a 12-minute tram ride from the station, where about thirty restaurants sit within four streets. The area immediately around the station is uniformly poor and expensive. Marchwood keeps later hours than anywhere else in the region — kitchens serve until 10:30pm, and until midnight on Fridays and Saturdays.
```

**Chunk 5** — source: `guide_seasons.md#2` — produced by: `chunker.py::split_documents`

```
## Summer, June to August

June is excellent everywhere. July and August split: Halden Bay becomes very
busy and the parking problem dominates, Kestrelford fills with walkers, and
Brightwater goes quiet to the point of dullness with the university empty.
```

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:**
Where can visitors eat in Corry Vale?

**Answer:**

```
Visitors in Corry Vale can buy bread and cheese from the farm shop at the valley mouth (guide_eating.md).
```

**My relevance cutoff:**
0.6

| Question | In corpus? | Best distance |
|---|---|---:|
| Where can visitors eat in Corry Vale? | Yes | 0.4026 |
| Is September a good month to visit Brightwater? | Yes | 0.2532 |
| How long does the coastal path from Halden Bay to the lighthouse take? | Yes | 0.1775 |
| How accessible is Kestrelford for walking? | Yes | 0.3960 |
| How is the mobile coverage in Halden Bay? | Yes | 0.4405 |
| What is the capital of Mongolia? | No | 0.8026 |
| How do I change the oil in a diesel engine? | No | 0.8917 |
| Who won the 1994 World Cup? | No | 0.9747 |
| What is the recommended dosage of ibuprofen for a headache? | No | 0.8486 |
| How do I write a for loop in Rust? | No | 0.8130 |

The in-corpus questions had best distances from 0.1775 to 0.4405. The out-of-corpus questions had best distances from 0.8026 to 0.9747. There was a gap between 0.4405 and 0.8026, so I kept the cutoff at 0.6 because it falls within that gap and separates the two groups.

## How I Used AI


**1.** During Milestone 3, I used AI to help develop my custom chunker for the city guides. My first version produced 119 chunks, and one of the sample chunks only contained the sentence “The Kestrelford Saturday market builds back to full size through April.” without the heading for that topic. I changed the chunking logic so that headings stay with the content they introduce when a section needs to be split. The final version produced 115 chunks.

**2.** During Milestone 4, I used AI to help evaluate whether my retrieval settings needed to be changed. I tested my 5 in-scope and 5 out-of-scope questions and compared their best embedding distances. The in-scope questions ranged from 0.1775 to 0.4405, while the out-of-scope questions ranged from 0.8026 to 0.9747. After reviewing the gap between the two groups, I decided that the existing 0.6 relevance cutoff was working well enough, so I did not change it.


---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 |  |  |  |
| 2 |  |  |  |
| 3 |  |  |  |
| 4 |  |  |  |
| 5 |  |  |  |

## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

## The Improvement

**What I changed:**

**Why I picked it:**

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
