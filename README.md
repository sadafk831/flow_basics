# Basic Use of Flow

## Introduction
Flow is a static type checker for javascript code using static type annotations.

* **Package Manager** - `Yarn`
* **Compiler** - `Babel-cli`

## Setup Compiler

Babel is a compiler for JavaScript code that has support for Flow. Babel will take your Flow code and strip out any type annotations.

1. First install babel-cli and babel-preset-flow with either Yarn or npm, I am using yarn.
	> yarn add --dev babel-cli babel-preset-flow

2. Create a `.babelrc` file at the root of your folder with "flow" in your "presets".
	```
	{
	  "presets": ["flow"]
	}
	```
	> Presets are collections of plugins used to support particular language features.

## Compile the code using babel

If your all source of code is in `src` directory and you wish to compile them into another directore `build`
> yarn run babel src/ -d build/

Or you can add this to your `package.json` script

	```
	{
	  "name": "flow-basic",
	  "scripts": {
	  	"build": "yarn run babel src/ -- -d build/"
	  }
	}
	```

> Note: You’ll probably want to add a `prepublish` script that runs this transform as well, so that it runs before you publish your code.

## Setup Flow

1. Add a devDependency on the flow-bin
	> yarn add --dev flow-bin
2. Init the flow
	> yarn run flow init

	This creates an empty file `.flowconfig`, tells the Flow background process the root of where to begin checking Flow code for errors.

3. Run FLow
> yarn run flow

## Prepare your code for Flow
1. Adding flag `// flow` in your javascript file.
2. Run `flow` or `flow status`. This strats the background process which monitors all Flow files.
3. Write the flow code
	```
	// @flow
	function foo(x: ?number): string {
		if (x) {
			return x;
		}
		return "Default string";
	}
	```

## How to configure Flow
You can configure Flow by modifying `.flowconfig`.

The `.flowconfig` consists of 7 sections.

### [declarations]

The [declarations] section in a .flowconfig file tells Flow to parse files matching the specified regular expressions in declaration mode.Declaration mode should only be used for existing third-party code. You should never use this for code under your control.

```
[declarations]
.*/third_party/.*. # Any file or directory under a directory named third_party
<PROJECT_ROOT>/third_party/.* # any file or directory under the directory named third_party/ within the project root
```

### [include]
This section tells Flow to include the specified files or directories.

```
[include]
../externalFile.js
```

### [ignore]
This section tells Flow to ignore files matching the specified regular expressions when type checking your code. By default, nothing is ignored.

```
[ignore]
.*/__test__/.*. # Any file or directory under a directory named __tests__
<PROJECT_ROOT>/__tests__/.* # ignore any file or directory under the directory named __tests__/ within the project root. 
```

### [untyped]
tells Flow to not typecheck files matching the specified regular expressions and instead throw away types and treat modules as any. This is different from the [ignore] config section that causes matching files to be ignored by the module resolver, which inherently makes them un-typechecked, and also unresolvable by import or require. When ignored [libs] must then be specified for each import using flow-typed, which may not always be desired.

It is also different from the [declarations] section. This also does not typecheck the file contents, but [declarations] does extract and use the signatures of functions, classes, etc, when checking other code.

[untyped] instead causes a file to be ignored by the typechecker as if it had noflow in it, resolve modules as any typ, but allow them to NOT be ignored by the module resolver. Any matching file is skipped by Flow (not even parsed, like other noflow files!), but can still be require()‘d.

### [libs]
The [libs] section in a .flowconfig file tells Flow to include the specified library definitions when type checking your code.

### [lints]
can contain several key-value pairs of the form:

```
[lints]
ruleA=severityA
```

### [version]
You can specify in the .flowconfig which version of Flow you expect to use



