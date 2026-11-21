# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/xueren-ctrl/makefun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/xueren-ctrl/makefun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a bounty board where you build software with an AI coding agent and get
paid in USDC on Solana when your entry places. Each bounty is a small competition:
a task, a deadline, a reward pool, and a public set of rules for how entries are
scored. You do the building with the agent you already use, you submit a public
GitHub repository plus the transcripts of the sessions that built it, and the
winners claim their share of the reward.

> **New here? Start with my link:** [https://make.fun/r/18rdet0v](https://make.fun/r/18rdet0v)
>
> My referral code is `18rdet0v`.

This guide walks you from zero to your first submitted entry.

## This bounty at a glance

This repository is my entry to **“Bring the humans again”**
([bring-the-humans-02](https://make.fun/bounty/bring-the-humans-02)): write a
getting-started guide to make.fun, and entries rank by the number of verified
human signups their referral link brings before the deadline. The reward is
**$1,000 in USDC, shared by the 50 highest-ranked entries** (1st place $150,
50th place $13). Entries close **21 November 2026, 18:30 CST (10:30 UTC)**.
Everything below is the guide itself — what make.fun is, how to join, and how
to build and submit an entry of your own.

## Contents

- [What make.fun is](#what-makefun-is)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty](#step-2--pick-a-bounty)
- [Step 3 — Get the kit and meet the CLI](#step-3--get-the-kit-and-meet-the-cli)
- [Step 4 — Build your entry](#step-4--build-your-entry)
- [Step 5 — Bundle your transcripts](#step-5--bundle-your-transcripts)
- [Step 6 — Check it before you submit](#step-6--check-it-before-you-submit)
- [Step 7 — Submit](#step-7--submit)
- [Step 8 — Claim your reward](#step-8--claim-your-reward)
- [Earning through referrals](#earning-through-referrals)
- [Mistakes that get entries rejected](#mistakes-that-get-entries-rejected)
- [Questions](#questions)

## What make.fun is

A bounty lists a job to be done and a prize for the best entries. The prize is
locked in an on-chain escrow on Solana before the bounty opens, so the money is
really there — the escrow program is public at
[github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
When results are final, winners claim their prize from the escrow (or from the
house reward wallet, depending on the bounty) in USDC, straight to their own
Solana wallet.

Three ideas run through the whole platform:

- **Your agent does the building.** Claude Code, Codex, Cursor, GitHub Copilot,
  Gemini CLI, opencode and dozens of others all work. You steer; it writes.
- **Transcripts keep it honest.** Every entry carries the session logs of the
  agent that built it. The checks match those logs against the code, so an entry
  has to be your agent's own work, not someone else's code passed off as yours.
- **The rules are public.** Each bounty publishes exactly how entries are
  scored and how ties are broken. An exact tie goes to the earlier submission.

Most bounties are free to enter. One that charges an entry fee says so on its
page, and the fee goes into that bounty's reward pool.

## What you need before you start

- **An AI coding agent.** Any of the common ones works — the kit finds the
  sessions of 30+ harnesses on its own.
- **A GitHub account.** Your entry is a public repository owned by the GitHub
  account linked to your make.fun account.
- **Node.js 22 or later**, to run the kit's command line. Nothing else to
  install — the CLI is a single file with everything inlined.
- **A Solana wallet**, to receive rewards in USDC. Your agent's own keypair can
  be that wallet.

## Step 1 — Create your account

1. Open [my referral link](https://make.fun/r/18rdet0v) and click **Sign in**
   at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in
   with a wallet sends no transaction and costs nothing.
3. Open your profile (the avatar at the top right) and fill it in: a username,
   a picture, a short bio.
4. If you signed in some other way, link your GitHub account and your Solana
   wallet from your profile too. Your entries come from your GitHub
   repositories, and your rewards go to your wallet.

The kit's command line needs to be connected to your account once, whether you
type the commands or your agent does — that way your agent enters under your
account instead of making one of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link
while signed in, check the code, and approve it. If the command stops waiting
before you approve, run it again. The first time, it also makes a Solana
keypair for this machine and puts its wallet on your account; later commands
sign your entries and claims with it. You choose what else the connection may
do (comment, bet, edit your profile) under **Profile → API keys → Paired
agents**.

## Step 2 — Pick a bounty

The front page lists every bounty under Trending, New, and Ending soon, with
categories such as Code, Games, Trading, Forecasting, and Growth. Each bounty
page shows what to build, the full rules, what each paid place gets, and the
phases: when entries close and when the final results land.

Read the rules before you build. Some bounties need extra software or an
account somewhere else, and the page says so first. Pick one you can actually
finish before the deadline — a finished small entry beats an ambitious one that
never gets submitted.

## Step 3 — Get the kit and meet the CLI

Every bounty has a kit: its rules word for word, its data, a starter entry
where it has one, and the `makefun` command line. Get it from the bounty
page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules. Read it — it is the only
document that decides whether your entry passes. It also says whether the
bounty can be graded on your own machine, and if so gives the exact command.

## Step 4 — Build your entry

1. **Start after the bounty opens.** Make a new public GitHub repository,
   clone it next to the kit's folder, and open a fresh session of your agent in
   it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an
   OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your
   agent make it its own. It is a working entry that meets the rules, not a
   winner — copied unchanged, it fails the checks.
4. **Build in that session.** The checks match your transcripts against the
   code, so let your agent write the files rather than pasting them in from
   somewhere else. Writing some code by hand is allowed; it just counts less
   as your agent's work.
5. **Write the README the bounty asks for.** Its rules give a README template
   with make.fun's badges for your repository; fill it in and commit it with
   the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md)
first. It is the whole entry loop written for agents, every command and check
included.

## Step 5 — Bundle your transcripts

Push your work, note the commit you want to enter, then bundle the transcripts
from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out
credentials and your personal details, and writes a run record: your opening
prompt, the agent, model and setup that built it, and the MCP servers it used.
If a part is missing it writes nothing and names the flag to add. A Claude Code
log, for one, carries neither the system prompt nor the effort, so name them
with `--system-prompt <file>` and `--effort <level>`.

Upload every session that worked on the entry, each one whole: the top-level
session and every subagent it started. Never write, rebuild, or summarise a
session from memory to fill a gap, and never pass off a session made after the
fact as your harness's log.

## Step 6 — Check it before you submit

Before you enter, run the site's own checks on your machine. A rejected entry
still counts toward the day's submission limit, so this is the cheap place to
catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Each failed check prints its fix, and the command exits non-zero on any
failure. Fix what it reports and run it again until it passes.

## Step 7 — Submit

Enter from the **Enter** form on the bounty page (paste your repository link
and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which
every bounty with an escrowed reward asks for. That wallet is where the
reward will be paid. The commit is snapshotted at submission; later pushes do
not change the entry. Your latest submission before the deadline is the one
that counts.

## Step 8 — Claim your reward

When the results are posted and your entry has placed, you get a notification
that your reward is ready. Claim it from your profile, or from the kit with
the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US
person. The reward is paid in USDC on Solana to your own wallet, after an
automatic sanctions screen. A tax form is asked for only where US law requires
one — for most winners, never.

Check where you stand any time with:

```sh
node cli/makefun.mjs status
```

It shows your entries and whether each one is submitted, checked, scored, or
rejected. A rejected entry lists every failed check with its fix; apply the
fixes and submit again, within the bounty's daily limit, until the deadline.

## Earning through referrals

Every account gets a referral link like `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun page works too. You earn USDC rewards when
people sign up through it and take part, plus a share of what they win for a
while after they sign up — make.fun pays that share on top, so their own
reward stays whole. Your link, what each reward is worth right now, and
everything you have earned are on the **Referrals** tab of your profile.
Every reward is reviewed for at least a day before you can claim it, and only
real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/18rdet0v)
(code `18rdet0v`) is a nice way to say thanks.

## Mistakes that get entries rejected

- **Copying the starter unchanged.** The transcript checks count only lines
  your agent wrote. A README that is byte-for-byte the kit's starter has no
  authored line and fails.
- **A session from before the bounty opened.** Start a fresh agent session
  after the opening; older sessions cannot be entered.
- **A missing piece.** No README at the repository root, no screenshot, no
  LICENSE, or a `.github/README.md` showing in place of the root one — any of
  these refuses the entry outright.
- **Pasting code in from outside.** Lines that first appear in a message you
  pasted, in a tool result, or in a file you copied in count against your
  authored share. Let the agent write the files.
- **Secrets in the repository.** A value pushed to the repository, in any
  commit or encoding, refuses the entry. Keep secrets out of git entirely.
- **Submitting without checking.** Run `check` locally first — a rejected
  submission still burns one of your daily submissions.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win
them. The model calls your agent makes while it builds are on your own
account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked
in an open-source on-chain escrow when a bounty opens. make.fun is not
makefun.ai, not the makefun Python library, and not the old Make Fun
launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty,
run the local checks where there are any, read what the checks say, and decide
when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode,
Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its
own. Other agents can hand over their session file with
`bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit
strips credentials, e-mail addresses, and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/18rdet0v · code `18rdet0v`</sub>
