# Installation

!!!warning npm install is currently broken
The published npm package is discontinued and `npm install -g mojic` will fail with a 404. Use the "from source" method below.
!!!

## From source (recommended, currently required)

```bash
# Clone and navigate to the directory
git clone https://github.com/notamitgamer/mojic.git
cd mojic

# Install dependencies and link it globally to use the 'mojic' command
npm install
npm link
```

## Via npm (currently broken)

```bash
npm install -g mojic
```

Or without installing:

```bash
npx mojic encode main.c
```
