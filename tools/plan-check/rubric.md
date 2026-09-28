# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | The plan's stated cause read against the behavior and artifacts in the repro-evidence block. | Pass if the proposed diagnosis is supported by the reproduced behavior and does not contradict or ignore the evidence. | required |
| scope | The plan's in-scope and out-of-scope statements, including the files or areas named. | Pass if the proposed work is a bounded change that directly addresses the reproduced issue without unrelated scope creep. | required |
| executable | The plan's implementation approach, named files or code areas, and work sequence read against the repo-facts block. | Pass if a stranger has enough concrete information to begin the planned work without needing unstated investigation, setup, or implementation decisions. | required |
| testable | The plan's test plan read against the repro-evidence block's steps and artifacts. | Pass if the proposed tests directly reproduce the reported behavior and provide observable evidence that distinguishes the fixed behavior from the original failure; a broad test suite alone is not sufficient. | required |
| honest | The plan's stated unknowns, risks, assumptions, and deviations read against the available evidence. | Pass if uncertainty is stated where the evidence does not establish a fact, rather than presenting an unsupported conclusion as certain. | required |
| conventions | The plan comment read against the issue thread highlights and repo-facts block. | Pass if the comment follows the repository's stated contribution, communication, and AI-use requirements, including any restrictions on AI-generated comments. | required |

## Verdict rule

Accept if every required check passes. Reject if any required check fails or is unclear.
