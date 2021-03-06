# Context

<small>**assembly:** Peachpie.Runtime.dll</small>

`Context` maintains the PHP application's state. It is usually associated with a single web request, a thread or a console application. In short, the context remembers the declared types and functions, global variables, 'static' locals, properties and included scripts. The context also provides information about the environment, services and local configuration.

It is important to note that the context instance is required by the compiled PHP routines and by class constructors. Additionally library functions may require the context instance in order to work properly.

## Construction

A new instance of the object is created in two ways:

- **Implicitly by the framework:** The appropriate context is created for a web application during its request handling routine. Its instance is then passed to PHP routines and to handlers during the request life cycle implicitly.
- **Explicitly by instantiating it:** It is possible to create an instance of a default context and use it in order to drive a custom PHP application's state. A new instance of the default context can be created by the static method below:
    * `#!c# Context.CreateEmpty()`

## Methods

Method | Summary
---    | ---
AddScriptReference(Assembly) | Loads declarations from given [compiled assembly](../assembly/compiled-assembly). *(app static)*
Call(string, [PhpValue](phpvalue)[] args) : [PhpValue](phpvalue) | Dynamically invokes a function declared within the current context.
Create(string, [PhpValue](phpvalue)[] args) : object | Dynamically instantiates a class declared within the current context.
DeclareFunction(string, Delegate) | Dynamically declares a global function within the current context.
DeclareScript(string, MainDelegate) | Adds or overwrites a script descriptor by its relative file path. *(app static)*
DeclareType&lt;T&gt;() | Dynamically declares a CLR type into the current context.
DefineConstant(string, [PhpValue](phpvalue)) | Defines a global constant within the current context.
GetDeclaredFunctions() : IEnumerable&lt;RoutineInfo&gt; | Enumerates global functions declared within the current context.
GetDeclaredType(string) : PhpTypeInfo | Gets type descriptor representing a type declared within the current context. Optionally performs autoload process if necessary.
GetDeclaredTypes() : IEnumerable&lt;PhpTypeInfo&gt; | Enumerates types declared within the current context.
GetIncludedScripts() : IEnumerable&lt;ScriptInfo&gt; | Enumerates script descriptors representing script files that were included within the current context.
TryGetConstant(string, out [PhpValue](phpvalue)) : bool | Gets a global constant value defined within the current context.
Dispose() | Ends the life cycle of the context and disposes associated resources.

## Helper methods

In case of an ASP.NET Core application, the instance can be obtained using a helper method: `#!c# GetOrCreateContext(this HttpContext) : Context`

## Properties

Property | Summary
---      | ---
RootPath : string | An absolute directory path representing the root of all the scripts. Full script paths are resolved as a combination of this path and relative script path.
StringEncoding : Encoding | The encoding used to perform encoding and decoding between byte[] and string. Used for scripts output (echo), and internal string encoding. Default and recommended value is `UTF-8`.
HttpPhpContext : IHttpPhpContext | Gets instance of an interface providing web application APIs. Gets `null` reference for non-web applications.
Output : TextWriter | Gets the output stream used for `echo` and other output routines.
Globals : [PhpArray](phparray) | Gets or sets an array representing PHP's `$GLOBALS`.
Server : [PhpArray](phparray) | Gets or sets an array representing PHP's `$_SERVER`.
Session : [PhpArray](phparray) | Gets or sets an array representing PHP's `$_SESSION`.
Cookie : [PhpArray](phparray) | Gets or sets an array representing PHP's `$_COOKIE`.
Get : [PhpArray](phparray) | Gets or sets an array representing PHP's `$_GET`.
Post : [PhpArray](phparray) | Gets or sets an array representing PHP's `$_POST`.
Request : [PhpArray](phparray) | Gets or sets an array representing PHP's `$_REQUEST`.

## Notes

## Samples

## Related links
