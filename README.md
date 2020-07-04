# NN - The Node CLI Helper

[![MIT License](https://img.shields.io/badge/license-MIT-green)](https://github.com/VaguelySerious/nn/blob/master/LICENSE)
[![NPM Version](https://img.shields.io/npm/v/node-cli-processing?style=flat)](https://www.npmjs.com/package/node-cli-processing)

## What is this?

It's a tool designed for use in the command line to process streams or files.
If you're a data scientist or hobbyist and find yourself working with JSON or CSV files a lot, but don't have the time or will to learn how to use `jq`, `awk`, `cut`, `tr`, `grep`, or `csvtool`, this is what you need!

**Note**: JSON support is currently much more developed than CSV, though both formats are usable.  
**Note 2**: Since this is driven by NodeJS and not buffered by line (due to JSON / CSV parsing), **avoid** processing files larger than a Gigabyte or so if you value your memory and CPU cycles.

**Features**:

- Automatically recognizes files as JSON, CSV, or plaintext, allowing you to use the same command for all file types.
- Lets you use familiar JS syntax to accomplish much with little effort
- Full NodeJS API support for those cases where you need to go all out

## How to use

Install via yarn or npm

- `yarn global add node-cli-processing`
- `npm install -g node-cli-processing`

This will make the `nn` command available globally.

Use the command either with a file or via shell pipe

- `nn ./fruits.json "data = data.filter(fruit => fruit.type === 'citrus')"`
- `cat ./fruits.json | nn "data = data.filter(fruit => fruit.type === 'citrus')"`

The commands accepts the input and a string of JS code that is used to process the data.  
The file or STDIN content is made available as the `data` variable, after being automatically turned into a JS object or array if the input file is deteced as being a JSON or CSV file respectively.  
Afterwards executing the code provided, the content of the `data` variable is then piped to STDOUT, after being serialized as JSON or CSV if the type matches.  

**Flags**:  
- `--raw` disables automatic parsing and formatting as JSON/CSV. Use this if the wrong type is detected.

## More examples

Assuming `fruits.json` is a JSON file like so:

```json
[
  { "name": "Orange", "weight": 100, "type": "citrus" },
  { "name": "Apple", "weight": 80, "type": "boring fruit" },
  { "name": "Lemon", "weight": 60, "type": "citrus" },
  { "name": "Pear", "weight": 85, "type": "boring fruit" },
  { "name": "Sugar melon", "weight": 2500, "type": "melon" },
  { "name": "Honeydew", "weight": 2400, "type": "melon" }
]
```

and `fruits.csv` is a CSV file like so:

```csv
name,weight,type
orange,100,citrus
apple,80,boring fruit
lemon,60,citrus
pear,85,boring fruit
sugar melon,2500,melon
honeydew,2400,melon
```

Here are some possible use-cases:

- **Filtering by json attribute**: `nn ./fruits.json "data = data.map(fruit => fruit.weight > 2000)"`
- **Filtering by csv column**: `nn ./fruits.csv "data = data.map(fruit => +fruit[1] > 2000)"`
- **Sorting by json attribute**: `nn ./fruits.json "data = data.sort((a,b) => a.weight - b.weight)"`
- **Sorting by csv column**: `nn ./fruits.csv "data = data.sort((a,b) => +a[1] - +b[1])"`

Since this is driven directly by NodeJS, **everything** is technically possible.

## Planned Features

- Add file ending detection to prioritize certain file type parsing
- Allow manual choice between file types
- Alternate CSV parsing that produces a json array
- Parse numbers where possible in CSV format
- Parse and serialize CSV via third-party package to include proper escaping
- Add a flag to automatically keep a log of commands executed
- Separate flags for disabling input or output parsing
