# Lesson 01 · Conversation evidence

AI-drafted task summary, not a transcript or grade. It may be public. Use actual
short quotes or labeled paraphrases, name any help supplied, and link actual
work. Leave missing contributions Pending. A learner can review, correct or
remove excerpts before publication; accuracy approval is not proof of learning.
Label role-play honestly rather than treating it as an actual learner response.

**Lesson:** STUDIO-001. **Available conversation context:** Claude Code
desktop chat, 2026-10-27 to 2026-11-06, from clone and setup onward.

**Classroom example (step 1):** Tried calc.mywebclass.org (instructor's
deployment, not the learner's): "both results appeared almost simultaneously
even when i used ridiculous numbers to try and break it with overflow."

**Proxy difference (after AI explanation of Caddy vs Traefik):** "caddy makes
it so that all the info is up in the repo/cloud and the information is updated
when changes are made to it specifically instead of being detected
automatically with traefik." (AI added: keeping the Caddyfile in the repo is
this setup's choice; Caddy itself just reads a file on the server.)

## Prediction

Before the plan was explained (after the Caddy/Traefik discussion): "im not
exactly sure but i think browser > network query > droplet then the droplet
responds."

## Check interpretation

Shown the `verify` division-by-zero case (input ÷ 0, expected rejection, actual
HTTP 400): "without the check we would be breaking the api." After an AI hint
about what the single check did not try: "this one check leaves open the
opportunity to keep functioning without crashing the whole system because of
one error." (Describes the benefit of rejecting bad input; the check's limits
were not stated. Gap preserved.)

## Browser observation

On their own URL (https://calc.acw33firstliveproj.online), asked to try 6 × 7:
"It responded almost instantly with both results and told me they match."

## Keep decision

"I will keep." Reason: because i belive that i have a good understanding.

## Review

On 2026-11-06 the learner was shown the quoted excerpts and AI summary, added
their own keep reason directly in this file, and approved the record as
accurate before the first commit. Approval covers record accuracy only.

## AI work and next step

AI help: confirmed the clone (`ACW900/IS373_hosting`), diagnosed GitHub SSH
(learner added their key; it is passphrase-protected), switched origin to SSH
and ran `studio.py setup` successfully. Learner gave their usual server SSH
command; it uses a nonstandard port the CLI cannot pass, so with approval the
AI added a laptop SSH alias `acw33` in `~/.ssh/config` (outside this repo; host
details are kept there, not here). Learner enabled ssh-agent; AI confirmed
non-interactive login and Docker access without sudo. Learner chose
`calc.acw33firstliveproj.online`; `configure` and read-only `doctor` reported
ready on network `web`.

**Baseline gap (resolved with a Caddy route):** the server's proxy is Caddy (static Caddyfile from the
learner's CI/CD repo), not Traefik. The studio CLI routes only through Traefik
labels, so a launch would run the container without a public HTTPS route.
`doctor` does not detect this. Learner chose to add a Caddy route. Learner
created issue #1; AI recorded it and created branch `studio-001-calculator`.
With approval, AI ran `launch`: the container `is373-studio-calculator-calculator-1`
started healthy on `web`; trusted HTTPS was not ready (expected: no Caddy
route yet). Existing site/QA/Caddy containers remained up. AI drafted the
`calc.` Caddyfile block (validated by the server's Caddy without reload) and
committed it on `qa` with approval; learner pushed; CI/CD run #14 succeeded.
AI ran `verify`: passed (see SPEC) and exported
[studio/evidence.json](studio/evidence.json). Local `check --fast` on Windows:
Black passed; Pylint/pytest hit Linux-only APIs (see SPEC); full check pending
in PR CI. Open: check limits (gap), PR/CI, merge of the Caddy route to the
CI/CD repo's `main`.
