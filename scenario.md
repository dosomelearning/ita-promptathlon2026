# Video Scenario Plan

This document defines the basis for three separate AI-generated videos that
will later be combined into one presentation of approximately 10 minutes.

The structure assumes short prompt budgets in free video-generation tools. Each
video section therefore separates:

- the visual scenario for the generator,
- the content basis that must remain factually stable,
- a compact prompt shape that can be adapted to a specific tool.

## Video 1: Project Introduction

### Purpose

Introduce the project, the team workflow, and the constraints under which the
master article was created.

### Target Duration

2 to 3 minutes

### Video Scenario

A lifelike presenter speaks in a clean academic or studio setting with simple
on-screen callouts. The visual flow should show:

- the article title `Edge Computing Architectures`,
- three team members working with three different AI systems,
- the rule set: no manual editing, no copy-paste, no manual correction,
- prompt engineering as the only method of intervention,
- three initial document artifacts converging into one final master article.

The visuals should stay minimal and readable: title cards, document icons,
prompt callouts, arrows showing synthesis, and a final frame with
`master_article.pdf`.

### Content Basis

The narration should explain:

- this is an AI-only technical writing project,
- the team has three members,
- each member used a different AI tool to create one initial article on the
  same title,
- the work was governed by strict rules that prohibited manual content editing,
- prompts were tracked deliberately as part of the project record,
- Claude was used to synthesize the three source documents into the final
  master article,
- the current project phase is the creation of an AI-generated presentation
  about that process.

### Generator Prompt Shape

Create a 2-3 minute academic presentation video with one lifelike presenter.
The presenter explains an AI-only project called "Edge Computing
Architectures." Show clean overlays for: three team members, three AI-generated
source documents, strict no-manual-editing rules, prompt tracking, and the
final combined document master_article.pdf. Style: professional, calm,
university presentation, readable text, no fast cuts, no decorative visuals.

## Video 2: Master Article Presentation

### Purpose

Present the substance of the master article itself, using the article as the
content source rather than the project README.

### Target Duration

4 to 5 minutes

### Video Scenario

A lifelike presenter gives a formal technical presentation with supporting
slides. The slides should use diagrams, short bullet summaries, and simple
architecture visuals rather than dense text. The visual flow should cover:

- what edge computing is and why it exists,
- the end-edge-cloud continuum,
- the three main paradigms: cloudlets, fog computing, and MEC,
- key architectural drivers: latency, bandwidth, privacy, resilience, context,
  and operational scale,
- modern platforms and trends: lightweight Kubernetes, serverless at the edge,
  edge AI, federated learning, zero trust,
- representative application domains,
- the article's central conclusion that edge paradigms have converged into a
  single continuum.

### Content Basis

This section should stay grounded in `artifacts/master_article.pdf`. The
narration should summarize these core points from the article:

- edge computing moves compute and storage closer to data sources because cloud
  alone cannot satisfy all latency, bandwidth, privacy, and regulatory needs,
- the article compares three dominant paradigms: cloudlets, fog computing, and
  Multi-access Edge Computing,
- modern architectures should be understood as an end-edge-cloud continuum
  rather than isolated models,
- current practice is cloud-native and increasingly relies on lightweight
  Kubernetes distributions and edge-capable orchestration,
- edge AI, federated learning, and zero-trust security are major themes in
  modern edge systems,
- application domains include autonomous driving, industrial IoT, smart cities,
  healthcare, and immersive media,
- the article concludes that the hard problem is no longer defining the edge
  but operating it reliably and securely at scale.

The narration should avoid inventing claims that are not present in the master
article. If the video tool supports uploading or referencing source material,
the master article should be treated as the primary content source for this
video.

### Generator Prompt Shape

Create a 4-5 minute university-style technical presentation video with one
lifelike presenter and clear supporting slides. The topic is the content of the
article "Edge Computing Architectures." Explain edge computing, the
end-edge-cloud continuum, cloudlets, fog computing, MEC, key design drivers,
lightweight Kubernetes, serverless at the edge, edge AI, federated learning,
zero trust, and major use cases. Keep the tone academically rigorous but clear.
Use concise diagrams and short readable text. Base the content on the supplied
master article only.

## Video 3: Lessons Learned

### Purpose

Explain what the team learned from using prompt engineering as the sole method
of producing and refining technical article artifacts.

### Target Duration

2 to 3 minutes

### Video Scenario

A lifelike presenter closes the presentation in a reflective but still
technical tone. The visual flow should show:

- selected prompt excerpts as readable on-screen cards,
- a simple workflow timeline from prompting to draft generation to synthesis,
- examples of verification and review steps,
- a closing summary of lessons, limitations, and next steps.

The visuals should emphasize process transparency rather than spectacle.

### Content Basis

The narration should cover:

- prompt engineering was the only allowed intervention mechanism,
- the quality and direction of AI output depended strongly on prompt clarity,
- using multiple AI systems created useful variation and broader coverage,
- comparing outputs helped expose overlaps, different emphases, and mistakes,
- verification remained necessary because AI systems can invent or distort
  sources,
- prompts themselves became meaningful project artifacts,
- one example prompt pattern was to request relevant information and sources for
  the article topic,
- another was to explicitly validate the links and references used in the
  generated article,
- the next project step is transforming the article work into an AI-generated
  video presentation workflow.

If prompt excerpts are shown, keep them short and readable on screen. Use them
as examples of method, not as dense full-screen text blocks.

### Generator Prompt Shape

Create a 2-3 minute reflective academic presentation video with one lifelike
presenter. Focus on lessons learned from an AI-only article creation project.
Show short prompt excerpts on screen, a simple workflow timeline, and concise
takeaways about prompt quality, multi-AI comparison, verification of sources,
and the limits of AI-generated content. Style: professional, clear, credible,
minimalist, readable.

## Production Notes

- Plan the full presentation as three separate generated videos and combine them
  later in editing.
- Keep each generator prompt compact. Put stable facts in the prompt, but keep
  long narration scripts in a separate document if the tool allows it.
- For each video, prefer one presenter, one setting, and limited on-screen text
  so low-cost tools remain stable.
- If a tool supports reference images, use the same presenter reference across
  all three videos to improve continuity.
- If a tool supports uploaded scripts, use this file as the scenario layer and
  prepare a separate short narration script per video.

## Possible Tool Candidates

As of April 23, 2026, the realistic constraint is that free AI video tools are
usually limited by clip duration, credits, watermarks, resolution, or monthly
quota. For that reason, the three-video plan is still sensible, but these tools
should be treated as candidates for prototyping or segmented generation rather
than guaranteed end-to-end free production of the full 10-minute result.

### 1. HeyGen

Best fit if the priority is a lifelike presenter speaking directly to camera.

- Relevant free-plan signal: the official pricing page lists 3 videos per month
  up to 1 minute each on the free plan, with 720p export.
- Strength for this project: strong talking-avatar and presenter workflow.
- Main limitation: the free limit is short, so it is better for proof-of-
  concept segments than for a full 10-minute presentation.

### 2. Pika

Best fit if the priority is short AI-generated visual scenes, transitions, or
supporting inserts rather than a full presenter-led lecture.

- Relevant free-plan signal: the official pricing page lists a free tier with
  80 monthly video credits, access to Pika 2.5 at 480p, and no watermark on
  downloads.
- Strength for this project: useful for short scene generation and visually
  varied inserts between presenter segments.
- Main limitation: it is not the strongest option for a long, consistent,
  presenter-driven academic talk by itself.

### 3. Runway

Best fit if the priority is controlled short visual clips and polished support
footage.

- Relevant free-plan signal: the official pricing page and help center describe
  a free plan with a one-time 125-credit allocation, enough for about 25
  seconds of Gen-4 Turbo generation, with watermarked output.
- Strength for this project: useful for selected visual sequences, title shots,
  or supporting motion graphics.
- Main limitation: the free allowance is too small for primary production of
  all three videos.

### Practical Recommendation

If the goal is to stay fully free, the safest plan is:

- use HeyGen first for presenter-style tests,
- use Pika or Runway only for short supporting visuals,
- expect a prototype-grade result unless an additional free tool or manual video
  assembly step closes the gap.

If later turns permit broader tool research, the next useful step would be to
compare free editing/assembly tools for stitching the generated clips into one
final presentation.
