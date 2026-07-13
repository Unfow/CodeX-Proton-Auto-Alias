---
name: create-proton-pass-aliases
description: Create verified batches of Proton Pass email aliases through an already-authorized browser session. Use when the user asks Codex to repeatedly create Proton Pass aliases, generate distinct one-word English titles, reach an exact alias count, or continue a previously paused Proton Pass alias-creation run.
---

# Create Proton Pass Aliases

Create exactly the requested number of aliases without changing existing items, forwarding settings, or account configuration.

## Prepare

1. Use the browser-control skill appropriate to the user's existing signed-in tab. Prefer Chrome when the task depends on the user's open Chrome session.
2. Claim the existing `Proton Pass Web App` tab instead of opening a duplicate.
3. Read the visible item count and record it as the baseline.
4. Convert the request into an exact target: `final item count = baseline + aliases to create`.
5. Prepare enough unique titles before starting. Use one English word per title. Prefer concise, intelligent concepts or proper names such as `Axiom`, `Lumina`, `Turing`, or `Orion`. Avoid titles already visible in the vault.

## Create Each Alias

Repeat this sequence once per requested alias:

1. Locate and uniquely verify the button named `Добавить новый элемент Создать элемент`.
2. Click it and take a fresh DOM snapshot.
3. Locate and uniquely verify `Псевдоним`, then click it.
4. Take a fresh snapshot and locate the `Заголовок` textbox.
5. Fill one unused one-word title.
6. Take a fresh snapshot and verify that `Создать псевдоним` is uniquely present and enabled.
7. Click `Создать псевдоним`.
8. Verify both authoritative signals:
   - the detail pane contains a heading exactly matching the title;
   - the `Все (N)` counter increased by exactly one.

Do not infer success from the click alone. Count an alias only after both signals pass.

## Work in Batches

- Use batches of about 10 aliases so progress remains observable and failures have a small recovery scope.
- Report the verified cumulative total between batches.
- Reuse stable locators only while the current snapshot supports them.
- Keep a local list of completed titles and the verified counter after every creation.
- Stop immediately when the requested number is reached. Never create an extra alias to test the interface.

## Recover Safely

- If a locator is missing or ambiguous, take a fresh snapshot and rebuild it from visible state. Do not retry the same failing selector blindly.
- If the new item is briefly marked as loading, wait for the matching heading or counter and re-snapshot. Use a short fixed delay only as a bounded fallback.
- If the counter does not increment, do not begin another alias. Determine whether the submitted item exists before retrying.
- If authentication, CAPTCHA, a permission prompt, or an unexpected confirmation appears, follow the browser confirmation policy and pause when user action is required.
- Never delete, rename, disable, or edit existing vault items while recovering.

## Finish

1. Verify the final counter equals the recorded baseline plus the requested number.
2. Verify the last alias heading.
3. Leave the Proton Pass tab open as a deliverable when the run is complete, or as a handoff when paused.
4. Report the number created, baseline and final counts, representative titles, and any failures or retries.
