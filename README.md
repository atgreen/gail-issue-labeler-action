# gail-issue-labeler-action
> Add labels to your GitHub issues automatically using LLMs

The `gail-issue-labeler-action` uses
[`gail`](https://github.com/atgreen/gail/) to automatically assign
labels to your repo's Issues as they are created.

The choice of labels comes from `.gail-labels` in your repo's root
directory.  For example, the `libffi` project uses `gail` and labels
Issues based on operating system and processor family with the
following `.gail-labels` file:

```
# This is a list of labels to be used for automatic tagging
# of github issues using gail: https://github.com/atgreen/gail

# Main categories
BUILD-ERROR
RUNTIME-ERROR
FEATURE-REQUEST

# Operating systems
ANDROID
IOS
LINUX
MACOS
SOLARIS
WINDOWS

# Processor families
AARCH64
ALPHA
ARC
ARM
AVR32
BLACKFIN
CSKY
HPPA
IA-64
KVX
LOONGARCH64
M68K
M88K
MICROBLAZE
MIPS
MOXIE
OPENRISC
POWERPC
RISC-V
S390
SPARC
TILE
VAX
WASM
X86
XTENSA
```

To use this Action, simply create a `.gail-labels` file and copy
something like the following into `.github/workflows/label-new-issues.yaml`:

```
on:
  issues:
    types: [opened]

jobs:
  label_issue_job:
    permissions: write-all
    runs-on: ubuntu-latest
    name: Label new issue
    steps:
      - id: label-new-issue
        uses: atgreen/gail-issue-labeler-action@master
        with:
          llm_api_key: ${{ secrets.OPENAI_KEY }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

### Inputs

| Input          | Description                | Default | Required |
|----------------+----------------------------+---------+----------|
| `llm_api_key`  | OpenAI API key for GAIL    | n/a     | yes      |
| `github_token` | GitHub token for API calls | n/a     | yes      |

### Outputs

None
