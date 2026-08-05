# VIGIL

## An autonomous art machine for reading the world

**Research preview · v6 alpha · code coming soon**

VIGIL reads a day before it makes an image. Each evening it gathers public signals about conflict, climate, health, infrastructure, technology, markets and human attention. It chooses one tension, develops five visual positions, generates five images, examines the pixels and selects one work before receiving human feedback.

The project asks a practical question: **can a machine develop an artistic method when its sources, alternatives, failures and revisions remain visible?**

VIGIL is a living experiment within Eugene Sannikov's PhD research on AI in Art at the National Academy of Fine Arts and Architecture in Kyiv.

<p align="center">
  <img src="assets/works/the-crossing-leads-back.png" width="620" alt="The Crossing Leads Back. A stair rises over a fortified border and returns to the side where it began.">
</p>

### The project in one cycle

1. **Sense.** Collect dated public records and attention signals.
2. **Choose.** Form one bounded statement about the day's tension.
3. **Position.** Develop five materially different artistic responses.
4. **Generate.** Create five images autonomously through an API gateway to GPT Image 2.
5. **Critique.** Read the finished pixels before reopening the intended meaning.
6. **Select.** Rank the set and choose one work before the human verdict is known.
7. **Learn.** Preserve disagreement, failure and accepted corrections in an append-only memory.

Human authority remains explicit. The researcher controls publication and the promotion of a local discovery into a durable method. Autonomy describes the bounded interval in which VIGIL moves from evidence to its own selection.

## System map

![VIGIL system map](assets/system-map.svg)

The map uses the [Carbon Design System](https://carbondesignsystem.com/) as a visual framework: Gray 100 layers, IBM Plex hierarchy, spacing tokens and directly labelled flows. Blue marks the autonomous nightly path; gray carries provenance and memory; green marks decisions reserved for human review.

## Why build it?

Creative work is usually judged after the result exists. The decisive moment remains hidden: why one possibility survived, why another disappeared and what could change the maker's method.

VIGIL turns that hidden interval into research material. Every public claim has a source boundary. Every cycle retains rejected positions. The visual critic first reads the image without access to the prompt. The machine's final choice is fixed before the human response. A lesson enters active memory only after it survives another context and receives human approval.

This makes the project useful for studying creativity without reducing it to a single score. The object of study is the path between evidence, association, form, judgment and revision.

## A decision trace: *The Crossing Leads Back*

The source packet concerned a mass crossing into Ceuta followed by the return of most migrants to Morocco. VIGIL narrowed the report to one defensible proposition: a border can appear passable while the conditions beyond it still force movement backward.

The first image used a gate and a conveyor. It failed because the device had no recognizable purpose. Human criticism identified that failure. VIGIL then searched for a familiar crossing structure and produced one continuous stair that climbs above the fence, turns in a hairpin and descends to its point of origin.

During blind review, the critic recovered the message as “an attempted crossing ends in return rather than passage.” VIGIL ranked the work first among five images before seeing the human verdict. Its nearest alternative communicated the news more literally; the stair was chosen because the entire form became necessary to the claim. The subsequent human verdict was strong, and the method entered memory as a verified transfer: **a familiar object performs one impossible but readable action.**

The source, initial failure, image request, generated artifact, blind review, machine ranking and human verdict remain connected in one trace. See [Provenance](PROVENANCE.md).

## Selected works

<table>
  <tr>
    <td width="50%" valign="top">
      <img src="assets/works/a-comma-over-iran.png" alt="A Comma Over Iran"><br>
      <strong>A Comma Over Iran</strong><br>
      A military trajectory becomes punctuation: force is paused inside the sentence rather than resolved.
    </td>
    <td width="50%" valign="top">
      <img src="assets/works/the-scroll-was-built-to-hold.png" alt="The Scroll Was Built to Hold"><br>
      <strong>The Scroll Was Built to Hold</strong><br>
      The interface gesture continues outside the screen and restrains the hand performing it.
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <img src="assets/works/the-chokepoint-deal.png" alt="The Chokepoint Deal"><br>
      <strong>The Chokepoint Deal</strong><br>
      A negotiation table acquires the geography of the pressure passing through it.
    </td>
    <td width="50%" valign="top">
      <img src="assets/works/the-war-runs-on-oil.jpg" alt="The War Runs on Oil"><br>
      <strong>The War Runs on Oil</strong><br>
      An oil conduit contains the military and industrial movement it sustains.
    </td>
  </tr>
</table>

## What informs VIGIL

The permanent context combines four kinds of knowledge:

- **Art as procedure and system:** Sol LeWitt, Jack Burnham, Hans Haacke, Yoko Ono, John Cage and On Kawara.
- **Evidence and public truth:** documentary practice, institutional critique and Forensic Architecture.
- **Visual metaphor and rhetoric:** Max Black, Charles Forceville, Charles S. Peirce, Roland Barthes and Rudolf Arnheim.
- **Computational creativity and reflective practice:** Margaret Boden, Geraint Wiggins, Anna Jordanous and Donald Schön.

Theory proposes operations and risks. It does not choose the work. VIGIL may use a familiar object, alter its function, stage a contradiction, expose an infrastructure or refuse an image when the evidence or ethical position is too weak.

Associative memory is provided by [Hindsight](https://github.com/vectorize-io/hindsight). It recalls related failures, motifs and theoretical fragments after the current event has been selected. It cannot establish a new fact, overwrite the trace or activate a method by itself.

## World inputs

The registry snapshot for 5 August 2026 contains 20 open or institutionally accessible sensors. Thirteen are queryable in the present runtime. They include USGS earthquakes, WHO outbreak reports, NASA natural events, NOAA space-weather and CO₂ records, internet-outage alerts, displacement statistics, public regulation, knowledge change and attention signals.

Each source carries a permission boundary. An instrumental record may support a precise event claim; an attention signal can show what a platform audience is looking at; an associative memory can only suggest a connection. The full public-facing list is in [Sources](SOURCES.md).

## Research status

VIGIL is an operational alpha prototype. The complete cycle works: sensing, artistic reasoning, image generation, pixel-aware criticism, machine selection, human review and trace-bound memory. The present research phase tests whether memory improves later decisions while preserving formal variety.

A planned 30-evening study compares runs with and without reviewed memory on matched evidence packets. The primary measure is whether independent readers can recover the intended subject, action and consequence from the image. Formal diversity, dependence on captions, selection regret and machine-human disagreement remain separate outcomes.

## Code coming soon

This repository currently publishes the concept, architecture, selected works, source map and research framing. It does **not** contain the VIGIL runtime, model adapters, credentials, internal prompts or private research traces.

A sanitized and reproducible code release is planned after the 30-evening protocol stabilizes the interfaces and removes private paths and service-specific configuration.

## Author

**Eugene Sannikov**  
PhD researcher in AI and Art, National Academy of Fine Arts and Architecture, Kyiv  
[ORCID 0009-0008-9917-8461](https://orcid.org/0009-0008-9917-8461)

The research text and curated visual works are published under the terms in [Rights](RIGHTS.md). Citation metadata is available in [`CITATION.cff`](CITATION.cff).
