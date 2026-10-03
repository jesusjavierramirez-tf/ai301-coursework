---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

This tool answers exactly one question for exactly one PR package: "is this ready to submit?" It evaluates the candidate PR against its accepted plan, issue/repro context, test evidence, diff, commits, and repository requirements. It does not broaden the tool into code review, issue selection, implementation planning, or general PR advice.

## Inputs and modes

This tool has two modes.

Live mode:
- Read scope.md before anything else.
- Read voice-guide.md for the communication gate.
- Inputs are the issue/thread, plan.md and deviation notes, the branch diff (`git diff main...HEAD`), the draft PR title/description, captured test evidence, and the repository PR template, contribution instructions, and policy requirements.
- Only the scoped Path Review repository is allowed.
- Voice rules gate the outgoing PR title/description but do not independently change the verdict unless the rubric contains a relevant check.

Eval mode:
- The bundle is the complete world.
- Use only the evidence contained in the package.
- Do not fetch GitHub or other outside information.
- Evaluate exactly one package at a time.
- Read rubric.md and procedure.md before grading.

## The scope seam (live mode only)

Read scope.md first. If the repository does not match the allowed scope, refuse to grade. If scope.md still contains its placeholder repository, stop and ask the instructor rather than guessing. Eval mode ignores scope.md.

## The voice seam (live mode only)

Read voice-guide.md before reviewing the outgoing title/description. Check the candidate PR communication against the voice rules. Report a broken voice rule. Voice alone does not change the verdict unless a rubric check makes it consequential. Eval mode ignores voice-guide.md.

## Component reads

Use the exact read order from procedure.md:
1. issue and accepted plan context
2. plan scope/boundary, deviation notes, and test plan
3. candidate PR title and description
4. commits and unified diff
5. test evidence and repo checks
6. repository requirements and policies

The executor must use evidence-guide.md to locate evidence for each rubric family and rubric.md to determine pass/fail/unclear. The key comparisons are: plan vs. diff, description vs. diff, planned tests vs. actual test evidence, and repo requirements vs. PR contents.

## Verdict and output

Run all five required rubric checks independently. Each check gets exactly pass, fail, or unclear. Missing or contradictory required evidence is unclear. Unclear required checks cause rejection. Accept only when every required check passes. Reject when any required check fails or is unclear. No numeric score and no third verdict.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first.
- Grade the outcome, not writing polish.
- Rubric decides the verdict.
- Procedure decides how evidence is gathered; never improvise a new grading rule.
- evidence-guide.md tells the executor where evidence lives and what good looks like.
- Do not guess when evidence is missing.
- Do not allow one strong evidence family to substitute for another.
- Do not automatically reject an honestly disclosed shortfall when the remaining evidence establishes readiness.
- Description fidelity belongs to plan fidelity, not standards/comms.
- Standards checks only use requirements actually stated by the repository/package.
