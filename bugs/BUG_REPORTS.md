# Bug Reports — Build 17

## Defect summary

| ID | Title | Severity | Priority | Related case | Status |
|---|---|---|---|---|---|
| BUG-01 | Partial message-text selection is unavailable | Medium | P1 | IOS-018 | Reproduced |
| BUG-02 | Whole-chat delete is exposed from single-message context | Medium | P2 | IOS-059 | Reproduced |
| BUG-03 | Reply loses source-message context | Medium | P2 | IOS-058 | Reproduced |
| BUG-04 | Editing own profile hangs on endless loader | Medium | P1 | IOS-060 | Reproduced |
| BUG-05 | Fully empty correspondent profile causes application crash | High | P1 | IOS-061 | Reproduced 2 / 2 |

See [TEST_CASES.md](../test_cases/TEST_CASES.md) for the full execution matrix and [LEGEND.md](../docs/LEGEND.md) for status/severity conventions.

---

## BUG-01 — Partial message-text selection is unavailable

**Severity:** Medium  
**Priority:** P1  
**Related test case:** IOS-018  
**Reproducibility:** 100%  
**Acceptance impact:** Direct mandatory acceptance failure

### Preconditions

A chat containing a text message is open.

### Steps to reproduce

1. Long-press a text message.
2. Attempt to select only part of the message using standard iOS selection handles.

### Actual result

The long press immediately opens the message context menu. Standard partial-text selection handles are unavailable.

### Expected result

The user can select part of the message text as required by the acceptance criteria.

### Evidence

Screenshot captured in the original QA delivery. The public repository does not publish client screenshots.

---

## BUG-02 — Whole-chat delete is exposed from single-message context

**Severity:** Medium  
**Priority:** P2  
**Related test case:** IOS-059  
**Reproducibility:** 100%  
**Acceptance impact:** Secondary UX/destructive-action risk

### Preconditions

A chat containing at least one message is open.

### Steps to reproduce

1. Select a single message.
2. Inspect the available destructive action.
3. Choose the displayed chat-delete action.
4. Confirm deletion.

### Actual result

The whole chat is deleted from a context initiated by selecting one message.

### Expected result

A whole-chat destructive action should be clearly separated from message-level interaction or otherwise provide unambiguous scope before confirmation.

### Evidence

Screenshot captured in the original QA delivery.

### Classification note

The label matches the resulting action, so this is primarily a **context/UX risk**, not a proven backend or data-integrity defect.

---

## BUG-03 — Reply loses source-message context

**Severity:** Medium  
**Priority:** P2  
**Related test case:** IOS-058  
**Reproducibility:** 100%  
**Acceptance impact:** Additional functional defect outside the nine mandatory checks

### Preconditions

A chat containing a text message is open.

### Steps to reproduce

1. Select an existing message.
2. Choose **Reply**.
3. Enter reply text.
4. Send the reply.

### Actual result

A normal outgoing message is created without a quote, reply preview, or visible association with the source message.

### Expected result

The sent message retains visible reply context linking it to the selected source message.

### Evidence

No separate public screenshot is included. The behavior was reproduced during the final QA run and recorded in the delivered execution sheet.

---

## BUG-04 — Editing own profile hangs on endless loader

**Severity:** Medium  
**Priority:** P1  
**Related test case:** IOS-060  
**Reproducibility:** Reproduced for multiple own-profile attributes  
**Acceptance impact:** Optional hidden-editor workflow

### Preconditions

The own profile has already been created and is available for editing.

### Affected operations

- changing own name;
- changing birth date;
- changing own avatar.

### Steps to reproduce

1. Open own-profile editing.
2. Change one of the affected attributes.
3. Save the change.

### Actual result

A loading indicator appears and the operation does not complete.

### Expected result

The change is saved, the loader finishes, and the UI remains interactive.

### Scope note

The hidden editor is optional scope, so BUG-04 does not change the mandatory 8/9 acceptance result.

---

## BUG-05 — Fully empty correspondent profile causes application crash

**Severity:** High  
**Priority:** P1  
**Related test case:** IOS-061  
**Reproducibility:** 2 / 2 controlled reproductions  
**Acceptance impact:** Stability defect in an editor-reachable state

### Preconditions

A correspondent exists with a chat, but all available profile data has been removed through the hidden service editor.

### Steps to reproduce

1. Open the dialog with the empty-profile correspondent.
2. Tap the correspondent name/profile in the chat header.

### Actual result

The application terminates.

### Expected result

The profile screen safely renders an empty/default state without crashing.

### Technical evidence

Two independent build-17 crash reports matched on:

- `EXC_BREAKPOINT`;
- `SIGTRAP`;
- faulting thread `0`;
- the same top application framework;
- the same application frame-offset sequence.

A live syslog was captured during the controlled reproduction.

See [Crash Analysis](../docs/CRASH_ANALYSIS.md).

### Diagnostic constraint

No exact source function or root cause is claimed because the matching dSYM was unavailable for symbolication. The evidence proves a stable crash signature, not a specific Swift failure mechanism.

---

## Defect prioritization summary

### Fix before final acceptance

- **BUG-05** — deterministic application crash.
- **BUG-01** — direct mandatory acceptance mismatch.

### Fix if hidden editor is part of operator workflow

- **BUG-04** — own-profile editing cannot complete.

### Secondary interaction / UX review

- **BUG-02** — destructive-action context.
- **BUG-03** — reply semantics.
