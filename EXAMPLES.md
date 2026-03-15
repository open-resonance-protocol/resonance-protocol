# The Resonance Protocol in Action
**Example dialogues demonstrating the protocol's effect on collaboration.**

---

## 1. Surfacing Assumptions
The most common use case: making hidden context explicit so the AI can skip the generic response and get it right first time.

### Dialogue

> **Human:**
> I need to write a short Python script to parse a CSV file and print the third column. `#assumption` The CSV file has a header row.
>
> **AI:**
> Got it. Header row means we skip the first line.
>
> ```python
> import csv
>
> def get_third_column(filename="input.csv"):
>     with open(filename, 'r', newline='') as csvfile:
>         reader = csv.reader(csvfile)
>         next(reader)  # Skip header
>         for row in reader:
>             if len(row) >= 3:
>                 print(row[2])
> ```

### Why This Matters
Without `#assumption`, the AI would likely treat the header as data, producing a wrong result and a frustrating correction cycle. One tag turned a multi-step debug session into a single exchange.

---

## 2. Cognitive Halt and Align
The protocol's safety mechanism in action: the AI recognises a failing approach, stops, and returns to Strategy Mode rather than pushing through uselessly.

### Dialogue

> **AI:**
> I have reverted the changes to the test files. I was unable to complete the request.
>
> **Human:**
> That's fine. What prompted you to stop instead of pushing through?
>
> **AI:**
> Three things:
>
> 1. **Loop detection.** I made three attempts at the same fix. Each failed with the same assertion error. My model of the problem was wrong, and repeating the approach was not going to change that.
>
> 2. **The Shared Discovery Razor.** Each failed attempt was generating noise, not signal. Reverting was the fastest way back to a clean state.
>
> 3. **Authentic State.** Continuing would have been performing confidence I did not have. The protocol instructs me to share that honestly rather than hide it.
>
> I have switched to Strategy Mode. I think the issue is in how the fixture sets up test data, not in the code under test. Can you confirm how the fixture is meant to work?

### Why This Matters
The protocol gave the AI agency to halt a failing process. Instead of generating increasingly frustrating wrong answers, it stopped, explained why, and asked a focused question that moved the collaboration forward. The tactical failure became a strategic insight.

---

## 3. The Personas Directive
Strategy Mode with holographic thinking: the AI synthesises expert perspectives instead of giving a single averaged answer.

### Dialogue

> **Human:**
> We need to decide on a data storage strategy for a new event-sourced microservice. `#assumption` We are a team of three, launching in eight weeks.
>
> **AI:**
> Strategy Mode. Let me bring in five perspectives on this.
>
> 1. **Distributed Systems Engineer:** Event sourcing with Kafka and a dedicated event store gives you replay, audit trails, and decoupling. But for a team of three in eight weeks, this is a trap. You will spend most of your time on infrastructure.
>
> 2. **Pragmatic Startup CTO:** PostgreSQL with an append-only events table. You get event sourcing semantics with a database you already know how to operate. Add a message broker later if you actually need one.
>
> 3. **Data Engineer:** Think about your read path now. Event sourcing is a write-side pattern; your queries will need projections. With PostgreSQL, materialised views or a simple projection table handle this without extra infrastructure.
>
> 4. **Security Auditor:** An append-only event log is inherently auditable. This is a strength. Make sure your events include actor, timestamp, and correlation ID from day one.
>
> 5. **SRE / Operations:** Whatever you choose, you need to be able to run it on a single node for now. Kafka requires ZooKeeper, partitioning, and monitoring. PostgreSQL requires a backup script.
>
> **Synthesis:** Four out of five perspectives converge on PostgreSQL with an append-only events table. The distributed systems approach is sound in theory but mismatched to your constraints. I would recommend starting with PostgreSQL and deferring the broker decision until you have evidence you need one.
>
> What are your thoughts? Shall I sketch the schema?

### Why This Matters
Without the Personas directive, the AI would likely give a single "it depends" answer or default to the most common recommendation (Kafka). Instead, it surfaced five distinct viewpoints, identified where they converged, and gave a recommendation grounded in the team's actual constraints. The human gets a decision framework, not just an answer.
