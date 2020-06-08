# NN - The Node CLI Helper

## What is this?

It's a tool designed for being used in the command line to process streams or files.
If you're a data scientist or hobbyist and find yourself working with JSON or CSV files a lot, but don't have the time or will to learn how to use `jq`, `awk`, `cut`, `tr`, `grep`, or `csvtool`, this is what you need!

**Features**:

- Automatically recognizes files as JSON, CSV, or plaintext, allowing you to use the same command for all file types.
- Lets you use familiar JS syntax to accomplish much with little effort
- Full NodeJS API support for those cases where you need to go all out

## How to use

- `yarn global add node-cli-processing` / `npm install -g node-cli-processing`
- `nn ./fruits.json "data.map(fruit => fruit.type = fruit.weight > 2 /*kilogram*/ ? 'melon' : 'other')"`

## More examples

Coming soon

## Planned Features

- Parse and serialize CSV via third-party package to include proper escaping
- Add a flag to automatically keep a log of commands executed
- Separat flags for disabling input or output parsing
- Add file ending detection to prioritize certain file type parsing
