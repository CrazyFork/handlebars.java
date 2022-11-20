
# Personal Notes

* a quick overview of handlebar syntax -  https://gist.github.com/nessthehero/4ea763350fc93100f002



todos:
* create a blog for antlr
* context 
* how parser is used
   * handlebars/src/main/java/com/github/jknack/handlebars/Handlebars.java, precompile hbs file to js function
   * 
* java ScriptEngine and js parser 
* https://plaid.com/blog/handlebars-to-react-migration/
* https://github.com/glimmerjs/glimmer-vm
* https://github.com/danakt/handlebars-to-jsx


## ANTLR

* intellij plugin - https://www.youtube.com/watch?v=0A2-BquvxMU&t=2s&ab_channel=ProfessorParr
* vscode plugin -
    * lexer visualization - https://github.com/mike-lischke/vscode-antlr4/blob/HEAD/doc/graphical-visualizations.md

## Lexer

[See lexer notes](./docs/lexer.md)


## Parser

[See parser notes](./docs/parser.md)
## java

* usage of `Class<T>` type.



* check Object type in runtime 


## files

```
handlebars/src/main/java/com/github/jknack/handlebars/
├── Context.java
├── Decorator.java
├── EscapingStrategy.java
├── Formatter.java
├── Handlebars.java                                    # used as core facade for most of lib's capabilities
├── HandlebarsError.java
├── HandlebarsException.java
├── Helper.java
├── HelperRegistry.java
├── Lambda.java
├── Options.java
├── Parser.java
├── ParserFactory.java
├── PathCompiler.java                                   #
├── PathExpression.java                                 # 
├── TagType.java                                        # all the possible `{{` syntax.
├── Template.java
├── TypeSafeTemplate.java
├── ValueResolver.java                                  # how to resolve value by name/key
├── cache
│   ├── ConcurrentMapTemplateCache.java
│   ├── HighConcurrencyTemplateCache.java
│   ├── NullTemplateCache.java
│   └── TemplateCache.java
├── context                                              # !!
│   ├── FieldValueResolver.java
│   ├── JavaBeanValueResolver.java
│   ├── MapValueResolver.java
│   ├── MemberValueResolver.java
│   └── MethodValueResolver.java
├── helper
│   ├── BlockHelper.java
│   ├── IfHelper.java
│   └── WithHelper.java
├── internal
│   ├── BaseTemplate.java
│   ├── Block.java
│   ├── BlockDecorator.java
│   ├── DefParam.java
│   ├── FastStringWriter.java
│   ├── Files.java
│   ├── FormatterChain.java
│   ├── ForwardingTemplate.java
│   ├── HbsErrorReporter.java
│   ├── HbsErrorStrategy.java
│   ├── HbsParserFactory.java
│   ├── HelperResolver.java
│   ├── Lambdas.java
│   ├── Locales.java
│   ├── MustacheSpec.java
│   ├── MustacheStringUtils.java
│   ├── Param.java
│   ├── Partial.java
│   ├── PartialBlockForwardingTemplate.java
│   ├── PathExpressionList.java
│   ├── RefParam.java
│   ├── StrParam.java
│   ├── TemplateBuilder.java
│   ├── TemplateList.java
│   ├── Text.java
│   ├── Throwing.java
│   ├── VarDecorator.java
│   ├── VarParam.java
│   ├── Variable.java
│   ├── WhiteSpaceControl.java
│   └── path                                                   
│       ├── DataPath.java
│       ├── IndexedPath.java
│       ├── ParentPath.java
│       ├── PropertyPath.java
│       ├── ResolveParentPath.java
│       ├── ResolveThisPath.java
│       └── ThisPath.java
└── io
    ├── AbstractTemplateLoader.java
    ├── AbstractTemplateSource.java
    ├── ClassPathTemplateLoader.java
    ├── CompositeTemplateLoader.java
    ├── FileTemplateLoader.java
    ├── ForwardingTemplateSource.java
    ├── ReloadableTemplateSource.java
    ├── ServletContextTemplateLoader.java
    ├── StringTemplateSource.java
    ├── TemplateLoader.java
    ├── TemplateSource.java
    ├── URLTemplateLoader.java
    └── URLTemplateSource.java

```









## [original readme](./README.original.md)