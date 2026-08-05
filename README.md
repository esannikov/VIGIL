# VIGIL

## An autonomous art machine for reading the world

**Research preview · v6 alpha · code coming soon**

VIGIL reads a day before it makes an image. Each evening it gathers public signals about conflict, climate, health, infrastructure, technology, markets and human attention. It chooses one tension, develops five visual positions, generates five images, examines the pixels and selects one work before receiving human feedback.

The project asks a practical question: **can a machine develop an artistic method when its sources, alternatives, failures and revisions remain visible?**

VIGIL is a living experiment within Eugene Sannikov's PhD research on AI in Art at the National Academy of Fine Arts and Architecture in Kyiv.

<p align="center">
  <img src="assets/works/the-crossing-leads-back.png" width="620" alt="The Crossing Leads Back. A stair rises over a fortified border and returns to the side where it began.">
  <br>
  <sub><strong>Figure 1.</strong> <em>The Crossing Leads Back</em> (2026). GPT Image 2 generation selected by VIGIL before human review.</sub>
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

<p align="center"><sub><strong>Figure 2.</strong> Current VIGIL v6 alpha architecture. Blue marks the autonomous cycle, gray marks trace and advisory memory, and green marks human authority.</sub></p>

The map uses the [Carbon Design System](https://carbondesignsystem.com/) as a visual framework: Gray 100 layers, IBM Plex hierarchy, spacing tokens and directly labelled flows. Blue marks the autonomous nightly path; gray carries provenance and memory; green marks decisions reserved for human review.

### Current modules

The table documents the working prototype while implementation remains private. Agent names describe decision roles; script names identify the runtime surfaces planned for the later code release.

| Stage | Agent or runtime surface | Responsibility | Recorded result |
|---|---|---|---|
| Evidence collection | `vigil_sensors.py` | Queries the source registry, normalizes records, records failures and reports coverage gaps | Dated evidence packet with source IDs and claim permissions |
| World interpretation | **World Reader** through `vigil_reasoning.py` | Reads the current packet independently, selects one tension and states its factual boundary or refusal | World read with counter-reading and cited signal IDs |
| Associative recall | **Hindsight Recall** through `vigil_reasoning.py` | Retrieves reviewed traces, failures and theory only after the current event has been framed | Advisory recall; no factual or procedural authority |
| Artistic reasoning | **Artistic Reasoner** through `vigil_reasoning.py` | Chooses a theoretical mode and develops five distinct positions with explicit message designs | Five concepts with subject, action, consequence and uncertainty |
| Pre-render review | **Studio / Concept Critic** through `vigil_reasoning.py` | Compares concepts pairwise and checks whether the visible mechanism can survive without explanatory prose | Comparative review and a narrow clarity gate |
| Visual translation | **Creative Sight** and **Prompt Director** through `vigil_creative_engine.py` | Converts each position into a scene, composition, material action and generation instruction | Five production scenes and prompts |
| Image production | **Image gateway** | Generates all five works through GPT Image 2 under the recorded model policy | Five bound image artifacts |
| Pixel review | **Visual Critic** through `visual_critic.py` | Performs a blind reading, then an informed reading, and compares the set | Artifact reviews and machine ranking |
| Trace integrity | `trace_contract.py` and `vigil_creative_engine.py` | Binds sources, alternatives, prompts, files, hashes, critiques and human verdicts | Append-only generation trace |
| Method learning | `trace_compiler.py`, event log and Hindsight | Detects repetition, records candidate discoveries and recalls only reviewed history | Candidate lesson, correction or human-approved method transfer |
| Slow reflection | **Dream Reasoner** through `vigil_reasoning.py` | Searches recent traces for unresolved relations and future experiments | Candidate-only dream; active rules remain unchanged |

## Why build it?

Creative work is usually judged after the result exists. The decisive moment remains hidden: why one possibility survived, why another disappeared and what could change the maker's method.

VIGIL turns that hidden interval into research material. Every public claim has a source boundary. Every cycle retains rejected positions. The visual critic first reads the image without access to the prompt. The machine's final choice is fixed before the human response. A lesson enters active memory only after it survives another context and receives human approval.

This makes the project useful for studying creativity without reducing it to a single score. The object of study is the path between evidence, association, form, judgment and revision.

## What is actually formalized

VIGIL uses two kinds of formalization. **Runtime computations** are arithmetic operations executed by Python. The **formal decision model** describes the variables available to an agent and the structure of its judgment without pretending that interpretation is a numerical optimizer. VIGIL does not calculate artistic value or derive the winning image from a weighted score.

### Runtime computations: coverage and balance

For each run, the system returns the number of registered sensors and the number the current runtime can query. Their reported ratio is:

$$
C_{run}=\frac{N_{queryable}}{N_{registered}}
$$

The 5 August 2026 snapshot gives $C_{run}=13/20=0.65$. Python produces both counts; the ratio is derived in the report. It describes technical availability and says nothing about the truth, independence or moral importance of the returned records. The following cap is executed directly. To prevent a prolific source from dominating by volume, the reasoning view retains at most eight records from any one sensor:

$$
n'_s=\min(n_s,8)
$$

### Formal decision model: World Reader

For every signal it retains, the World Reader records six bounded judgments:

$$
x_i=(e_i,\Delta_i,c_i,r_i,d_i,a_i),
\qquad 0\leq x_{i,m}\leq4
$$

They describe evidence strength, change, consequence, systemic reach, duration and an attention gap. This is a mathematical model of the agent's input and judgment surface. The agent assigns the coordinates under a validated schema; Python checks their range and provenance but does not calculate them or add them into a hidden importance score. The World Reader must still state why a signal matters now, where the claim ends and what counter-reading remains possible.

### Formal decision model: criticism and selection

After generation, the Visual Critic records a fourteen-coordinate diagnostic description for each artifact:

$$
q_j\in[0,10]^{14}
$$

The coordinates include first reading, composition, formal necessity, ambiguity, source relation, ethical attention, affect and originality. They are model judgments constrained to the interval by schema, not measurements calculated from pixels. `overall` is a separate holistic judgment, not their mean. VIGIL then compares the five actual images and commits to one through an agent judgment:

$$
\hat{j}=A\big((I_j,q_j,b_j,k_j)_{j=1}^{5}\big)
$$

Here $I_j$ is the image, $b_j$ its blind reading, $k_j$ its source-and-concept context, and $A$ denotes the recorded agent decision. The expression is a formal model of the decision path. It names the evidence available to the agent and does not claim a closed numerical solution.

### Runtime computation: learning gate

A candidate belief can be revised only when one exact artifact has a pixel-aware review, an accepted human verdict, an artifact-scoped learning proposal and a critic score at or above the current threshold of 7:

$$
P(a)=1\Longleftrightarrow R_a\land H_a\land D_a\land(s_a\geq7)
$$

$R_a$ denotes an attached pixel-aware review, $H_a$ an accepted artifact-bound human verdict and $D_a$ an artifact-scoped learning proposal.

When the gate passes, confidence is damped toward the new evidence with $\alpha=0.25$:

$$
b_{t+1}=\min\left(1,\max\left(0,(1-\alpha)b_t+\alpha e_t\right)\right),
\qquad e_t=s_a/10
$$

This formula is implemented in the runtime and the result is rounded to three decimal places. The update changes confidence in a named working hypothesis. It does not prove that an image is good, that a method generalizes or that the machine has learned creativity. A belief remains a hypothesis until it has support from three distinct trace sources; durable procedural rules remain subject to human review and transfer testing.

The current use of exactly five candidates and the pre-render clarity gate belongs to the v6 alpha study design. Five gives a comparable choice set; the clarity gate tests whether a proposed central relation survives without explanatory prose. Neither is presented as a universal theory of art.

The same gate creates a known methodological pressure. The current concept schema asks every candidate to expose a subject, an action, a consequence and a target-source metaphor. This improved message recovery after earlier images became opaque, but it also favors causal visual riddles over indexical, durational, atmospheric, serial or nonrepresentational work. The 30-evening protocol keeps the constraint stable for comparison and renders selected rejected concepts on control days. A proposed later studio mode would let VIGIL choose the work's logic while code continues to protect evidence, identity and trace integrity.

The active runtime contains no lexical or Jaccard novelty score. Repetition is retained as trace evidence and may be discussed by the agent or reported as an attractor; it cannot reject a concept through word overlap.

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
      <sub><strong>Figure 3.</strong> <em>A Comma Over Iran</em> (2026). A military trajectory becomes punctuation: force is paused inside the sentence rather than resolved.</sub>
    </td>
    <td width="50%" valign="top">
      <img src="assets/works/the-scroll-was-built-to-hold.png" alt="The Scroll Was Built to Hold"><br>
      <sub><strong>Figure 4.</strong> <em>The Scroll Was Built to Hold</em> (2026). Selected calibration work. The interface gesture continues outside the screen and restrains the hand performing it.</sub>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <img src="assets/works/the-chokepoint-deal.png" alt="The Chokepoint Deal"><br>
      <sub><strong>Figure 5.</strong> <em>The Chokepoint Deal</em> (2026). Historical calibration work with partial provenance. A negotiation table acquires the geography of the pressure passing through it.</sub>
    </td>
    <td width="50%" valign="top">
      <img src="assets/works/the-war-runs-on-oil.jpg" alt="The War Runs on Oil"><br>
      <sub><strong>Figure 6.</strong> <em>The War Runs on Oil</em> (2026). Historical calibration work with partial provenance. An oil conduit contains the military and industrial movement it sustains.</sub>
    </td>
  </tr>
</table>

## What informs VIGIL

VIGIL has not been fine-tuned on a private art dataset. Its artistic support is a versioned retrieval corpus: selected theory, art-historical precedents, reviewed traces and procedural rules are introduced when they can change a decision. One primary lens guides a cycle; a second may add one operation. This prevents theory from becoming decorative name-dropping.

| Corpus lens | Principal references | Effect on the Artistic Reasoner | Test used by the Critic |
|---|---|---|---|
| Visual metaphor and signs | Max Black; Charles Forceville; C. S. Peirce; Roland Barthes | Names the target, source and single property transferred between them | Both terms remain available in the pixels; a caption may anchor meaning but cannot manufacture the central relation |
| Visual forces | Rudolf Arnheim | Uses scale, direction, balance, weight and negative space as parts of the argument | First, second and third visual fixation support the intended subject, action and consequence |
| Defamiliarization and compression | Viktor Shklovsky; Bertolt Brecht; Guy Debord and Gil J. Wolman | Alters the function or scale of a familiar thing so a normalized mechanism can be seen again | One readable contradiction dominates; unrelated symbols and explanatory clutter count against the work |
| Evidence and institutions | Hans Haacke; Forensic Architecture; Taryn Simon | Exposes a material chain, institutional space, classification or omission | Every public claim stays within its source boundary; interpretation cannot pose as an indexical trace |
| Procedure, systems and constrained chance | Sol LeWitt; Yoko Ono; John Cage; Jack Burnham; Oulipo | Treats an artwork as an auditable instruction while allowing bounded variation | The procedure must produce a public proposition; chance cannot select the fact or its moral importance |
| Memory, duration and archive | On Kawara; Tehching Hsieh; Christian Boltanski; Hal Foster | Works through date, repetition, accumulation, absence and historical difference | Analogy must preserve historical differences; archival display is not used as an automatic visual solution |
| Computational creativity | Margaret Boden; Geraint Wiggins; Anna Jordanous | Treats creativity as generation within, exploration of and transformation of a possibility space | Alternatives remain visible; novelty, value, clarity and formal diversity are assessed separately |
| Reflective practice and agent memory | Donald Schön; [Hindsight](https://github.com/vectorize-io/hindsight) | Brings reviewed failures and prior decisions back into a new but already framed situation | Recall remains advisory, preserves provenance and cannot promote a method without reviewed transfer |

The Critic receives the same corpus with a different role. It checks whether the chosen operation is visible, whether composition carries the relation, whether the image exceeds the evidence and whether VIGIL is repeating a recent solution. It does not choose the political importance of the event or define artistic value with one score.

### Memory corpus

| Layer | Contents | Authority |
|---|---|---|
| Current evidence | Dated sensor records, source health, caveats and counter-readings | May support only the claims permitted by each source |
| Theory corpus | Versioned notes and source references behind the lenses above | Suggests an operation and a failure condition |
| Trace archive | Concepts, prompts, images, hashes, blind readings, machine choices and human verdicts | Preserves what happened in a particular cycle |
| Method bank | Candidate failures, discoveries, corrections and transferred procedures | Only reviewed and promoted methods may guide later runs automatically |
| Hindsight bank | Associative synthesis across reviewed traces, entities, time and theory | Recall and reflection only; it cannot establish facts or rewrite the audit trail |

## World inputs

The registry snapshot for 5 August 2026 contains 20 open or institutionally accessible sensors; 13 are queryable in the present runtime. VIGIL keeps event occurrence, public attention and slow background conditions separate.

| Sensor | Observed signal | Epistemic use | Access snapshot |
|---|---|---|---|
| [USGS Earthquake Catalog](https://earthquake.usgs.gov/fdsnws/event/1/) | Earthquake time, place and magnitude | Direct physical event; human impact requires corroboration | Connected |
| [GDACS](https://www.gdacs.org/) | Multi-hazard alerts and modelled impact | Event and humanitarian context with model caveats | Intermittent |
| [WHO Disease Outbreak News](https://www.who.int/emergencies/disease-outbreak-news) | Dated outbreak assessments and response | Direct claims within the report's scope | Connected |
| [NASA EONET](https://eonet.gsfc.nasa.gov/docs/v3) | Curated storms, fires, volcanoes and ice events | Event location and originating-source discovery | Connected |
| [IODA](https://ioda.inetintel.cc.gatech.edu/) | Regional internet-outage alerts | Network disruption; cause remains open | Connected |
| [NOAA Space Weather](https://www.swpc.noaa.gov/) | Solar and geomagnetic alerts | Direct planetary condition | Connected |
| [CISA Known Exploited Vulnerabilities](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) | Vulnerabilities observed in active exploitation | Cybersecurity and infrastructure pressure | Connected |
| [Federal Register](https://www.federalregister.gov/developers/documentation/api/v1) | US federal rules, notices and actions | Institutional change within one jurisdiction | Connected |
| [Wikimedia Pageviews](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews) | Changes in article readership | Attention proxy, never proof of importance | Connected |
| [Google News RSS](https://news.google.com/rss/) | Cross-publisher headline discovery | Discovery only; claims return to the publisher | Limited |
| [GDELT](https://www.gdeltproject.org/) | News volume, themes and tone | Media-attention proxy and corroboration | Degraded |
| [NOAA Mauna Loa CO₂](https://gml.noaa.gov/ccgg/trends/) | Weekly atmospheric CO₂ | Slow planetary substrate | Connected |
| [UNHCR Refugee Data Finder](https://www.unhcr.org/refugee-statistics/) | Displacement stocks and flows | Long-duration human context with reporting lag | Connected |
| [OpenAlex](https://docs.openalex.org/) | Scholarly works and publication change | Knowledge-production and research-attention context | Limited |
| [World Bank Open Data](https://datahelpdesk.worldbank.org/knowledgebase/articles/889392) | Development and economic indicators | Slow structural baseline | Degraded |
| [NASA FIRMS](https://firms.modaps.eosdis.nasa.gov/) | Satellite active-fire observations | Physical occurrence and spread; interpretation needs context | Setup required |
| [ReliefWeb](https://apidoc.reliefweb.int/) | Humanitarian situation reports | Civilian consequence and response context | Registration required |
| [Cloudflare Radar](https://developers.cloudflare.com/radar/) | Internet outages and traffic anomalies | Regional digital disruption with coverage limits | Setup required |
| [US Energy Information Administration](https://www.eia.gov/opendata/) | Energy production, supply, prices and flows | Political-economy baseline and anomaly context | Setup required |
| [ACLED](https://acleddata.com/) | Curated political violence and protest events | Conflict evidence under ACLED methodology and terms | Setup required |

An instrumental record may support a bounded event claim. An attention signal shows where a platform audience looked. A slow indicator supplies context. The extended notes and access caveats remain available in [Sources](SOURCES.md).

## Research status

VIGIL is an operational alpha prototype. The complete cycle works: sensing, artistic reasoning, image generation, pixel-aware criticism, machine selection, human review and trace-bound memory. The present research phase tests whether memory improves later decisions while preserving formal variety.

A planned 30-evening study compares runs with and without reviewed memory on matched evidence packets. The primary measure is whether independent readers can recover the intended subject, action and consequence from the image. Formal diversity, dependence on captions, selection regret and machine-human disagreement remain separate outcomes.

Two planned outcome measures are intentionally simple. Message recovery is the share of works for which an independent reader identifies the intended subject, action and consequence. Selection agreement is the share of cycles in which the machine and human choose the same work. These measures have not yet produced study results; the repository reports no effect size or claim of improvement.

## Code coming soon

This repository currently publishes the concept, architecture, selected works, source map and research framing. It does **not** contain the VIGIL runtime, model adapters, credentials, internal prompts or private research traces.

A sanitized and reproducible code release is planned after the 30-evening protocol stabilizes the interfaces and removes private paths and service-specific configuration.

## Author

**Eugene Sannikov**  
PhD researcher in AI and Art, National Academy of Fine Arts and Architecture, Kyiv  
[ORCID 0009-0008-9917-8461](https://orcid.org/0009-0008-9917-8461)

The research text and curated visual works are published under the terms in [Rights](RIGHTS.md). Citation metadata is available in [`CITATION.cff`](CITATION.cff).

## References

Reports supporting individual works, together with their claim boundaries and trace status, are listed in [Provenance](PROVENANCE.md).

### Art, theory and computational creativity

Arnheim, R. (1974). *Art and visual perception: A psychology of the creative eye* (Rev. ed.). University of California Press.

Atkin, A. (2022). Peirce's theory of signs. In E. N. Zalta (Ed.), *The Stanford encyclopedia of philosophy*. Stanford University. https://plato.stanford.edu/entries/peirce-semiotics/

Barthes, R. (1977). Rhetoric of the image. In *Image, music, text* (S. Heath, Trans., pp. 32–51). Hill and Wang.

Black, M. (1977). More about metaphor. *Dialectica, 31*(3–4), 431–458. https://doi.org/10.1111/j.1746-8361.1977.tb01296.x

Boden, M. A. (2004). *The creative mind: Myths and mechanisms* (2nd ed.). Routledge.

Brecht, B. (1964). *Brecht on theatre: The development of an aesthetic* (J. Willett, Ed. & Trans.). Hill and Wang.

Burnham, J. (1968). Systems esthetics. *Artforum, 7*(1), 30–35.

Cage, J. (1961). *Silence: Lectures and writings*. Wesleyan University Press.

Debord, G., & Wolman, G. J. (1956). Mode d'emploi du détournement. *Les Lèvres Nues, 8*.

Forceville, C. (2008). Metaphor in pictures and multimodal representations. In R. W. Gibbs Jr. (Ed.), *The Cambridge handbook of metaphor and thought* (pp. 462–482). Cambridge University Press. https://doi.org/10.1017/CBO9780511816802.028

Forensic Architecture. (n.d.). *Ground truth*. Retrieved August 5, 2026, from https://forensic-architecture.org/methodology/ground-truth

Foster, H. (2004). An archival impulse. *October, 110*, 3–22. https://doi.org/10.1162/0162287042379847

Haacke, H. (1975). *Framing and being framed: 7 works, 1970–75*. Press of the Nova Scotia College of Art and Design.

Heathfield, A., & Hsieh, T. (2009). *Out of now: The lifeworks of Tehching Hsieh*. MIT Press.

Jordanous, A. (2012). A standardised procedure for evaluating creative systems: Computational creativity evaluation based on what it is to be creative. *Cognitive Computation, 4*(3), 246–279. https://doi.org/10.1007/s12559-012-9156-1

LeWitt, S. (1967). Paragraphs on conceptual art. *Artforum, 5*(10), 79–83.

Motte, W. F. (Ed. & Trans.). (1986). *Oulipo: A primer of potential literature*. University of Nebraska Press.

Ono, Y. (1964). *Grapefruit*. Wunternaum Press.

Schön, D. A. (1983). *The reflective practitioner: How professionals think in action*. Basic Books.

Semin, D., Garb, T., & Kuspit, D. (1997). *Christian Boltanski*. Phaidon.

Shklovsky, V. (1965). Art as technique. In L. T. Lemon & M. J. Reis (Eds. & Trans.), *Russian formalist criticism: Four essays* (pp. 3–24). University of Nebraska Press. (Original work published 1917)

Simon, T. (2007). *An American index of the hidden and unfamiliar*. Steidl.

Weiss, J., & Wheeler, A. (Eds.). (2015). *On Kawara—Silence*. Guggenheim Museum Publications.

Wiggins, G. A. (2006). A preliminary framework for description, analysis and comparison of creative systems. *Knowledge-Based Systems, 19*(7), 449–458. https://doi.org/10.1016/j.knosys.2006.04.009

### System and memory infrastructure

IBM. (n.d.). *Carbon Design System*. Retrieved August 5, 2026, from https://carbondesignsystem.com/

Sannikov, E. (2026). *VIGIL: An autonomous art machine for reading the world* (Version 6 alpha) [Research software]. GitHub. https://github.com/esannikov/VIGIL

Vectorize. (n.d.). *Hindsight: Agent memory that learns* [Computer software]. GitHub. Retrieved August 5, 2026, from https://github.com/vectorize-io/hindsight

### Sensor and public-data sources

Armed Conflict Location & Event Data. (n.d.). *ACLED*. Retrieved August 5, 2026, from https://acleddata.com/

Cybersecurity and Infrastructure Security Agency. (n.d.). *Known Exploited Vulnerabilities Catalog*. Retrieved August 5, 2026, from https://www.cisa.gov/known-exploited-vulnerabilities-catalog

Cloudflare. (n.d.). *Cloudflare Radar API documentation*. Retrieved August 5, 2026, from https://developers.cloudflare.com/radar/

Federal Register. (n.d.). *API documentation*. Retrieved August 5, 2026, from https://www.federalregister.gov/developers/documentation/api/v1

Georgia Tech Internet Intelligence Lab. (n.d.). *Internet Outage Detection and Analysis*. Retrieved August 5, 2026, from https://ioda.inetintel.cc.gatech.edu/

Global Disaster Alert and Coordination System. (n.d.). *GDACS*. Retrieved August 5, 2026, from https://www.gdacs.org/

Google. (n.d.). *Google News*. Retrieved August 5, 2026, from https://news.google.com/

National Aeronautics and Space Administration. (n.d.-a). *Earth Observatory Natural Event Tracker API*. Retrieved August 5, 2026, from https://eonet.gsfc.nasa.gov/docs/v3

National Aeronautics and Space Administration. (n.d.-b). *Fire Information for Resource Management System*. Retrieved August 5, 2026, from https://firms.modaps.eosdis.nasa.gov/

National Oceanic and Atmospheric Administration. (n.d.-a). *Global Monitoring Laboratory: Trends in atmospheric carbon dioxide*. Retrieved August 5, 2026, from https://gml.noaa.gov/ccgg/trends/

National Oceanic and Atmospheric Administration. (n.d.-b). *Space Weather Prediction Center*. Retrieved August 5, 2026, from https://www.swpc.noaa.gov/

OpenAlex. (n.d.). *OpenAlex technical documentation*. Retrieved August 5, 2026, from https://docs.openalex.org/

ReliefWeb. (n.d.). *ReliefWeb API documentation*. Retrieved August 5, 2026, from https://apidoc.reliefweb.int/

The GDELT Project. (n.d.). *The GDELT Project*. Retrieved August 5, 2026, from https://www.gdeltproject.org/

United Nations High Commissioner for Refugees. (n.d.). *Refugee Data Finder*. Retrieved August 5, 2026, from https://www.unhcr.org/refugee-statistics/

U.S. Energy Information Administration. (n.d.). *Open data*. Retrieved August 5, 2026, from https://www.eia.gov/opendata/

U.S. Geological Survey. (n.d.). *Earthquake Catalog API*. Retrieved August 5, 2026, from https://earthquake.usgs.gov/fdsnws/event/1/

Wikimedia Foundation. (n.d.). *Wikimedia Analytics API: Pageviews*. Retrieved August 5, 2026, from https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews

World Bank. (n.d.). *World Bank Open Data*. Retrieved August 5, 2026, from https://data.worldbank.org/

World Health Organization. (n.d.). *Disease Outbreak News*. Retrieved August 5, 2026, from https://www.who.int/emergencies/disease-outbreak-news

### Selected-work source reports

Huamani, K., & Ortutay, B. (2026, March 25). *Jury finds Instagram and YouTube liable in a landmark social media addiction trial*. AP News. https://apnews.com/article/social-media-addiction-trial-la-5e54075023d837ccdc76c4ca512e925d

Madhani, A., & Magdy, S. (2026, August 2). *Trump says Gulf leaders' input weighed heavily in decision to hold off on ordering new Iran strikes*. AP News. https://apnews.com/article/f4c225f6667d9fd171616304701825a0

Naishadham, S. (2026, August 2). *Ceuta grapples with aftermath of border surge after most migrants leave the Spanish territory*. AP News. https://apnews.com/article/9960b15a7cf31a0592b09ac47a8eac3f

Ruíz, S. R., Naishadham, S., & Oubachir, A. (2026, August 1). *Spain installs sea barrier on Ceuta's border with Morocco after frontier rush that killed 67*. AP News. https://apnews.com/article/d76c6dc9d2da828907a1c04e1d482bbe
