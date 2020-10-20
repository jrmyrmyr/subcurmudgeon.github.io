# publi.sh
Publi.sh is a wrapper for the pandoc universal document converter, written in bash, and intended for replicating directories of Markdown documents into HTML to be published on the web.

## Usage
`./publi.sh [options] <input directory> <output directory>`

## Options
| Flag        | Description                           |
| ----------- | ------------------------------------- |
| `-d`, `-v`  | display verbose debugging output      |
| `-h`        | display help                          |
| `-i <file>` | specify file to become index.html     |
| `-o`        | confirm overwrite of output directory |
| `-p <args>` | pass optional arguments to pandoc     |

### `-d`, `-v`
Verbose debugging output will display all options passed to pandoc, external or otherwise, as well as the input and output paths of each file being processed.

### `-i <file>`
If an `index.html` file is required but does not exist, any files glob-matching `file` will be renamed `index.html` upon conversion. For example, if every directory contains a markdown file beginning with the characters `000_` which serves as a table of contents, that may serve as a meaningful `index.html` when published online.

Example: `publi.sh -o -i "000_*.md" ~/markdown ~/public_html`

Here, each file matching `000_*.md` will be named `index.html` when converted.

### `-o`
By default, publi.sh will exit with an error if the chosen output directory is not empty to prevent accidentally overwriting its contents. The user can either remove the contents of the output directory prior to running publi.sh, or use the `-o` flag to acknowledge the overwrite and disable the error.

### `-p <args>`
Sometimes it may be useful to specify additional arguments to pandoc, such as `--title-prefix` or `--toc-depth`. This can be done using the `-p` flag, which can be specified multiple times if needed.

Example: `publi.sh -o -p --title-prefix="My Website" -p --toc-depth=3 ~/markdown ~/public_html`

Here, `--title-prefix` and `--toc-depth` will be passed to pandoc for every file converted. Some pandoc arguments are also able to be specified in a YAML header on a per-file basis. See the [pandoc user's guide](https://pandoc.org/MANUAL.html) for more information.

Example: `publi.sh -o -p --defaults="/home/user/.pandoc-defaults" ~/markdown ~/public_html`

Here, `--defaults` points to a YAML file containing pandoc options. See the [default files](https://pandoc.org/MANUAL.html#default-files) section of the [pandoc user's guide](https://pandoc.org/MANUAL.html).
