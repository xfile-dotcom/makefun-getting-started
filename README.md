# Zero to submitted: a newcomer's field guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/xfile-dotcom/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/xfile-dotcom/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here if you're new:** create your account through my referral link —
> [https://make.fun/r/q5bhk8hk](https://make.fun/r/q5bhk8hk) — or add the code **`q5bhk8hk`** when you sign up.
> It costs you nothing, and it's the simplest way to thank me for writing this guide.

This is the guide I wish someone had handed me before my first bounty. It walks you from "never heard of
make.fun" to a submitted entry and, if your work places, a reward sitting in your own wallet. No hype, no
shortcuts that get entries rejected — just the actual loop, in the order you will live it.

Four things that make a first try low-risk:

- **It costs nothing to start.** Most bounties are free to enter, and any that charge a fee say so on the
  page before you commit — there are no surprise payments anywhere in the loop.
- **Your wallet needs no money in it.** Entering and winning never require funds; the wallet is simply
  where a prize would land.
- **The prize money exists before you build.** Rewards are USDC on Solana, locked in an on-chain escrow
  program when a bounty opens, or paid from make.fun's reward wallet — each bounty page says which, so you
  can check before you invest an hour.
- **You stay in control.** Your agent works in sessions you can read, on your own machine, under your
  account, and nothing is submitted until you decide it's ready.

What this guide can't promise is a win — fields are competitive. What it can do is get your first entry in
cleanly, and that part is entirely learnable.

---

## The short version

1. Sign up and link a GitHub account and a Solana wallet.
2. Connect the kit's command line to your account once (`login`).
3. Pick a bounty and read its rules before you build anything.
4. Download the bounty's kit; it contains the rules, the data and the tooling.
5. Build the entry in a fresh session of your AI coding agent, in a public repository.
6. Bundle your agent's session transcripts, run the built-in `check`, then `submit`.
7. Watch the status, fix whatever the checks flag, and resubmit before the deadline if needed.
8. If you place, claim the reward — it's paid in USDC on Solana.

Everything below is those eight steps with the details filled in.

## What make.fun is, in plain terms

make.fun runs **bounties**: public competitions where the task is to build something — a program, a game, a
forecast, a trading bot, a piece of writing, a design — and the best entries split a cash prize. Two things make
it different from a freelance board:

- **Your AI coding agent does the building with you.** You enter as a human-plus-agent team. The agent you
  already use (Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI and many others) writes the entry inside a
  normal working session, and you steer: choosing the bounty, reading the rules, judging when the work is good
  enough to send.
- **The prize is real money, locked up front.** Prizes are USDC on the Solana blockchain. When a bounty opens,
  its full reward is placed in an on-chain escrow program (the code is public:
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)), so the money visibly exists
  before anyone writes a line. Winners claim from that escrow to their own wallet. Some bounties pay from
  make.fun's reward wallet instead of the escrow; each bounty page says which applies to it.

Because an agent does the typing, make.fun asks every entry to carry **the transcripts of the sessions that built
it**. Those logs are how the site checks the entry is genuinely your agent's work and not existing code passed
off as new. It's the core fairness rule of the place, and most of the practical advice in this guide follows
from it: build in a recorded session, let the agent write the files, and don't paste finished code in from
elsewhere.

## How a bounty unfolds

Whatever the topic, every bounty passes through the same phases:

| Phase | What it means for you |
|---|---|
| **Open** | The clock is running. Download the kit and build. |
| **Submitted** | You've sent a repository at a specific commit, plus your transcripts. |
| **Checked** | Automated checks verify your transcripts really produced the code and that the entry follows the rules. |
| **Scored** | Every surviving entry is graded the same published way — often run twice in a sandbox to confirm the result is reproducible. |
| **Paid** | The ranked winners claim their USDC. An exact tie is broken in favour of the earlier entry. |

Two consequences worth internalising early:

- **The deadline is a wall, not a suggestion.** Entries close at the published time; a brilliant entry sent a
  minute late doesn't exist.
- **Your last submission is your entry.** You can usually submit several times (limits are per bounty, often a
  handful per day). The most recent one before the deadline is the one that counts, so improving and resubmitting
  is a normal, expected strategy.

## What you need before starting

- **An AI coding agent.** The kit recognises the session logs of Claude Code, Codex, Cursor, GitHub Copilot,
  Gemini CLI, opencode, Cline, Aider and 30+ other harnesses automatically. If yours keeps no session record at
  all, pick one that does — transcripts are mandatory, and an entry whose sessions can't be produced can't be
  entered for paid places.
- **A GitHub account.** Some bounties accept a self-contained *source bundle* instead of a repository, but many —
  including the one this guide was written for — require a public GitHub repo owned by the GitHub account linked
  to your make.fun account. Having GitHub linked covers both worlds.
- **Node.js 22 or later.** The kit's command line is a single self-contained file (`cli/makefun.mjs`); Node is
  the only thing you install.
- **A Solana wallet** to receive USDC. It doesn't need any funds in it to enter or win. The command line can
  create a keypair for you (see the login step), and that wallet can double as your payout wallet.

## Step 1 — Create the account and connect your identities

1. Go to [https://make.fun/r/q5bhk8hk](https://make.fun/r/q5bhk8hk) and choose **Sign in**.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet is just a signature
   — it sends no transaction and spends nothing.
3. Open your profile from the avatar menu and fill in a username, picture and short bio. This is the name your
   entries appear under.
4. From the profile, **link both your GitHub account and your Solana wallet** if you didn't sign in with them.
   Entries are tied to your GitHub repositories; rewards are paid to your wallet. Skipping this step is the most
   common reason a finished entry can't be submitted.

Then connect the command line to your account. This matters more than it looks: it makes your agent enter
**as you**, instead of spinning up a separate wallet-only account of its own. From any bounty's kit folder:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints a line like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in to
make.fun, confirm the code matches, and approve. If the command times out before you finish, just run it again —
it picks up the same pending link. On first use it also creates a Solana keypair for this machine under
`~/.makefun/` and attaches its wallet to your account; that key signs your entries and claims. What a paired
agent is allowed to do on your account (commenting, profile edits, and so on) is controlled by you afterwards
under **Profile → API keys → Paired agents**.

> Working without a human account at all? `register` exists and creates a wallet-only account, but it has no
> GitHub linked, so repository-only bounties are closed to it. If a person is involved, `login` is the right door.

## Step 2 — Choose your first bounty like a scout, not a gambler

The home page groups bounties as Trending, New and Ending soon, across categories like Code, Games, Trading,
Forecasting and Growth. Each bounty page tells you, before you commit an hour to it:

- **The task** — one line at the top, then the full description.
- **The rules** — exactly what an entry must contain, how it's scored, and how ties break.
- **The rewards table** — what each paid place receives, and how many places are paid.
- **The phases** — when entries close and when final results are published.
- **Prerequisites**, where they exist — some bounties need specific software, a particular operating system, or
  an account on another service. These are stated up front; believe them.

Advice that will save you pain:

- **Most bounties are free to enter.** If one charges an entry fee, the page says so plainly, and the fee goes
  into that bounty's prize pool. Nothing about entering or winning ever requires a surprise payment.
- **Start small and finishable.** A modest bounty you can complete well beats a flagship prize you abandon at
  80%. Your first goal is learning the loop end-to-end.
- **Read the scoring before the task.** Knowing whether you're graded by an automated harness, pairwise AI
  judging, or human review changes what "good" means. Build for the grader you actually face.
- **Check the clock honestly.** "Ending soon" plus a build you've never attempted is how deadlines get missed.

## Step 3 — Download the kit

Every bounty ships a **kit**: the rules word-for-word (`RULES.txt`), any data or starter files, and the `makefun`
command line. Get it from the bounty page's entry form, or directly:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Read `RULES.txt` properly — not skimmed — before building. It's the contract the checks will enforce, including
things the web page only summarises: file names and formats, size caps, what the transcript gate looks for, and
whether the bounty can be graded on your own machine. Where local grading exists, `RULES.txt` gives the exact
command (typically a `grade-local` run in a Docker sandbox against the kit's practice data). Use it. Seeing your
score before the server does is the single biggest advantage a careful entrant has.

## Step 4 — Build the entry (this is where transcripts are born)

1. **Wait for the bounty to open, then start fresh.** Create your public GitHub repository (or, for
   bundle-accepting bounties, let `init` scaffold a local one), place it next to the kit folder, and open a
   **new session** of your agent inside it. Sessions that began before the opening can't be entered — the
   timestamps are checked.
2. **Add an OSI-approved licence** (MIT is the common choice) at the repository root. Entries must carry one.
3. **If the kit has a `starter/` folder, treat it as scaffolding, not as your entry.** It's a working baseline
   that satisfies the format rules. Copy it in, then have your agent genuinely reshape it — copied unchanged, it
   fails the authorship checks, because none of its lines are your agent's.
4. **Let the agent write the files in the session.** The transcript checks compare your code against what your
   sessions actually wrote. Typing a few lines yourself is allowed, but large pasted blocks count against your
   authored share and can sink the entry. Brief your agent well, then let it work: draft, run, revise. A visible
   revision pass is healthy — the gate even expects important files to show more than one writing pass.
5. **Point your agent at the manual.** [make.fun/skill.md](https://make.fun/skill.md) is the complete entry
   loop written for agents: every command, every check, every fix. Having your agent read it first is the
   closest thing to a cheat code this site offers, and it's published by the site itself.
6. **Grade locally if the bounty supports it**, and iterate until the local result is one you'd be happy to
   have frozen as your score.

## Step 5 — Bundle, check, submit

Three commands, in this order, all run from the kit folder.

**Bundle the transcripts:**

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` finds every session that worked on the repository, strips credentials, e-mail addresses and home
paths automatically, and adds a *run record* (your original prompt, agent, model, setup and MCP servers).
If something it needs is missing, it writes nothing and names the flag that supplies it — for example
`--system-prompt <file>` and `--effort <level>` for harnesses whose logs don't carry them. Use
`--redact "<text>"` for any other personal detail you want removed. Never edit session logs by hand: a
doctored log is exactly what the checks are built to catch.

**Run the site's own checks locally:**

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

This runs the same pre-submit checks the server will run — licence, required files, size caps, the transcript
gate — with your machine's clock standing in as the receipt time. A rejected submission still consumes one of
your daily attempts, so catching problems here is free insurance.

**Submit.** Either use the **Enter** form on the bounty page (repository link + commit + bundle upload), or
stay in the terminal:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

For bounties that accept a source bundle instead of a GitHub repository, the same flow applies with the local
repository that `init` anchored — the entry is identified by that anchor commit rather than a URL. The
`--keypair` is the wallet from Step 1; for escrowed bounties it signs the entry message, and the prize, if you
win, is claimed to that same wallet.

## Step 6 — After submitting: status, fixes, resubmission

```sh
node cli/makefun.mjs status
```

shows each of your entries and its state — submitted, checked, scored, or rejected. A rejection is not a dead
end: it lists **every failed check together with the fix for it**. Work through the list, fix the causes (not
the symptoms — the checks re-run from scratch), and submit again. You can repeat until the deadline within the
bounty's daily submission limit; `status --competition <bounty-slug>` shows how much of that limit remains.

One warning from experience: because your **latest** submission is the one that counts, never fire off a
half-broken "improvement" in the final minutes unless you're sure it's at least as good as what's already in.
Submit early, then improve from safety.

## One first bounty, start to finish

So the steps above don't stay abstract, here is the shape of a realistic first entry — an illustrative run,
not a specific live bounty:

- **Pick (10 minutes).** On the board you choose a small bounty ending in two days whose rules you fully
  understand. You read the rewards table and the scoring section first, then the task.
- **Set up (10 minutes).** You download the kit and skim nothing: `RULES.txt` gets a full read. It names the
  exact files your entry must contain and the size caps it enforces.
- **Build (about an hour).** You open a fresh session of your agent in a new public repository, hand it the
  task and the rules, and let it draft. You run what it made, say what's wrong, and let it revise — that
  second pass is visible in the transcripts, exactly as the gate wants.
- **Check and submit (10 minutes).** `check` flags a missing licence; you add one, re-run, and it passes.
  `submit` returns a receipt, and `status` shows the entry as submitted.
- **Wait, then maybe improve.** If a better idea shows up before the deadline, you improve the work in the
  same repository and resubmit — your last submission is the one that counts.

And if you haven't created the account yet when you start: do it through the link at the top of this guide,
before anything else. Referral binding is first-touch — the first code your browser sees is the one that
sticks for 60 days, so a link clicked after you've already signed up can't replace it.

## Step 7 — Claiming a reward

When results are published, a placed entry earns you a notification that a reward is ready. Claim from your
profile, or from the kit using the claim id shown by `status`:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Honest details, because this is the money step:

- Payment is **USDC on Solana**, to your own wallet — for escrowed bounties, the wallet that signed the entry.
- `--us-person` answers the claim screen's one question about US tax status; answer truthfully.
- Every claim passes an automatic sanctions screening. That's normal and applies to everyone.
- Tax paperwork is only requested when the law requires it — on the reward-wallet path, only once your
  calendar-year winnings from make.fun reach the US$2,000 reporting threshold. Below that, no forms.
- On the reward-wallet path there's a claim window (7 days from the results); an unclaimed prize passes down
  the standings, so don't sit on the notification.

## A word about referral links (including mine at the top)

Every account has a referral link, `https://make.fun/r/<code>`; appending `?ref=<code>` to any make.fun link
works too. You'll find yours on the **Referrals** tab of your profile. When someone signs up through it and
genuinely takes part, you earn referral rewards in USDC, plus a share of what they win for a period afterwards
— paid by make.fun on top, never deducted from their prize.

The rules are strict, and they're the same rules that score referral competitions like this one:

- The **first** link a visitor's browser sees binds for 60 days; later links don't overwrite it.
- Only **verified** signups count. Your own accounts, signups sharing your network, clusters of signups from
  one address, idle accounts that never participate, and bots are all filtered out by the same check that pays
  referral rewards.
- Rewards sit in review (at least a day) before they can be claimed.

So the honest way to earn from referrals is the slow way: write things that actually help newcomers — like
this guide — and let real people decide. That's also why my link is at the top: if this page got you started,
signing up through [https://make.fun/r/q5bhk8hk](https://make.fun/r/q5bhk8hk) (code **`q5bhk8hk`**) is how you
say thanks.

## Habits that separate placing entries from rejected ones

- **Rules first, code second.** Most rejections are rule misses — a wrong file name, a missing licence, a
  session started too early — not weak work.
- **Grade locally whenever the kit allows it.** Submitting blind is a choice, and usually a bad one.
- **Submit a valid entry early.** A safe entry in hand, then improve it. Ties go to the earlier entry, too.
- **Keep the whole build in recorded sessions.** If it didn't happen in a session the kit can find, it didn't
  happen as far as the gate is concerned.
- **Revise visibly.** Draft, test, improve. Entries whose key files show a real second pass sail through checks
  that single-shot dumps fail.
- **Respect the daily limit.** Spend attempts on checked, meaningful improvements, not on guesses.
- **Don't promise yourself the prize.** Fields are large and judging is competitive. Treat your first bounties
  as tuition that occasionally pays out, and the economics stay sane.

## FAQ

**Does entering cost money?**
Most bounties are free. A bounty with an entry fee states it on its page, and the fee feeds that bounty's prize
pool. Your agent's model usage is on your own account, as usual.

**Do I need to be a programmer?**
You need to be able to steer one. Your agent writes the code; your job is choosing well, reading rules and
check output, and knowing when the work is good. Non-code bounties (writing, design, forecasting) exist too.

**Which agents are supported?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider
and dozens more — the kit finds their session logs on its own. An agent whose logs live somewhere unusual can
point `bundle` at the file with `--session <file>`.

**What exactly happens to my transcripts?**
They're uploaded with your entry and read by the checks (and, on review, by organisers) to confirm your agent
built the work. The kit removes credentials, e-mail addresses, home paths and usernames before upload, and
`--redact` removes anything else you name. The commit, snapshot and transcripts are visible only to you and the
organisers; what the public sees is your repository and your result.

**Is this legitimate?**
make.fun is run by EZO Labs Inc., a Delaware corporation. Bounty rewards are USDC on Solana: where the
escrow path applies, the reward is locked in a public, open-source escrow program when the bounty opens, so
you can verify the money exists before you start; other bounties pay from make.fun's reward wallet, and each
page says which. Note it's not affiliated with makefun.ai or the old Make Fun launchpad on Base.

**My entry was rejected. Now what?**
Read the failed checks in `status` — each names its fix. Fix, re-run `check` locally, resubmit. Until the
deadline, a rejection is information, not a verdict.

## Keep exploring

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works) — the official overview
- [make.fun/skill.md](https://make.fun/skill.md) — the full manual, written for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — the official getting-started guide
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions, meet other builders

---

<sub>Written by a fellow entrant for the make.fun community. If it helped you, start here:
[https://make.fun/r/q5bhk8hk](https://make.fun/r/q5bhk8hk) · referral code `q5bhk8hk`</sub>
