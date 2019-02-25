#Basic Use of Flow**

##Introduction
Flow is a static type checker for your javascript code using static type annotations

*Package Manager*
Yarn
*Compiler*
Babel-cli

**Setup Compiler**
Babel is a compiler for JavaScript code that has support for Flow. Babel will take your Flow code and strip out any type annotations.

1. First install babel-cli and babel-preset-flow with either Yarn 
	> yarn add --dev babel-cli babel-preset-flow

2. Create a `.babelrc` file at the root of your folder with "flow" in your "presets".
	```
	{
	  "presets": ["flow"]
	}
	```
	> Presets are collections of pluginsused to support particular language features.

**Compile the code using babel**
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

**Setup Flow**

1. Add a devDependency on the flow-bin
> yarn add --dev flow-bin
2. Init the flow
> yarn run flow init
This creates an empty file `.flowconfig`, tells the Flow background process the root of where to begin checking Flow code for errors.
3. Run FLow
> yarn run flow

**Prepare your code for Flow**
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
