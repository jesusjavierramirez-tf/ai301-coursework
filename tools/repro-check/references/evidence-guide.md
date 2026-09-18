# Evidence guide: where proof lives in a reproduction package

## Environment

Where it lives: In the repro report's environment record, compared with the issue context's stated version, platform, runtime, or configuration requirements. In live mode, also check the issue thread and repository documentation when they define the target environment.

What good looks like: The recorded environment contains the details needed to determine whether the reproduction matches the issue's target. Any relevant difference between the reported environment and the issue target is explicitly identified.

## Steps

Where it lives: In the repro report's reproduction procedure, including its starting state and the actions taken before the behavior is observed. In live mode, compare these steps with the issue description and any repository-provided reproduction instructions.

What good looks like: A stranger can start from the stated starting state, follow the listed actions, and reach the reported test condition without needing unstated actions or private knowledge.

## Behavior shown

Where it lives: In the repro report's output excerpts, logs, screenshots, test results, or other artifacts, read against the issue context and its described behavior.

What good looks like: The artifacts demonstrate the behavior described by the issue, including the relevant input and observed result, or they provide sufficient evidence that the issue cannot be reproduced. Evidence of a different or adjacent problem does not establish the issue.

## Honesty

Where it lives: At the connection between the repro report's stated outcome and its supporting artifacts, plus the claim comment's wording about what is being investigated.

What good looks like: The stated outcome does not claim more than the evidence establishes. A report that honestly says the issue could not be reproduced passes when its evidence supports that conclusion; a confident reproduction claim without matching evidence does not.

## Comms

Where it lives: In the claim and repro comments, compared with the issue thread, the repo-facts block, the repository's bug-report conventions, contribution policy, and any AI-use disclosure requirement.

What good looks like: The claim describes the issue being investigated and promises investigation rather than a fix or a date. The repro comment states the observed result specifically and follows required repository conventions, including AI-use disclosure when required by the repository policy.
