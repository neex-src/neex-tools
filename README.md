# neex-tools

Five tools. Each one is its own git repo. This repo only holds them together as git submodules.

All the code is written by AI (Claude Code) and has not been reviewed.

| folder         | what it is |
|----------------|------------|
| `reus/`        | Records what an AI coding agent (Claude Code, GitHub Copilot) does, as git commits. You look at every step later, with git or in the browser. |
| `deliberator/` | IntelliJ plugin, daemon (`deliberatord`) and CLI (`dlb`). Runs a microservice / AWS setup on your machine: services in Podman, AWS faked by Floci. |
| `inliner/`     | IntelliJ plugin "Inline Reading Mode". The body of a called method opens right under the call. You can follow a value and fold away the rest. |
| `sling/`       | A fake Ping Identity (ForgeRock) cloud tenant that runs locally: logins, journeys, OAuth, IDM, served from a Frodo export. |
| `devkit/`      | All of it inside one Podman container: Linux with IntelliJ and the two plugins, shown in your browser. |

## You need

- git
- [bb](https://babashka.org) (babashka)
- [Podman](https://podman.io)
- Java 21 or newer and the [Clojure CLI](https://clojure.org/guides/install_clojure): deliberator and sling
- Maven and Terraform: deliberator's example estate
- IntelliJ IDEA 2026.2 or 2026.3, for the two plugins

reus needs only git and bb. devkit needs only Podman, bb and fzf.

## Get it

    git clone --recurse-submodules https://github.com/neex-src/neex-tools.git
    cd neex-tools

Cloned without `--recurse-submodules`? Then `git submodule update --init`.

Newest of everything:

    git pull
    git submodule update --remote    # each tool to the newest main of its repo

## Run

Every tool has its own README with the details.

    cd reus && bb gui                    # http://127.0.0.1:7350
    cd deliberator && bb tour:ide        # a sandbox IntelliJ with the tour open
    cd sling && bb serve                 # the fake tenant on http://127.0.0.1:8080
    cd devkit && bb vm                   # the menu of the dev VM

## The plugins

Ready zips are on the Releases page of each repo:

- https://github.com/neex-src/deliberator/releases
- https://github.com/neex-src/inliner/releases

In IntelliJ: Settings, Plugins, the gear icon, Install Plugin from Disk, pick the zip, restart.

Or build them yourself:

    cd deliberator && bb ide:build       # ide/build/distributions/deliberator-0.1.0.zip
    cd inliner && ./gradlew buildPlugin  # build/distributions/inliner-0.1.0.zip
