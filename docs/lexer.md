# First and foremost

a quick overview of handlebar syntax
  * https://gist.github.com/nessthehero/4ea763350fc93100f002
  * https://handlebarsjs.com/guide/partials.html#partial-contexts
  * https://handlebarsjs.com/guide/expressions.html?#path-expressions
  * https://handlebarsjs.com/guide/partials.html#dynamic-partials


---

# ANTLR lexer syntax (be sure to familiar yoursef with ENBF notation)
lexer located at `handlebars/src/main/antlr4/com/github/jknack/handlebars/internal/HbsLexer.g4`, it is written using antlr syntax.

* ! https://github.com/antlr/antlr4/blob/master/doc/lexer-rules.md
* https://www.antlr2.org/doc/metalang.html


<br/><br/>



## Rule
<br/><br/>
### Programmatic Rule
are rules defined using code, not ENBF syntax. the keypart is to call `getInterpreter().setCharPositionInLine` function to mark matched words.

```
COMMENT
  : {comment(start, end)}? .
  ;
```

this rule basically try every char `.` until finds a pattern `{{!-- --}}`


<br/><br/>

### static Rule

<br/>

### the `|` in lexer grammar


```
ID_SEPARATOR
  : ('.'|'/'|'-');             // OR rule has to be enclosed in parenthesis, or it would be in conflicts with lexer Rule grammar


RULE                            // this is lexer Rule grammar
    :
        PATTEN_A
    |   PATTEN_B
    ;
```


<br/>

###  fragment rules 
> These fragment rules do not result in tokens visible to the parser:

only `INT ` non-terminal can be returned.

```
INT : DIGIT+ ; // references the DIGIT helper rule
fragment DIGIT : [0-9] ; // not a token by itself
```



<br/>

### notes for each rule


* ID_ESCAPE:  
this would match text with regex pattern `\.[ ([^\])* ]` , like `[0]` part in string `a.[0]`.





* ID:  
  * match 
    * string starts with `{character}`, followed with `.[.*]` or `{number}` or `{char}` or `-`.
    * string starts with `.[.*]` , followed with `.[.*]` or `{number}` or `{char}` or `-`.

* SINGLE_STRING

```
SINGLE_STRING  :
    '\'' ( '\\\'' | . )*? '\''
  ;

```

matchs a single quoted string starts with `'`, followed with zero or one more  `\'` or any ` {char}`, then end with `'`

<br/>

* END_RAW, START_RAW: 
  * https://handlebarsjs.com/guide/block-helpers.html?#raw-blocks
```
{{{{raw-loud}}}}
  {{bar}}
{{{{/raw-loud}}}}
```

would render 

```
  {{bar}}
```


<br/>

* START_DELIM, END_DELIM: 

match `{{=` and `=}}`

I guess this is also some deprecated feature of handlebar

<br/>

* START_BLOCK

block helper starts with `{{#`, https://handlebarsjs.com/guide/#block-helpers


<br/>

* START_PARTIAL_BLOCK: 
if target partial not found, would render a fallback.

```
{{#> myPartial }}
  Failover content
{{/myPartial}}
```

would render, if `myPartial` not found.
```
Failover content
```
https://handlebarsjs.com/guide/partials.html#partial-blocks

<br/>

* UNLESS
shorthand for `else`

```
{{#each nav}}
  <a href="{{url}}">
    {{#if test}}
      {{title}}
    {{^}}
      Empty
    {{/if}}
  </a>
{{~/each}}
```

* START_AMP
??
