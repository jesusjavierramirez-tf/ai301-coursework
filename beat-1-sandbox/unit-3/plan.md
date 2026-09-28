# Unit 3 — Plan

## Issue
#53 — PII scrubber fails to redact parenthesized US phone numbers

## Diagnosis
The phone-number regex in `safety/pii_scrubber.py` does not match the parenthesized US format `(555) 123-4567`, so `scrub()` leaves the number unredacted and `detect()` returns no match.

## Scope
In scope:
- `safety/pii_scrubber.py`
- The four related tests in `tests/unit/test_pii_scrubber.py`
- Update the phone-number matching logic to recognize the parenthesized US format.

Out of scope:
- Changes to unrelated PII types.
- Changes to unrelated files or scrubber behavior.
- Refactoring the entire PII detection system.

## Implementation Plan
1. Inspect the existing phone-number pattern in `safety/pii_scrubber.py`.
2. Update the pattern so it recognizes `(555) 123-4567` while preserving the existing supported phone-number formats.
3. Inspect the four tests in `tests/unit/test_pii_scrubber.py` and remove their `xfail(strict=True)` markers as required by the repository's issue contract.
4. Run the focused PII scrubber tests.
5. Confirm the parenthesized number is detected and replaced with `[REDACTED]`.
6. Confirm the existing phone-number cases still pass.

## Test Plan
Run the focused PII scrubber tests and verify:
- `(555) 123-4567` is detected.
- `scrub()` replaces the number with `[REDACTED]`.
- The four previously failing tests now pass without `xfail`.
- Existing supported phone-number formats continue to pass.

## Risks / Unknowns
The existing regex may support several phone-number formats, so the change must preserve those formats rather than replacing the pattern with a narrower one.

## Plan Comment
I plan to update the phone-number matching logic in `safety/pii_scrubber.py` so parenthesized US phone numbers such as `(555) 123-4567` are detected and redacted, then remove the related strict xfail markers and run the focused tests.
