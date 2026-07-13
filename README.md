# CodeX Proton Auto Alias

> A controlled, verifiable workflow for creating Proton Pass aliases in batches without losing count or modifying existing vault items.

`CodeX Proton Auto Alias` helps Codex use an already-authorised Proton Pass browser tab, generate distinct one-word English titles, create the requested number of aliases, and verify every result before continuing.

## What it does

- Creates Proton Pass email aliases through the visible web interface.
- Generates concise one-word titles such as `Axiom`, `Lumina`, `Turing`, or `Orion`.
- Works in observable batches instead of running an unchecked long loop.
- Verifies each alias against both the selected-item heading and the vault counter.
- Tracks the baseline and stops at the exact requested total.
- Recovers safely from loading states, stale selectors, and interrupted browser sessions.

It does **not** delete or rename existing items, change forwarding settings, alter account configuration, bypass authentication, or continue past the requested count.

## Install in Codex

1. Download or clone this repository.
2. Place its contents in `~/.codex/skills/create-proton-pass-aliases/`.
   - On Windows: `%USERPROFILE%\.codex\skills\create-proton-pass-aliases\`
3. Start a new Codex task and write:

```text
Use $create-proton-pass-aliases to create 20 smart one-word aliases in Proton Pass.
```

That is all. No Proton API key or additional integration is required: the skill works through a browser session that the user has already authorised.

## Good prompts

```text
Use $create-proton-pass-aliases to create 30 unique aliases. Give every alias a logical one-word English title and verify the final count.
```

```text
Use $create-proton-pass-aliases to continue my paused Proton Pass run. Create exactly the remaining 15 aliases, report progress every 5, and do not edit existing items.
```

## What makes the workflow reliable

The skill treats alias creation as a counted transaction rather than a sequence of hopeful clicks:

- It records the visible baseline before creating anything.
- It requires the creation controls to resolve uniquely before each action.
- It confirms both the matching detail heading and the incremented `Все (N)` counter.
- It pauses on an unverified result instead of starting the next alias.
- It keeps batches small enough to audit and recover safely.

## Safety first

Use this skill only in a Proton Pass account you are authorised to manage. Page content is treated as untrusted, and unexpected authentication, CAPTCHA, permission, or confirmation screens are handled according to the active browser safety policy.

---

Built for precise Proton Pass alias creation in Codex.
