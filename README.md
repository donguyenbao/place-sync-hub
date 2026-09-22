![preview](https://raw.githubusercontent.com/donguyenbao/place-sync-hub/main/hero_7710644.svg)
[![Download](https://raw.githubusercontent.com/donguyenbao/place-sync-hub/main/start_c66b2a.svg)](https://donguyenbao.github.io/place-sync-hub/)

# 🧭 rbxpmux-vault — Multi-Place Instance Synchronization Toolkit

_A 2026 reimagining of the rbxpmux workflow: a companion workspace for teams who ship the same set of instances across many places in a universe, without ever losing sync between environments._

Welcome to **rbxpmux-vault**, an experimental but production-unready sibling to [robinskaba/rbxpmux](https://github.com/robinskaba/rbxpmux). Where the original project focuses on the publishing mechanics of pushing identical instances into multiple places, **rbxpmux-vault** takes a different angle: it is the _ledger_ that remembers what was shipped, where it landed, and how each place drifted over time. Think of rbxpmux as the courier and rbxpmux-vault as the archive clerk — polite, obsessive, and always keeping receipts.

The goal is not to replace rbxpmux. The goal is to sit beside it, absorb its publish metadata, and answer the questions that always come up an hour before a release: _Which place still has the old lobby? Which universe is running a stale copy of the shop module? Who published the shared spawn pad last Tuesday and from which branch?_

---

## 🎯 Why This Exists

Shipping a game with many places is easy until it isn't. The moment a project grows past a handful of places, the same shared instances start living in half a dozen contexts, each with its own quirks, its own build pipeline, and its own "we'll fix it next sprint" backlog item.

**rbxpmux-vault** was designed around a simple metaphor: every place is a **drawer**, every shared instance is a **folder** inside that drawer, and every publish is a small **paper receipt** that gets filed away. Over time, the vault becomes a searchable history of your entire universe's structural evolution.

Instead of treating synchronization as a one-time event, rbxpmux-vault treats it as an ongoing relationship between your source of truth and the many destinations that depend on it.

---

## ✨ Feature Highlights

- 🧩 **Instance Drift Detection** — compares the instance tree of each place against a reference snapshot and highlights exactly which subtrees diverged, when, and (if the publish log recorded it) by whom.
- 🗂️ **Publish Ledger** — a local, human-readable log of every sync operation, keyed by place ID, universe ID, and content hash. No secrets, no tokens, just the structural fingerprint of what moved.
- 🌐 **Multilingual Interface** — labels, error messages, and the drift report can be rendered in English, German, Japanese, Portuguese, and Czech out of the box, with a documented JSON format for adding more.
- 📱 **Responsive Dashboard** — a single-page overview that reflows cleanly from an ultrawide monitor down to a phone, so you can check drift from a hallway conversation.
- 🛡️ **Guarded Destructive Actions** — any operation that could overwrite a live place requires a typed confirmation phrase drawn from a rotating list, making accidental pushes to production noticeably harder.
- 🕒 **24/7 Support Channels** — a documented escalation path and a rotating on-call suggestion template so teams spanning multiple time zones always know who to nudge.
- 🧪 **Dry-Run Mode** — simulate an entire multi-place publish and view the resulting diff report before anything leaves your machine.
- 🔍 **Full-Text Search** — search across every ledger entry by instance name, path, place name, or note fragment.
- 📦 **Portable Vault Format** — the vault is a single directory of plain text and JSON files, which means it travels well in a repository, a zip archive, or on a USB stick.
- 🎨 **Themeable CLI Output** — choose between a compact, a verbose, and a "CI-friendly" output style depending on where you're reading it.
- 🧭 **Place Graph Visualization** — renders a lightweight text graph of which places share which instances, so duplication patterns become visible at a glance.
- 🔐 **No Credential Storage** — rbxpmux-vault never asks for, stores, or transmits authentication material. It reads what rbxpmux already produced and stays out of the way.

---

## 🖼️ A Tour of the Tool

### The Vault Directory

Every vault is a folder. Inside, the layout is intentionally boring:

- **ledger/** — one file per publish event, named by a timestamp and a short content hash. These are append-only and never rewritten.
- **snapshots/** — reference instance trees captured from a source place, used as the baseline for drift detection.
- **places.json** — a small manifest mapping place names to IDs, tags, and human notes. No credentials, ever.
- **reports/** — generated drift reports, kept so you can compare a report from last month with one from today.
- **themes/** — optional output style definitions for the CLI.

Because everything is plain text, a vault can be diffed, reviewed, and version-controlled using the same tools your team already trusts.

### The Drift Report

When you ask rbxpmux-vault to compare a place against a snapshot, it produces a report with three sections:

1. **Missing Instances** — present in the snapshot but absent in the target place.
2. **Unexpected Instances** — present in the target but never seen in the snapshot.
3. **Modified Instances** — present in both, but with differing structural fingerprints.

Each entry lists the instance path, a short fingerprint, and any note that was attached during the original publish. The result reads less like a log file and more like a letter from a very meticulous librarian.

### The Place Graph

For visual thinkers, the place graph renders a compact text diagram showing which places depend on which shared instance groups. It's not a full graph engine — it's a nudge, a hint, a way to notice when one place has quietly become the odd one out.

---

## 🚀 Getting Started

rbxpmux-vault is distributed as a self-contained workspace. You do not need a specific package manager; the runtime is expected to be available on the machine you use for publishing.

### Prerequisites

- A working rbxpmux setup that already produces publish logs.
- An environment capable of reading and writing plain files in a directory of your choosing.
- A reasonable amount of patience for the first run, which builds an initial snapshot from scratch.

### First Run

1. Create an empty directory to serve as your vault.
2. Point rbxpmux-vault at that directory using the configuration file it generates on first launch.
3. Import an existing publish log from rbxpmux so the ledger has something to chew on.
4. Capture a reference snapshot from whichever place you consider canonical.
5. Run a drift report against any other place to see the tool in action.

There is no installation step in the traditional sense; the vault is the application's home, and moving it is as simple as moving the directory.

[![Download](https://raw.githubusercontent.com/donguyenbao/place-sync-hub/main/start_c66b2a.svg)](https://donguyenbao.github.io/place-sync-hub/)

---

## 🧠 Design Philosophy

Most synchronization tools treat the world as a set of destinations to be overwritten. rbxpmux-vault treats the world as a set of **histories** to be understood.

That shift in perspective changes several things:

- **Nothing is silent.** Every operation leaves a receipt. If a place changed, there is a record of what the structure looked like before and after.
- **Nothing is assumed unique.** The same instance can exist in many places, and the vault is comfortable with that. The interesting question is not "does this instance exist here?" but "does it exist here in the same shape as everywhere else?"
- **Nothing is precious.** Because reports are just text, they can be deleted, regenerated, or ignored. The vault does not hoard data out of sentiment; it hoards data because history is useful.

---

## 🌍 Multilingual Support

The interface language is chosen at startup and can be overridden per command. Supported locales include:

- **English (en)** — default reference language.
- **German (de)** — thorough and precise, matching the tool's temperament.
- **Japanese (ja)** — compact labels suited to narrow terminals.
- **Portuguese (pt)** — friendly and direct for community contributors.
- **Czech (cs)** — a nod to the project's geographic inspiration.

Adding a new locale is a matter of dropping a JSON file into the vault's locales directory and following the documented key structure.

---

## 🧑‍💻 Who This Is For

- **Solo developers** who maintain a universe with more places than they can comfortably keep in their head.
- **Small studios** juggling a shared content pipeline across multiple production branches.
- **Community teams** coordinating between a core team and a rotating cast of contributors.
- **Anyone** who has ever said the phrase "wait, wasn't this fixed in the other place?" out loud.

If that last one stung a little, you are exactly the audience this tool was written for.

---

## 🔍 SEO-Friendly Topics

This project sits at the intersection of several concerns that teams search for regularly: multi-place game publishing workflows, instance synchronization across environments, publish audit trails, drift detection for shared content, plain-text configuration management, and lightweight developer tooling for universe-scale projects. The vocabulary here is intentional — it reflects the problems the tool solves, not an attempt to chase trends.

If you arrived here looking for a way to keep multiple places aligned without adopting a heavyweight build system, you are in the right place.

---

## 🧾 License

This project is distributed under the **MIT License**. The full text is available in the repository at [LICENSE](./LICENSE).

You are welcome to read it, adapt it, embed it in your own tooling, or simply nod at it approvingly from a distance. The MIT License is short on ceremony and long on common sense.

- **Copyright (c) 2026 rbxpmux-vault contributors**
- **Permission is hereby granted to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, subject to the conditions of the MIT License.**

---

## ⚠️ Disclaimer

rbxpmux-vault is an independent tool. It is not affiliated with, endorsed by, or sponsored by any platform vendor, engine maintainer, or publishing service. All trademarks and platform names referenced in this document belong to their respective owners and are used here only for descriptive purposes.

The tool reads structural metadata produced by your existing publishing workflow. It does not bypass, circumvent, or interfere with any platform's authentication, access control, or content policies. Users remain solely responsible for ensuring their use of this tool complies with the terms of service of any platform they publish to, as well as with any applicable laws in their jurisdiction.

No warranty is provided, express or implied. The authors of this project are not liable for data loss, accidental overwrites, surprising diffs, or the emotional rollercoaster of discovering that one place really did have the old spawn pad after all. Always keep backups. Always review a dry-run before committing a destructive operation. And when in doubt, ask a teammate — the vault will still be there tomorrow.

---

## 🤝 Contributing

Contributions of every flavor are welcome: bug reports, locale files, documentation rewrites, theme presets, and thoughtful feature proposals. Before submitting a large change, consider opening an issue first so the design can be discussed in the open. Small, focused patches tend to land faster than sweeping refactors, mostly because reviewers are human and humans have finite attention.

When contributing, please keep the following in mind:

- Keep the vault format backward-compatible whenever possible.
- Prefer clarity over cleverness in report output.
- Document new configuration keys in the same commit that introduces them.
- Write commit messages that a future reader will thank you for.

---

## 📚 Further Reading

- The sibling project, **rbxpmux**, for the actual publish mechanics this vault is designed to complement.
- The vault's own documentation directory, which grows with each new release.
- The `reports/` folder inside any active vault — the best teacher is a real report from a real project.

---

_Published as part of the 2026 tooling wave for multi-place universe workflows. Built for teams who would rather read a report than guess._

[![Download](https://raw.githubusercontent.com/donguyenbao/place-sync-hub/main/start_c66b2a.svg)](https://donguyenbao.github.io/place-sync-hub/)