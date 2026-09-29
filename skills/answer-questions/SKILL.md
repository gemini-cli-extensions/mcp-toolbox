---
name: answer-questions
description: >-
  Answer a factual question about MCP Toolbox for Databases from the published
  docs and source code instead of from memory, and label every claim with where
  it came from and which version it holds for. Use whenever someone asks whether
  Toolbox supports something, what fields a source or tool takes, what
  `--prebuilt <x>` actually serves, what a flag or error means, what changed
  between versions, or why a `tools.yaml` is rejected. Use it also whenever you
  are about to state a config key, tool `type`, or flag name you have not just
  read.
---

# Answer Toolbox questions from the docs and the code

Toolbox ships roughly monthly across ~40 integrations, so config keys, tool
`type` strings, and flags all move. Look it up, then say where you looked.

**Never state a config key, tool `type`, flag, or "yes, it supports that"
without reading it in this session.**

## Which version

**Answer for the latest release and say so.** The unversioned docsite always
serves the current stable release, and the [Reference](#reference) links below
point at it. Do not go hunting for an installed binary: most questions (does
Toolbox support X, what does this tool do, how do I start) never need one.

Read the version you are answering for from the top of `llms.txt`, which names
it directly:

```
**DOCUMENTATION VERSION:** v1.12.0
```

Pin to the user's own build only when they ask something specific to a version:
they quote a startup error, ask why their `tools.yaml` is rejected, ask what
changed between releases, or name a version themselves.

```bash
toolbox --version    # toolbox version 1.12.0+binary.darwin.arm64
```

The git tag is `v` plus the part before `+` (here, `v1.12.0`). The first metadata
field after `+` is the build type, which decides the tree to read:

| Build type | Means | Read from |
|---|---|---|
| `binary`, `container` | A release | Tag `v<version>` |
| `dev` | Built from source | The user's checkout, else `main` |

Whichever version you land on, read docs and code at the **same** one. Skew makes
you recommend fields that do not exist yet, and it explains nearly every apparent
docs-versus-code conflict.

## Step 1: Docs first

The docs publish a machine-readable page index:

```
https://mcp-toolbox.dev/llms.txt              # current stable release
https://mcp-toolbox.dev/v<version>/llms.txt   # a specific release
https://mcp-toolbox.dev/dev/llms.txt          # unreleased, tracks main
```

- **Format:** one line per page, `- [Title](permalink): description`, indented
  two spaces per nesting level. Tool pages sit six deep, so anchoring a search
  at `^- [` finds only the six top-level sections. Fetch the index, find the
  permalink, then fetch that page.
- **Size:** ~120 KB. Its sibling `llms-full.txt` holds the whole corpus at ~2 MB,
  so reach for that only after a targeted page hunt has failed.

Docs are authoritative for concepts, quickstarts, deployment, and anything the
user will read themselves. They are not authoritative for the exact set of
config keys, which is Step 2.

## Step 2: Code for exact behavior

Go to the code when the docs are silent, ambiguous, or stale, or when the
question is exactly what something accepts or does. No checkout, no auth:

```
https://raw.githubusercontent.com/googleapis/mcp-toolbox/v<version>/<path>
```

Use the tag that matches the version from the previous section. Use `main` only
when you are answering about unreleased behaviour, and say that you did.

| Question | Path |
|---|---|
| Fields a source accepts | `internal/sources/<source>/<source>.go`, `Config` struct |
| What a tool accepts and does | `internal/tools/<source>/<tooldir>/<tooldir>.go`, `Config` struct then `Invoke` |
| What `--prebuilt <x>` serves, and which env vars it reads | `internal/prebuiltconfigs/tools/<x>.yaml`, the literal config: every tool name, every toolset, and the `${ENV_VAR}` behind each source field |
| CLI flags | `cmd/internal/flags.go` |
| Whether a source or tool exists at all | The Step 1 `llms.txt` index (one line per tool page, titled with the exact `type`) |

Deriving `<tooldir>`:

- **It is the tool `type` with the hyphens removed**, nested under its source
  family. `postgres-sql` becomes `internal/tools/postgres/postgressql/`, and
  `firestore-list-collections` becomes
  `internal/tools/firestore/firestorelistcollections/`.
- **A 404 at the derived path is itself an answer:** that tool does not exist at
  that version.
- **Confirm the `type` string against the constant** near the top of the file.
  Tools and sources name it differently:

  ```go
  const resourceType string = "postgres-sql"   // internal/tools/...
  const SourceType   string = "postgres"       // internal/sources/...
  ```

### Reading a Config struct

The struct tags are the config surface, so one block answers most "what can I
set" questions:

```go
Host          string `yaml:"host" validate:"required"`
QueryExecMode string `yaml:"queryExecMode" validate:"omitempty,oneof=cache_statement cache_describe describe_exec exec simple_protocol"`
ConnectTimeout *int  `yaml:"connectTimeout" validate:"omitempty,gte=1"`
```

- `yaml:"..."` is the exact key in `tools.yaml`: camelCase, never the Go field
  name. The one key absent from every Config is `kind`: it selects which struct
  to decode into and is stripped before decoding, so do not call it invalid just
  because no struct tag carries it.
- `validate:"required"` means required. Anything else (`omitempty`, or no
  `validate` tag at all) is optional.
- `oneof=` is the **complete** allowed set. Nothing outside it is valid.
- A pointer (`*bool`, `*int`) distinguishes unset from zero, usually meaning the
  driver default applies when unset.
- Tool configs embed `tools.ConfigBase`, which supplies `name`, `description`,
  `authRequired`, and `scopesRequired`. Do not report those as missing just
  because the tool's own struct omits them.

## Step 3: Label every claim

Attribute inline and carry the version. An unlabeled answer is indistinguishable
from a guess.

- `[docs v1.12.0]` plus the page link, so they can read it themselves
- `[code v1.12.0 internal/sources/postgres/postgres.go:56]`
- `[UNVERIFIED]` for reasoning or recall you could not confirm, with what would
  confirm it

**When docs and code disagree at the same version, code wins.** Answer from the
code, say plainly that the docs are wrong, quote the line that settles it, and
point the user at <https://github.com/googleapis/mcp-toolbox/issues> to file a
docs bug.

## Rules

- **Answer for the release, not for `main`.** When something exists on `main` but
  not the version you are answering for, say so precisely: "not in v1.12.0, landed
  after it, currently in `dev`, shipping in the next release." Never hand a
  release user a config key only `main` accepts.
- **Do not invent field names or tool types.** If it is not in the struct tags,
  the prebuilt YAML, or `--help`, it does not exist. Say so, and say what you
  searched (version, docs pages, code paths) so the next step is obvious. "I
  could not find it" is a valid answer; a plausible-looking key is not.
- **Prefer what the user can verify locally.** `toolbox --help`, `toolbox invoke
  <tool> '<json>' --config tools.yaml`, and the server's own startup error settle
  a question about *their* setup better than any URL.
- **Answer the question that was asked.** One line with a citation beats a tour
  of the configuration system.

## Reference

- [Configuration reference](https://mcp-toolbox.dev/documentation/configuration/)
- [All sources and tools](https://mcp-toolbox.dev/integrations/)
- [Documentation index](https://mcp-toolbox.dev/llms.txt)
- [Source and releases](https://github.com/googleapis/mcp-toolbox)

<!-- {x-release-please-start-version} -->
This skill ships with mcp-toolbox-devkit v0.7.1.
<!-- {x-release-please-end} -->
