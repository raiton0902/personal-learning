# Installation

Install the entire `personal-learning` folder, including `references`, `scripts`, and `agents`. Copying only `SKILL.md` leaves supporting links incomplete.

## Codex: local installation

The bundled Codex skill installer uses `$CODEX_HOME/skills`, or `~/.codex/skills` if `CODEX_HOME` is unset. These commands follow that convention. See [official skill documentation](https://developers.openai.com/codex/skills/) for current host guidance.

Open a terminal in the repository root, beside README.md.

### Windows PowerShell

```powershell
$skillBase = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $HOME '.codex' }
$skillTarget = Join-Path $skillBase 'skills/personal-learning'
if (Test-Path -LiteralPath $skillTarget) {
    throw "A skill already exists at $skillTarget. Back it up before replacing it."
}
New-Item -ItemType Directory -Path (Split-Path -Parent $skillTarget) -Force | Out-Null
Copy-Item -LiteralPath './personal-learning' -Destination $skillTarget -Recurse
Test-Path -LiteralPath (Join-Path $skillTarget 'SKILL.md')
```

The final command should return `True`.

### macOS or Linux

```sh
skill_target="${CODEX_HOME:-$HOME/.codex}/skills/personal-learning"
if [ -e "$skill_target" ]; then
  printf '%s\n' "A skill already exists at $skill_target. Back it up before replacing it."
else
  mkdir -p "$(dirname "$skill_target")"
  cp -R ./personal-learning "$skill_target"
  test -f "$skill_target/SKILL.md" && printf '%s\n' 'Skill files copied.'
fi
```

Start a new turn and invoke `$personal-learning`. If it is not discovered, reopen the chat or restart the host and check the destination. Avoid an extra nested `personal-learning/personal-learning` folder.

## Install from GitHub after publication

This local repository has no published URL yet. Once published, give Codex the real URL and ask:

```text
Use $skill-installer to install the personal-learning folder from this repository:
<paste the actual GitHub repository URL here>
```

For ZIP downloads, extract the repository first, then follow the local installation instructions from its root.

## Other AI hosts

Use the host's documented skill-loading mechanism if it supports this format. Otherwise, ask it to read `personal-learning/SKILL.md` and linked references as needed. Without filesystem access, provide those files in the conversation. Manual instruction loading is not a native integration; behavior may differ between hosts.

## Verify

Ask:

```text
Use $personal-learning to help me study basic algebra.
Ask about my goals and materials, then propose a curriculum for approval.
```

The host should gather missing context and wait for curriculum acceptance before teaching. This checks the entry flow, not overall tutoring quality.

## Optional review helper

Python 3.10+ is needed only for this helper; no packages are required. From the repository root:

```sh
python personal-learning/scripts/select_review.py --help
python personal-learning/scripts/select_review.py /path/to/state.json --today 2026-10-17 --count 2 --seed 42
```

Replace the example path and date with your saved state file and local date. Use `python3` if that is your Python command. Omit `--seed` for ordinary randomized selection. See the [state example](personal-learning/references/continuity.md) and [review policy](personal-learning/references/review-policy.md).

## Update or remove

Manual installation makes a copy. Back up the installed skill folder before replacing it with an updated complete folder. Keep course records elsewhere.

To uninstall, remove only the installed `personal-learning` skill folder. Course records remain in the location you chose for them.
