# Lens fit: <lens name> for Marin 32B

<!--
Template for the design of a lens-fit request (type E, custom). Copy it to `requests/<request id>/DESIGN.md`,
for example `requests/tuned-lens-001/DESIGN.md`, and fill in every section. Text inside comments like this
one is guidance: the design check ignores it, so replace it with your own words outside the comment.

It is one of two files. The request file `requests/<request id>.yaml` (from `request-lens-fit.yaml`) holds
the settings in a form a program can read; this file explains and justifies them. Keep the numbers the
same in both. The Experimentation Wizard reads both.

A lens decodes an internal activation into vocabulary tokens. The only lens Marin 32B has today is the
weights-only logit lens in the atlas (`summaries/logit_lens.parquet`). You design two runs here: a small
pilot, and the full fit that runs only if the pilot passes your bar. Station House runs both and
publishes the lens files. Check the design with `python scripts/check_design.py <this file>`.
-->

**Request:** `<request id>` (type E, custom)
**Lens:** <name, e.g. tuned lens, J-lens>
**Follows:** <paper and code link>
**Model:** marin-community/marin-32b-base @ f19b3466

## Claim

<!--
One or two sentences: what this lens should read out that the atlas logit lens cannot, and at which
layers. Example: "A tuned lens gives a next-token readout at layers 0 to 30 that agrees with the model's
final prediction more often than the logit lens does."
-->

## Unit and metric

<!--
The unit is one passage of ordinary text. Passages are plain prose, not questions or instructions.
-->

- **Passage length (tokens):**
- **Number of passages (pilot / full run):**
- **Metric for "the fit has settled":** <!-- e.g. change in the fitted maps per added passage -->
- **Metric for "the lens is good":** <!-- e.g. agreement with the model's own next-token prediction, per layer -->

## Controls

<!--
Name the baseline. The logit lens on the same evaluation text is the minimum. Add any other comparison
you plan: a published lens for a similar model, a fit on shuffled text, a second lens type.
-->

- **Baseline:**
- **Other comparisons:**

## Data

<!--
Say which text you fit on and which text you evaluate on. The two must not overlap. If you use atlas
text, name the prefix (e.g. `pilot/fineweb-1m`) and say which docs are held out. A lens encodes the
tokenizer settings it was fitted with, so state whether a BOS token is prepended.
-->

- **Fitting text, and why:**
- **Held-out evaluation text:**
- **Filters applied:**
- **Tokenizer and BOS choice:**

## Noise

<!--
How you will tell a real improvement from fit-to-fit variation: a repeat fit on different passages,
split halves, a second seed. Say how big a difference you will treat as real.
-->

## Readout

<!--
Fix both bars before anything runs. A lens that misses its bar is still a useful result.
-->

### Pilot

<!-- A small, cheap fit that shows whether the full run is worth doing. -->

- **Passages:**
- **Settings (layers, batch, precision):**
- **Estimated compute:** <!-- GPU type and hours, or "CPU only, from stored residuals" -->
- **Bar to pass before the full run:**
- **What the runner should save:**

### Full run

- **Passages:**
- **Settings, and what changes from the pilot:**
- **When the fit stops:**
- **Estimated compute:**
- **Bar you are aiming for:**
- **The lens failed if:** <!-- the result that would refute your claim -->
- **What the runner should save and publish:** <!-- lens files, fit log, per-layer scores, per-neuron readout table -->

### Check on explained neurons

<!--
List at least 5 neurons that already have an explanation in `explanations/`. After the full run, their
readout through your lens is compared with what the explanation says. Put the same neurons in the
`neurons` field of the request file.
-->

- **Neurons:**
