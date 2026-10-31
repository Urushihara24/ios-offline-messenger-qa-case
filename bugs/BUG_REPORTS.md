# Bug Reports

## Defect summary

| ID | Title | Severity | Priority | Status |
|---|---|---|---|---|
| BUG-01 | Partial text selection is unavailable | Medium | P1 | Reproduced |
| BUG-02 | Whole-chat delete action is exposed from single-message context | Medium | P2 | Reproduced |
| BUG-03 | Reply action loses source-message context | Medium | P2 | Reproduced |
| BUG-04 | Editing own profile hangs on endless loader | Medium | P1 | Reproduced |
| BUG-05 | Crash when opening a fully empty correspondent profile | High | P1 | Reproduced |

---

## BUG-01 — Partial text selection is unavailable

**Severity:** Medium  
**Priority:** P1  
**Related test case:** IOS-018  
**Reproducibility:** 100%

### Preconditions

A chat containing a text message is open.

### Steps

1. Long-press a text message.
2. Attempt to select only part of the message using standard iOS selection handles.

### Actual result

The long press immediately opens the message context menu. Standard partial-text selection handles are unavailable.

### Expected result

The user can select part of the message text as required by the acceptance criteria.

### Evidence

A screenshot was captured in the original QA delivery. The public repository does not publish client screenshots.

---

## BUG-02 — Whole-chat delete action is exposed from single-message context

**Severity:** Medium  
**Priority:** P2  
**Related test case:** IOS-059  
**Reproducibility:** 100%

### Preconditions

A chat containing at least one message is open.

### Steps

1. Select a single message.
2. Inspect the available destructive action.
3. Choose the displayed chat-delete action and confirm it.

### Actual result

The whole chat is deleted from a context initiated by selecting one message.

### Expected result

A whole-chat destructive action should be clearly separated from message-level interaction or otherwise provide unambiguous context before destructive confirmation.

### Note

This is primarily a UX/destructive-action risk rather than a mandatory acceptance failure.

---

## BUG-03 — Reply action loses source-message context

**Severity:** Medium  
**Priority:** P2  
**Related test case:** IOS-058  
**Reproducibility:** 100%

### Preconditions

A chat containing a text message is open.

### Steps

1. Select an existing message.
2. Choose **Reply**.
3. Enter reply text.
4. Send the reply.

### Actual result

A normal outgoing message is created without a quote, reply preview or visible association with the source message.

### Expected result

The sent message should retain visible reply context linking it to the selected source message.

---

## BUG-04 — Editing own profile hangs on endless loader

**Severity:** Medium  
**Priority:** P1  
**Related test case:** IOS-060  
**Reproducibility:** reproduced for multiple profile attributes

### Preconditions

The own profile has already been created and is available for editing.

### Affected operations

- changing own name;
- changing birth date;
- changing own avatar.

### Steps

1. Open own-profile editing.
2. Change one of the affected attributes.
3. Save the change.

### Actual result

A loading indicator appears and the operation does not complete.

### Expected result

The change should be saved, the loader should finish and the UI should remain interactive.

### Scope note

The hidden editor is optional scope, so this defect does not change the mandatory 8/9 acceptance result.

---

## BUG-05 — Crash when opening a fully empty correspondent profile

**Severity:** High  
**Priority:** P1  
**Related test case:** IOS-061  
**Reproducibility:** 2 / 2 controlled reproductions

### Preconditions

A correspondent exists with a chat, but all profile data has been removed through the service editor.

### Steps

1. Open the dialog with the empty-profile correspondent.
2. Tap the correspondent name/profile in the chat header.

### Actual result

The application terminates.

### Expected result

The profile screen should safely render an empty/default state without crashing.

### Technical evidence

Two independent crash reports from build 17 matched on:

- `EXC_BREAKPOINT`;
- `SIGTRAP`;
- faulting thread `0`;
- the same top application framework;
- the same frame-offset sequence.

See [Crash Analysis](../docs/CRASH_ANALYSIS.md).

### Root-cause constraint

No source-level root cause is claimed because the matching dSYM was not available for symbolication.
