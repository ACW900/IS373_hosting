# Lesson 01 specification

## STUDIO-001 · Launch a tested calculator on an existing server

**Status:** Scope agreed; launch and evidence pending.
**Next step:** Launch, add the Caddy route, then verify ([Lesson 01](studio/lesson-01.md) step 3).
**Instructor implementation:** [issue #9](https://github.com/kaw393939/373_hosting/issues/9).
Create your own issue from the [lesson template](.github/ISSUE_TEMPLATE/studio-calculator.md).

## Agreed result

Launch the supplied published calculator image through your existing Traefik
network and a nonconflicting HTTPS hostname. Preserve unrelated services and
host access. Do not add another proxy/updater or build a substitute image.
The [release selection](studio/calculator-release.json) supplies the expected
commit and multi-platform digest independently of the running website.
An explicitly agreed adoption of a matching existing deployment is recorded
as adoption, not a fresh launch. This bounded lesson does not certify the whole
server baseline or a vulnerability-free image.

- **Public hostname:** `https://calc.acw33firstliveproj.online` (existing DNS
  already resolves to the server; no route existed before this lesson).
- **New launch or adopted deployment, and reason:** New launch. `doctor`
  reported `launch-new` with no existing calculator deployment; on 2026-11-06
  `launch` started the container but stopped at its HTTPS wait (no Caddy route
  yet), so it saved no launch report. The later `verify` reports
  `already-managed`, which describes that verification, not the creation.
- **Caddy route:** [ACW900/IS-373-TEST-CICD@7e9bf1e](https://github.com/ACW900/IS-373-TEST-CICD/commit/7e9bf1e)
  on `qa`, deployed by [CI/CD run #14](https://github.com/ACW900/IS-373-TEST-CICD/actions/runs/42262618440)
  (succeeded). Not yet merged to `main`.
- **Own issue / feature branch:** [ACW900/IS373_hosting#1](https://github.com/ACW900/IS373_hosting/issues/1)
  / `studio-001-calculator`.
- **Agreed scope or actual access/configuration gap:** One pinned image on the
  existing Docker network `web`, without sudo. Gap: the server's proxy is Caddy
  (static Caddyfile in the learner's CI/CD repo), not Traefik. The CLI's
  Traefik labels are inert there, so public routing needs one added `calc.`
  Caddyfile block deployed through that repo's workflow. `doctor` does not
  check this route. No proxy is added or replaced.

Private SSH targets and configuration stay in ignored local state. Share only
reviewed, selected evidence; never commit credentials or raw server output.

## Evidence to keep

| Evidence | Actual result / link |
|---|---|
| Prepared Black/Pylint/pytest and real-image browser checks | Local `check --fast` on Windows (2026-11-06): Black passed; Pylint and pytest failed on Linux-only APIs (`os.geteuid`/`os.chown`, `signal.SIGHUP`) in unchanged template code. Local E2E not run. Full check and E2E: PR CI on Ubuntu, pending |
| Hosted image/commit, trusted HTTPS, valid and rejected API cases | `verify` passed 2026-11-06T17:34Z: pinned digest and commit `4600202` match; trusted HTTPS; 6×7 → 200/42; ÷0 → 400; numeric string → 422. Export with `report` pending |
| Preservation of unrelated services | `verify`: 3 existing containers unchanged (identity, state, ports) |
| Own prediction, check interpretation, browser observation and keep/revise reason | [LEARNING.md](LEARNING.md): all recorded with AI help disclosed; check limits not stated (gap) |
| Accuracy review before publishing learner excerpts | Learner approved accuracy 2026-11-06, before first commit |
| Actual PR, latest CI, merge and issue closure | Pending |

Exported evidence: [studio/evidence.json](studio/evidence.json). Link actual CI
and the PR when available.
CI does not deploy this server. A fixture, green check, timestamp, closed issue
or AI assertion alone does not establish the full result. `status` reports
recorded evidence and readiness for instructor review; it does not grade,
certify authorship or establish understanding.

## Optional instructor history

The records below are background, not steps to repeat. Their original anchors
remain here so earlier links continue to work.

## HOST-001 · Keep the Traefik dashboard private

[Historical requirement and evidence](book/changes/hosting-spec-history.md#host-001--keep-the-traefik-dashboard-private).

## HOST-002 · Controlled host maintenance

[Historical requirement and evidence](book/changes/hosting-spec-history.md#host-002--controlled-host-maintenance).

## HOST-003 · Companion image security maintenance

[Historical requirement and evidence](book/changes/hosting-spec-history.md#host-003--companion-image-security-maintenance).
