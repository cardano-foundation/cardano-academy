# Aiken: Getting Started

We claimed it only takes minutes to get started with Aiken, so let's put this theory to test! On a Mac, install with the **homebrew** package manager…

```sh
brew install aiken-lang/tap/aikup
```
if you are using Linux, you can also use `npm`:

```sh
npm install -g @aiken-lang/aikup
```
This command installs ```aikup```, a basic cross-platform utility tool to download and manage Aiken across multiple versions and enable seamless one-click upgrades. Once installed, we can just run:

```sh
aikup
```

```aikup``` runs on its own, installing the latest version available. If we want, we can also install specific versions by specifying a version number. To review different commands available, run ```aikup --help```. Check you have the latest version by running:

```sh
aiken --version
```

## Language Server

The ```aikup``` command-line comes with a built-in language server.[^1] There are also plugins for most popular code editors that provide syntax highlighting and indentation rules for Aiken. I used *VSCode*[^2] for the code in this book. 

## Creating a project

Let’s create our first project. Use ```aiken new cfacademy/cfaiken``` to create the scaffolding for a new project. We can follow instructions in the newly generated ```README.md``` at the root of the project. The folder structure should look like this:

```sh
.
├── README.md
├── aiken.toml
├── env
├── lib
└── validators
	└── placeholder.ak
```

## Common commands

Let’s familiarise ourselves with some common commands. We can first run ```aiken check``` to check everything locally first. Note this only type-checks a project and runs tests. 

```aiken check``` supports flags that allow you to run more specific tests–subsets of all tests in your project.

```sh
aiken check -m "cfacademy/cfaiken" 
```
This command runs only tests inside the module named ```cfacademy/cfaiken```. We can get even more granular by running the following command:

aiken check -m "aiken/option.{john}"

This command only runs tests within the ```aiken/option``` module that contains the word ```john``` in their name. We can be even more precise and use the ```-e``` flag, which will force an exact match 

```sh
aiken check -e -m exactly_this
```

This runs only tests in the whole project that exactly match the name ```exactly_this```. Next we’ll use ```aiken build``` to compile our project. If your project is more complex, with many custom libraries, you should use ```aiken docs``` to generate HTML documentation from types, type annotations and comments. That’s enough for now. We’ll explore more commands as we go. 

## Project folder structure

Let's review what we just created. Aiken projects split the source code into two categories: library code and application code. 

You’ll find the library code located in a ```lib``` folder, and the application code, meaning the on-chain ```validators```, in the validators folder.

When we run ```aiken build```, the compiler generates a CIP-0057 Plutus blueprint[^3] as a ```plutus.json``` file in the root folder of our project. This is the interoperable document we mentioned earlier. This is basically a summary of the project that contains the compiled code for each validator in the project. It also contains their corresponding hash digests that can be used to construct addresses. Note this blueprint is framework-agnostic so it enables interoperability between tools.

## Configuration

At the root level of the project, there should be an ```aiken.toml``` file with all the metadata about the project, including the dependencies required by it.

```sh
# Project's name, as {organisation}/{repository}
name = "cfacademy/cfaiken" 

# Project's version, we recommend semantic versioning for libraries. However,
# any UTF-8 string is accepted.
version = "0.0.0" 

# [Optional]
# A license name. We recommend Apache-2.0 or MPL-2.0 for open source projects.
licence = "Apache-2.0"

# [Optional]
# An informative albeit short description of the project.
description = "Aiken contracts for project 'cfacademy/cfaiken'" 

# [Optional]
# Structured information on a project to show in generated documentation.
[repository]
user = "cfacademy"		# Username or organisation on that platform
project = "cfaiken"	# Repository or project on that platform
platform = "github" 	# Platform type, only `github` for now. 

# [Optional]
# A list of dependencies. Avoid editing by hand, use `aiken packages` to manage them.

[[dependencies]]

source = "github"            # Platform type, only `github` for now.
name = "aiken-lang/stdlib"   # The github project, in the form of {organisation}/{repository}.

version = "v2.2.0"            
source = "github"
[config]
```

## Important packages & modules

```prelude``` hosts the bare minimum set of functions, constructors[^4] and modules that come automatically with all Aiken projects. The  ```builtin``` module exposes useful builtin functions from Plutus Core and is documented in ```prelude```.

The standard library, ```stdlib```, contains common functions and data-structures needed for most validators. If we go back to our ```aiken.toml``` file, we’ll see that standard library was added by default when we ran ```aiken new``` earlier. When we ran ```aiken check```, it would have downloaded any dependencies needed. 


[^1]: Language Server Protocol (LSP) enables convenience features like auto complete, go to definition, or pop-up documentation on hover over. The Language Server Protocol (LSP) standardizes how such servers and development tools communicate, so a single Language Server can be re-used for different tools and languages.
[^2]: VSCode plugin for Aiken, marketplace.visualstudio.com/items?itemName=TxPipe.aiken
[^3]: CIP-57 Plutus blueprint, github.com/cardano-foundation/CIPs/pull/258
[^4]:In class-based, object-oriented programming, a constructor is a special function used to create an object. It 'constructs' the new object so it's ready for use, usually by accepting arguments that the constructor needs to set required member variables.
