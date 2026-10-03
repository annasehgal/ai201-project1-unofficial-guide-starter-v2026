# Run log — after_titled

- Produced by: `run_eval.py::main`
- Retrieval: `store.py::search`, chunks from `chunker.py::split_documents`
- Corpus: `city_guides` (index variant `titled`)
- top-k: 5 · relevance cutoff: 0.6
- Runs per question: 3, caching off
- When: 2026-10-02 21:19

This table is one row per QUESTION. The run log your README asks for is
one row per CRITERION, so aggregate these into it — criterion 1 is how many
of your questions had the answer in the retrieved chunks, and so on.

| Question | Run 1 | Run 2 | Run 3 |
|---|---|---|---|
| Where can visitors  eat in Corry Vale? | pass | pass | pass |
| Is September a good month to visit Brightwater? | pass | pass | pass |
| How long does the coastal path from Halden Bay to the lighthouse take? | pass | pass | pass |
| How accessible is Kestrelford for walking? | fail | fail | fail |
| How is the mobile coverage in Halden Bay? | pass | pass | pass |

---

## The relevance gate on out-of-corpus questions

Produced by `run_eval.py::check_out_of_scope`, cutoff 0.6. Refused 5 of 5.

Retrieval is deterministic and the gate is a comparison against a
fixed number, so these do not vary between runs — one pass over the
list is the whole measurement.

| Out-of-scope question | Best distance | Gate |
|---|---|---|
| What is the capital of Mongolia? | 0.803 | refused |
| How do I change the oil in a diesel engine? | 0.882 | refused |
| Who won the 1994 World Cup? | 0.975 | refused |
| What is the recommended dosage of ibuprofen for a headache? | 0.818 | refused |
| How do I write a for loop in Rust? | 0.814 | refused |

---

## Real output

This is what the system actually produced. Paste the relevant parts
into your README underneath the table — the rubric asks for real
output as text, not a description of it.

### Where can visitors  eat in Corry Vale? — run 1

- Best distance: 0.2406 (passed the gate)
- Sources retrieved: guide_corry_vale.md, guide_eating.md

```
Visitors in Corry Vale can eat at the two pubs (one in the largest village serving food seven days a week, and a second in the third village opening Thursday to Sunday) or buy limited supplies like bread and cheese at the farm shop located at the valley mouth. 

Source: `guide_corry_vale.md`
```

### Where can visitors  eat in Corry Vale? — run 2

- Best distance: 0.2406 (passed the gate)
- Sources retrieved: guide_corry_vale.md, guide_eating.md

```
Visitors in Corry Vale can eat at the two pubs (one in the largest village serving food seven days a week, and a second in the third village that opens Thursday to Sunday) and purchase bread and cheese from the farm shop at the valley mouth. 

Source: `guide_corry_vale.md`
```

### Where can visitors  eat in Corry Vale? — run 3

- Best distance: 0.2406 (passed the gate)
- Sources retrieved: guide_corry_vale.md, guide_eating.md

```
Visitors in Corry Vale can eat at the valley's two pubs (one in the largest village serving food seven days a week, and a second in the third village opening Thursday to Sunday) or purchase bread and cheese from the farm shop at the valley mouth. 

Source: `guide_corry_vale.md`
```

### Is September a good month to visit Brightwater? — run 1

- Best distance: 0.2255 (passed the gate)
- Sources retrieved: guide_brightwater.md, guide_seasons.md

```
September is considered a sweet spot because it is warm and quiet, and everything is still open. However, from late September the town becomes at its busiest as the term starts, making accommodation hard to find and expensive. 

Source: `guide_seasons.md`
```

### Is September a good month to visit Brightwater? — run 2

- Best distance: 0.2255 (passed the gate)
- Sources retrieved: guide_brightwater.md, guide_seasons.md

```
September is described as a "sweet spot" that is warm and quiet with everything still open, though it is also noted as a time when accommodation in Brightwater becomes hard to find and expensive as term starts. 

Source: `guide_seasons.md`
```

### Is September a good month to visit Brightwater? — run 3

- Best distance: 0.2255 (passed the gate)
- Sources retrieved: guide_brightwater.md, guide_seasons.md

```
September is considered a sweet spot because it is warm and quiet, and everything is still open. However, from late September the town is at its busiest as term starts, making accommodation hard to find and expensive. 

Source: `guide_seasons.md`
```

### How long does the coastal path from Halden Bay to the lighthouse take? — run 1

- Best distance: 0.1785 (passed the gate)
- Sources retrieved: guide_halden_bay.md, guide_regional_transport.md, guide_walking.md

```
The coastal path from Halden Bay to the lighthouse takes about two hours.

Source: `guide_halden_bay.md`
```

### How long does the coastal path from Halden Bay to the lighthouse take? — run 2

- Best distance: 0.1785 (passed the gate)
- Sources retrieved: guide_halden_bay.md, guide_regional_transport.md, guide_walking.md

```
The coastal path from Halden Bay to the lighthouse takes about two hours. 

Source: `guide_walking.md`
```

### How long does the coastal path from Halden Bay to the lighthouse take? — run 3

- Best distance: 0.1785 (passed the gate)
- Sources retrieved: guide_halden_bay.md, guide_regional_transport.md, guide_walking.md

```
The coastal path running north from Halden Bay to a lighthouse takes about two hours. 

Source: `guide_walking.md`, `guide_halden_bay.md`
```

### How accessible is Kestrelford for walking? — run 1

- Best distance: 0.3301 (passed the gate)
- Sources retrieved: guide_accessibility.md, guide_kestrelford.md, guide_walking.md

```
Kestrelford is built on a slope, and the walk up from the lower car park is steeper than it looks on a map, though everything in the town is within a ten-minute walk of the market square. There is no transport or local bus service within the town itself, and the walk is considered "difficult" for those with limited mobility. 

Source: `guide_accessibility.md`, `guide_kestrelford.md`
```

### How accessible is Kestrelford for walking? — run 2

- Best distance: 0.3301 (passed the gate)
- Sources retrieved: guide_accessibility.md, guide_kestrelford.md, guide_walking.md

```
Everything in Kestrelford is within a ten-minute walk of the market square. However, the town is built on a slope, and the walk up from the lower car park is steeper than it appears on a map. 

Source: `guide_kestrelford.md`
```

### How accessible is Kestrelford for walking? — run 3

- Best distance: 0.3301 (passed the gate)
- Sources retrieved: guide_accessibility.md, guide_kestrelford.md, guide_walking.md

```
Everything in Kestrelford is within a ten-minute walk of the market square. However, the town is built on a slope, and the walk up from the lower car park is steeper than it appears on a map. 

Source: `guide_kestrelford.md`
```

### How is the mobile coverage in Halden Bay? — run 1

- Best distance: 0.4255 (passed the gate)
- Sources retrieved: guide_accessibility.md, guide_halden_bay.md

```
Mobile coverage in Halden Bay is good in the centre and patchy on the outskirts. 

Source: `guide_halden_bay.md`
```

### How is the mobile coverage in Halden Bay? — run 2

- Best distance: 0.4255 (passed the gate)
- Sources retrieved: guide_accessibility.md, guide_halden_bay.md

```
Mobile coverage is good in the centre of Halden Bay and patchy on the outskirts. 

Source: `guide_halden_bay.md`
```

### How is the mobile coverage in Halden Bay? — run 3

- Best distance: 0.4255 (passed the gate)
- Sources retrieved: guide_accessibility.md, guide_halden_bay.md

```
Mobile coverage in Halden Bay is good in the centre and patchy on the outskirts. 

Source: `guide_halden_bay.md`
```
