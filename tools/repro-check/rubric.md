# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment | The repro report's environment record, read against the issue's stated version, platform, runtime, or configuration requirements. | Pass if the report records the environment details needed to determine whether the reproduction matches the issue's target, or explicitly identifies any relevant difference. | required |
| steps | The repro report's reproduction procedure, including the stated starting state and actions used to trigger the behavior. | Pass if a stranger could follow the described procedure from the stated starting state and reach the reported test condition without needing unstated actions. | required |
| behavior_shown | The repro report's output excerpts, logs, screenshots, or other artifacts, read against the issue description and its expected behavior. | Pass if the artifacts demonstrate the behavior described by the issue, or demonstrate that the issue cannot be reproduced; evidence of an adjacent or different problem does not pass. | required |
| honesty | The repro report's stated outcome and the evidence supporting that outcome. | Pass if the conclusion matches what the evidence actually establishes; an evidenced cannot-reproduce result passes, while a confident claim of reproduction without supporting evidence fails. | required |
| conventions | The claim/repro comments and the repo-facts block, including the repository's bug-report conventions and contribution policy. | Pass if the comments follow the repository's stated conventions and include any required AI-use disclosure when the repo policy requires it. | required |

## Verdict rule

Accept if every required check passes. Preferred checks, if added later, never change the verdict. Any `unclear` result on a required check counts as fail. Reject if any required check fails or is unclear.
