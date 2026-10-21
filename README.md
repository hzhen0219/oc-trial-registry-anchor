# oc-trial-registry-anchor

External, append-only trust root for the oc-options-trader certificate **trial registry** (#640).

The trading host signs nothing itself. Its trial registry head is authenticated only by commits on
`main` of this repository, which must be **owned by hzhen0219** (not by the bot `stuart-minion-ai`).
The bot keeps *write* access only: it may append anchor commits, it can never rewrite or delete them.

The verifier (`scripts/external_anchor.py`) re-checks on every read, live against the GitHub API:

* repository is `hzhen0219/oc-trial-registry-anchor` and the bot is neither owner nor admin;
* a ruleset on `main` enforces **deletion** and **non_fast_forward** with no bypass for the bot;
* `main` is one linear chain.

If any check fails, every certificate read fails closed. Please do **not** make this repository
private (GitHub Free disables rulesets on private repositories), delete it, or remove its ruleset.

`owner-ruleset.json` is the exact ruleset. If it is ever missing, import it at
Settings -> Rules -> Rulesets -> New ruleset -> Import a ruleset.
