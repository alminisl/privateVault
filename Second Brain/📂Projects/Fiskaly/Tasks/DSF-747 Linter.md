

Find a linter configuration for us which includes VSCode + Other editors if possible. Try to see if this will work on both but also discuss which rules should be and which should not be included. 

### List of linting rules

- https://typescript-eslint.io/getting-started
- https://typescript-eslint.io/rules/naming-convention/
	- This is something we need to discuss and update the code base. 
- https://typescript-eslint.io/rules/adjacent-overload-signatures/
	- Function overload signatures represent multiple ways a function can be called, potentially with different return types. It's typical for an interface or type alias describing a function to place all overload signatures next to each other. 
- https://typescript-eslint.io/rules/array-type/
	- TypeScript provides two equivalent ways to define an array type: `T[]` and `Array<T>`. The two styles are functionally equivalent. Using the same style consistently across your codebase makes it easier for developers to read and understand array types.
- https://typescript-eslint.io/rules/consistent-type-assertions/
	- TypeScript provides two syntaxes for "type assertions":

		- Angle brackets: `<Type>value`
		- As: `value as Type`

		This rule aims to standardize the use of type assertion style across the codebase. Keeping to one syntax consistently helps with code readability.
- https://typescript-eslint.io/rules/consistent-type-imports/
	- TypeScript allows specifying a `type` keyword on imports to indicate that the export exists only in the type system, not at runtime. This allows transpilers to drop imports without knowing the types of the dependencies.
- https://typescript-eslint.io/rules/explicit-function-return-type/
	- Functions in TypeScript often don't need to be given an explicit return type annotation. Leaving off the return type is less code to read or write and allows the compiler to infer it from the contents of the function.
	
	However, explicit return types do make it visually more clear what type is returned by a function. They can also speed up TypeScript type checking performance in large codebases with many large functions.
	
	This rule enforces that functions do have an explicit return type annotation. 
- https://typescript-eslint.io/rules/explicit-module-boundary-types/#examples
	- Explicit types for function return values and arguments makes it clear to any calling code what is the module boundary's input and output. Adding explicit type annotations for those types can help improve code readability. It can also improve TypeScript type checking performance on larger codebases.
- https://typescript-eslint.io/rules/member-ordering/
	- This rule aims to standardize the way classes, interfaces, and type literals are structured and ordered. A consistent ordering of fields, methods and constructors can make code easier to read, navigate, and edit. Personally would really like this to be included
- https://typescript-eslint.io/rules/no-empty-interface/ ? 
	- Not sure if we need this one, as I did not see empty interfaces that we used or do we care about it?
- https://typescript-eslint.io/rules/no-misused-promises/
	- This rule forbids providing Promises to logical locations such as if statements in places where the TypeScript compiler allows them but they are not handled properly. These situations can often arise due to a missing `await` keyword or just a misunderstanding of the way async functions are handled/awaited.
- https://typescript-eslint.io/rules/prefer-optional-chain/
	- This is just a nice to have probably nothing major
- https://typescript-eslint.io/rules/sort-type-constituents/
	- Same as member-ordering this one sorts some of the types and union types
- https://typescript-eslint.io/rules/explicit-function-return-type
	- This one I also really like to know what the return type of a function is. However, If we want to use this one we should just use it as a warning at and maybe sometimes later switch it to Erroring. 


Argument all the rules and write a PR for it. Set the rules to Warnings to not break anything and see what the colleagues think about it. 

### Prettier 

https://prettier.io/docs/en/options.html 

