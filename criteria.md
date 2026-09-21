# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
One of my questions asks about eating in Corry Vale, and that information is specifically present in the Corry Vale guide only. I expect most questions to retrieve the relevant guide, but I chose 4 of 5 because one question may  be harder if the information is less directly stated.

---


Every answer the system produces names at least one source document.

**Why this target:**
I chose all five because each of my questions asks about information covered in a specific city guide, so the system should have a source document to cite for every answer. This could fail if the system generates an answer without including a source or retrieves information from a different guide, but I expect the source requirement in the pipeline to make this achievable.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

**Why this target:**
I chose 4 of 5 because these questions are fully out of scope from the corpus related to city guide, so it should return "I don't have enough information about that" and reject at least 4 of these questions. One of the tests could fail due to word overlap leading to out-of-scope question to pass the relevance cutoff.

---

## 4. Something about your chunks

At least 4 of 5 sampled chunks contain complete information about a specific topic without cutting off the relevant information.
       
**Why this target:**
The city guides are organized into sections covering specific topics such as eating, getting around, and places to see. I want most chunks to preserve a complete piece of information from one of these topics so the information can be understood when retrieved.


---

## 5. Your choice

For at least 4 of 5 ambiguous questions that do not specify a city, the answer identifies which city the information refers to. 

**Why this target:**
I picked 4 of 5 because most guides contain information about similar topics, such as food and transportation, so the answer should make it clear which city the information comes from. I chose 4 instead of 5 because questions without a specified city can be ambiguous, so one answer may not clearly identify the city.


---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
