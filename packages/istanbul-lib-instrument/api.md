<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [createInstrumenter][1]
    -   [Parameters][2]
-   [Instrumenter][3]
    -   [Parameters][4]
    -   [instrumentSync][5]
        -   [Parameters][6]
    -   [instrument][7]
        -   [Parameters][8]
    -   [lastFileCoverage][9]
    -   [lastSourceMap][10]
-   [programVisitor][11]
    -   [Parameters][12]

## createInstrumenter

createInstrumenter creates a new instrumenter with the
supplied options.

### Parameters

-   `opts` **[Object][13]** instrumenter options. See the documentation
    for the Instrumenter class.

## Instrumenter

Instrumenter is the public API for the instrument library.
It is typically used for ES5 code. For ES6 code that you
are already running under `babel` use the coverage plugin
instead.

### Parameters

-   `opts` **[Object][13]** optional. (optional, default `{}`)
    -   `opts.coverageVariable` **[string][14]** name of global coverage variable. (optional, default `__coverage__`)
    -   `opts.reportLogic` **[boolean][15]** report boolean value of logical expressions. (optional, default `false`)
    -   `opts.preserveComments` **[boolean][15]** preserve comments in output. (optional, default `false`)
    -   `opts.compact` **[boolean][15]** generate compact code. (optional, default `true`)
    -   `opts.esModules` **[boolean][15]** set to true to instrument ES6 modules. (optional, default `false`)
    -   `opts.autoWrap` **[boolean][15]** set to true to allow `return` statements outside of functions. (optional, default `false`)
    -   `opts.produceSourceMap` **[boolean][15]** set to true to produce a source map for the instrumented code. (optional, default `false`)
    -   `opts.ignoreClassMethods` **[Array][16]** set to array of class method names to ignore for coverage. (optional, default `[]`)
    -   `opts.sourceMapUrlCallback` **[Function][17]** a callback function that is called when a source map URL.
            is found in the original code. This function is called with the source file name and the source map URL. (optional, default `null`)
    -   `opts.debug` **[boolean][15]** turn debugging on. (optional, default `false`)
    -   `opts.parserPlugins` **[array][16]?** set babel parser plugins, see @istanbuljs/schema for defaults.
    -   `opts.coverageGlobalScope` **[string][14]** the global coverage variable scope. (optional, default `this`)
    -   `opts.coverageGlobalScopeFunc` **[boolean][15]** use an evaluated function to find coverageGlobalScope. (optional, default `true`)

### instrumentSync

instrument the supplied code and track coverage against the supplied
filename. It throws if invalid code is passed to it. ES5 and ES6 syntax
is supported. To instrument ES6 modules, make sure that you set the
`esModules` property to `true` when creating the instrumenter.

#### Parameters

-   `code` **[string][14]** the code to instrument
-   `filename` **[string][14]** the filename against which to track coverage.
-   `inputSourceMap` **[object][13]?** the source map that maps the not instrumented code back to it's original form.
    Is assigned to the coverage object and therefore, is available in the json output and can be used to remap the
    coverage to the untranspiled source.

Returns **[string][14]** the instrumented code.

### instrument

callback-style instrument method that calls back with an error
as opposed to throwing one. Note that in the current implementation,
the callback will be called in the same process tick and is not asynchronous.

#### Parameters

-   `code` **[string][14]** the code to instrument
-   `filename` **[string][14]** the filename against which to track coverage.
-   `callback` **[Function][17]** the callback
-   `inputSourceMap` **[Object][13]** the source map that maps the not instrumented code back to it's original form.
    Is assigned to the coverage object and therefore, is available in the json output and can be used to remap the
    coverage to the untranspiled source.

### lastFileCoverage

returns the file coverage object for the last file instrumented.

Returns **[Object][13]** the file coverage object.

### lastSourceMap

returns the source map produced for the last file instrumented.

Returns **(null | [Object][13])** the source map object.

## programVisitor

programVisitor is a `babel` adaptor for instrumentation.
It returns an object with two methods `enter` and `exit`.
These should be assigned to or called from `Program` entry and exit functions
in a babel visitor.
These functions do not make assumptions about the state set by Babel and thus
can be used in a context other than a Babel plugin.

The exit function returns an object that currently has the following keys:

`fileCoverage` - the file coverage object created for the source file.
`sourceMappingURL` - any source mapping URL found when processing the file.

### Parameters

-   `types` **[Object][13]** an instance of babel-types.
-   `sourceFilePath` **[string][14]** the path to source file. (optional, default `'unknown.js'`)
-   `opts` **[Object][13]** additional options. (optional, default `{}`)
    -   `opts.coverageVariable` **[string][14]** the global coverage variable name. (optional, default `__coverage__`)
    -   `opts.reportLogic` **[boolean][15]** report boolean value of logical expressions. (optional, default `false`)
    -   `opts.coverageGlobalScope` **[string][14]** the global coverage variable scope. (optional, default `this`)
    -   `opts.coverageGlobalScopeFunc` **[boolean][15]** use an evaluated function to find coverageGlobalScope. (optional, default `true`)
    -   `opts.ignoreClassMethods` **[Array][16]** names of methods to ignore by default on classes. (optional, default `[]`)
    -   `opts.inputSourceMap` **[object][13]** the input source map, that maps the uninstrumented code back to the
        original code. (optional, default `undefined`)

[1]: #createinstrumenter

[2]: #parameters

[3]: #instrumenter

[4]: #parameters-1

[5]: #instrumentsync

[6]: #parameters-2

[7]: #instrument

[8]: #parameters-3

[9]: #lastfilecoverage

[10]: #lastsourcemap

[11]: #programvisitor

[12]: #parameters-4

[13]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[14]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[15]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[16]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array

[17]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function
