# LTK Engineering ADRs

This is a repository where we keep track of ADRs, or architectural decisions that we make and their rationales.

## When do I use this?

If you are making a decision that feels "architecturally significant", such as choosing one framework over another, write a short ADR using [template.md](./docs/template.md) and open a PR.

## How do I get this merged?

You need at least one approval from a staff engineer, and 24 hours of no other dissent.

## Why do I need this?

When someone pops up in the chat saying "why did we do this?", you now have a record you can send them something that recorded that the decision was made, and _why_ it was made.

## How do I use the tooling in this repo?

The ADRs themselves are short markdown documents. This can be as lo-fi as you want it to be. Otherwise, the community has developed a CLI below that you can use to list them.

### Install

Install with [npm](https://www.npmjs.com/):

```sh
npm install -g adr-log
```

### CLI

```text
Usage: adr-log [-d <directory>] [-i <input>] [-p <path_prefix>]

  input:  The markdown file to contain the table of contents.
          If no <input> file is specified, an index.md file containing the log is created in the current directory.

  -i:     Edit the <input> file directly, injecting the log at <!-- adrlog -->.
          Using only the -i flag, the tool will scan the current working directory for all *.md files and
          inject the resulting adr-log into the default index.md file.
          (Without this flag, the default is to print the log to stdout.)

  -d:     Scans the given <directory> for .md files.
          (Without this flag, the current working directory is chosen as default.)

  -e      Exclude any files matching the given <pattern>

  -p:     Path prefix for each ADR file path written in log
          (Default is empty)

  -b      Change the character used to for bullets
          Supports: asterisk, dash, plus
          (Default is asterisk)

  -h:     Shows how to use this program
```

### Usage

#### Examples

##### Printing the adr log to stdout

Consider a directory consisting of three files (`0000-example-1.md`, `0001-example-2.md`, `0002-example-3.md`).
Execute following command:

```sh
adr-log -d .
```

This outputs following log on your console:

```markdown
* [ADR-0000](0000-example-1.md) - Example 1
* [ADR-0001](0001-example-2.md) - Example 2
* [ADR-0002](0002-example-3.md) - Example 3
```

##### Generating an index.md file containing the adr log

Since this is basically a fork of [Jon Schlinkert's](https://github.com/jonschlinkert) [markdown-toc](https://github.com/jonschlinkert/markdown-toc), you can also choose to insert the log into an existing file.
For this to work the file must contain an opening `<!-- adrlog -->` code comment, after which the log will be inserted.

If the file already contains an adrlog surrounded by an opening `<!-- adrlog -->` and closing `<!-- adrlogstop -->` code comment, the existing is be replaced.

Using `-i` alone (`adr-log -i`) generates an `index.md` file in the current working directory containing the log.

```sh
$ adr-log -i
```

Result in following `index.md`:

```markdown
<!-- adrlog -->

* [ADR-0000](0000-example-1.md) - Example 1
* [ADR-0001](0001-example-2.md) - Example 2
* [ADR-0002](0002-example-3.md) - Example 3

<!-- adrlogstop -->
```

#### Alternative Indexing

- search recursively underneath the given directory
- allow date prefixes as well as number prefixes
- allow specification of `index` or `date` properties in frontmatter
- fallback to auto-numbering for ADRs without filename prefixes or frontmatter

### Developing

- Run `node cli.js` to execute the CLI.
  Also works with relative directgories.
  E.g., `node ../../../adr-log/cli.js -d .` runs adr-log and outputs the result to the console.
- You can turn on debugging output by adjusting lines 6 and 7 in `cli.js`.
- Use [relase-it](https://www.npmjs.com/package/release-it) and [github-release-from-changelog](https://github.com/MoOx/github-release-from-changelog) for release management.
  See also [ADR-0003](docs/adr/0003-use-release-it-and-github-release-from-changelog-as-release-tooling.md).

### Related Tooling

[adr-tools](https://github.com/npryce/adr-tools) is the most prominent related tool.
It supports generating an ADR log by using `adr generate toc`.
An example to can be investigated at <https://github.com/npryce/adr-tools/blob/master/tests/generate-contents.expected>.

The difference to adr-tools is

1. adr-log is available using `npm` and thus more easy to install.
2. adr-tools does not include the heading of each ADR into the output.

### License

Copyright © 2017 [Tino Stadelmaier](https://github.com/tstadelmaier), [Oliver Kopp](https://github.com/koppor), [Armin Hüneburg](https://github.com/hueneburg), [Tobias Wältken](https://github.com/mee4895).

Released under the [MIT License](LICENSE).
