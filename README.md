Generate `.npmignore`, `.dockerignore`, and any other `.*ignore` files from a single `.gitignore`.  This avoid repetition and keeps things DRY.

# Usage

Install:

    npm install -g generate-ignore

Or install locally for use in npm scripts:

    npm install --save-dev generate-ignore

Write your `.gitignore`:

```
##<generate npm />
.vagrant

##<for git>
lib
.npmignore
##</for>

##<for npm>
##tsconfig.json
##</for>
```

Run this tool from the same directory:

    generate-ignore

The first line, `##<generate ... />`, tells the tool to create a .npmignore file.
The `##<for>` and `##</for>` delimeters tell the tool to comment or uncomment those lines
in the appropriate .ignore files.

Our example above generates the following `.npmignore`:

```
##<generate npm />
.vagrant

##<for git>
##lib
##.npmignore
##</for>

##<for npm>
tsconfig.json
##</for>
```

The `<for git>` rules only apply to git, so they've been commented out.
The `<for npm>` lines, however, should apply to npm, so they've been uncommented.

`<generate>` and `<for>` tags can list multiple types of .ignore.  The following example will generate a `.npmignore` and `.dockerignore`:

```
##<generate npm docker />
##<for npm docker>
##test-harness
##</for>
```