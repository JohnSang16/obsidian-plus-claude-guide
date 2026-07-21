# Obsidian + Claude Code: A Student's Second Brain

A practical guide to pairing Obsidian (notes) with Claude Code (agent) into a self-maintaining personal knowledge base. Written from the perspective of a CS student juggling an internship, a student org, coursework, and a FAANG-prep grind, but the pattern generalizes to anyone who wants an agent that actually knows their life instead of starting from zero every session.

This guide leans on [Daniel Nest's "Build Your Second Brain With Claude Code & Obsidian"](https://www.whytryai.com/) for the core concept and setup steps. What follows is my own working system built on top of that idea, plus what I've learned running it daily.

---

## The idea

Claude Code already reads your whole working folder as context. The gap is that a chat-based agent has no durable, agent-agnostic place to keep what it learns about you, structured in a way you (a human) can also browse, link, and skim.

Obsidian fills that gap:

- **Notes are Markdown.** Exactly what Claude Code already reads and writes natively.
- **The vault is just a folder.** Point Claude Code at it and it has full context, no upload, no separate memory system to maintain by hand.
- **`[[wiki-links]]` connect ideas across notes.** Trivial for an agent to create and follow, and visually browsable for you in Obsidian's graph view.
- **It's agent-agnostic.** The vault outlives any single tool. If a better agent comes along next year, you point it at the same folder and keep going.

In short: Obsidian is the durable, human-readable memory. Claude Code is the agent that reads it, writes to it, and acts on it.

**Why this matters as a student specifically:** you're context-switching constantly (classes, internship, clubs, job search) and re-explaining your situation to an AI every session is wasted time. A vault + agent setup means the agent already knows your goals, your schedule, your ongoing threads, and can pull it all together on command instead of you reassembling it from memory every morning.

---

## Quick setup

Two installs, then you're ready to scaffold:

1. **Obsidian** (free): [obsidian.md](https://obsidian.md/download)
2. **Claude Code**: install steps and IDE/terminal setup are covered in Daniel Nest's [Claude Code series](https://www.whytryai.com/) (start with his "getting Claude Code running" post if you're new to it)

Create your vault as its own folder, then open Claude Code from that same folder. That's the entire technical setup. Everything else below is structure and habit, not tooling.

---

## Scaffolding from zero

Don't hand-design the folder structure up front. Let Claude Code interview you and propose one instead, it'll ask about your goals, your commitments, and how you actually think, then draft a structure you approve before it writes anything.

Starter prompt:

> I want to use Obsidian to help you and me better manage context. The vault is at [folder path]. Ask me about my goals, responsibilities, and how I want to work with you, one question at a time. Once we're aligned, propose a folder structure and starter files. Wait for my approval before creating anything.

From there, the one file that matters most is **`CLAUDE.md`** at the vault root. Claude Code reads it at the start of every session, and it should define:

- Who you are and what you're working on (link out to a profile/goals note, don't cram it all in-line)
- The vault's folder structure, so the agent knows where things belong
- Writing conventions (naming, linking style, tone)
- Any standing behaviors you want automated (auto-commit, daily briefs, etc.)

Everything downstream, daily logs, knowledge notes, slash commands, grows out of that one file staying accurate.

---

## My setup

```
vault/
├── CLAUDE.md              # entry point, read every session
├── HOME.md                 # daily cockpit / quick links
├── _meta/                  # identity + goals the agent references constantly
├── memory/                 # Claude Code's persistent cross-session memory
├── cox/                     # internship: daily logs, knowledge base, people, projects
├── career/                  # FAANG prep, LeetCode tracker, resume, LinkedIn drafts
├── progsu/                  # student org (Tech VP role): projects, people, knowledge
├── personal/                 # finances, fitness, personal projects
└── .claude/commands/         # slash commands, mirrored in _agents/commands/ by category
```

A few decisions that mattered more than the folder names:

- **Knowledge notes are separate from daily logs.** Daily logs are a stream of what happened; knowledge notes are distilled, linked, written for "me in six months," and filed into topic subfolders (`cox/knowledge/cs/web`, `.../security`, etc.). The daily brief flags things worth promoting into a knowledge note instead of letting them rot in a log.
- **`memory/` is not a task list.** It holds durable facts about how I work and what's been decided, not in-progress state. Tasks live in the actual planning tools; memory is for things that should still be true next month.
- **Commands are organized twice on purpose.** A flat `.claude/commands/` folder so Claude Code can find them, and a categorized `_agents/commands/<category>/` mirror so a human browsing the repo can find them too. The tradeoff (keeping two copies in sync) is worth it for readability.

---

## How I actually use it

**`/daily`** — a morning brief that pulls calendar, email, and messages, cross-references my LeetCode tracker and a FAANG-prep priority dashboard, and surfaces only what's actionable today. The point isn't the individual pulls, it's that the agent already has my goals and priorities on file, so the brief is filtered through "does this move the needle on what I've already told you matters," not a generic digest.

**Daily logging** — end-of-day, a `/eod`-style command writes a short shipped/pending/wins entry into the current week's log file. Cheap to do, and it's what turns into knowledge notes and future daily-brief context later. The agent flags patterns across logs (a topic showing up three days running, a person mentioned with no page yet) that I'd otherwise miss.

**Introspection and goal alignment** — because `CLAUDE.md` and `_meta/` encode my actual goals (not vague ones, specific ones with dates and named milestones), the agent can push back or reprioritize instead of just executing. Asking "what should I focus on this week" gets an answer grounded in what I've already committed to, not a generic productivity answer.

**LeetCode coaching (`/lc`, `/lc-coach`)** — a structured coaching protocol that never hands over the answer directly, tracks streak/session state in a tracker file, and is deliberately the one command that stays encouraging regardless of how the session goes. Consistency in tone across sessions is something a plain chat can't give you; a vault-backed command can.

**School-specific agents (`/tutor`, `/quiz`, `/hw-check`)** — coursework support that reads what I'm actually taking and where I'm stuck from vault notes, instead of generic tutoring. `/hw-check` in particular is just a review pass against my own submitted work before I turn it in.

**Auto-commit as an audit trail** — every meaningful vault change gets its own commit. It sounds like overkill until you realize it turns the vault into a real history of how your thinking and priorities evolved, not just a static snapshot.

---

## End notes

- **The vault is worth more than any single agent.** Markdown + Git means it survives tool churn. When a better agent shows up, it's a folder path, not a migration.
- **`CLAUDE.md` is the highest-leverage file in the whole system.** Everything else is downstream of it staying current. Review and edit it directly, don't just let it drift.
- **Let the agent do the admin work.** Filing, linking, flagging stale notes, that's exactly the "busy work between having an idea and executing on it" that a self-maintaining vault is supposed to remove. If you're manually tagging and organizing, you've recreated the problem Obsidian-plus-agent was supposed to solve.
- **Public and private don't mix in one repo.** If you're sharing your setup (like this guide), keep a sanitized version separate from the vault that has your actual daily logs, goals, and personal data in it.

Credit: this system is my own build, but the core concept, and the nudge to actually try it, comes from Daniel Nest's [Why Try AI](https://www.whytryai.com/) newsletter.
