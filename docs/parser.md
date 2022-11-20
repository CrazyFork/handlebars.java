

# Parser


## handlebar
* decorator - https://handlebarsjs.com/guide/partials.html#inline-partials


## ANTLR parser syntax  (be sure to familiar yoursef with ENBF notation)
* https://github.com/antlr/antlr4/blob/master/doc/parser-rules.md

## notes for each rule

* test cases - handlebars/src/test/java/com/github/jknack/handlebars/internal/HbsParserTest.java


// copied from file: handlebars/src/main/antlr4/com/github/jknack/handlebars/internal/HbsParser.g4
```

template
  : body EOF
  ;

body
  : statement*
  ;

statement
  :
    text
  | block
  | var
  | tvar
  | ampvar
  | unless
  | partial
  | partialBlock
  | rawBlock
  | escape
  | comment
  | delimiters
  ;

escape
  :
    ESC_VAR
  ;

text
  :
    TEXT
  ;

block
  :
    startToken = START_BLOCK DECORATOR? sexpr blockParams? END
    thenBody=body
    elseBlock*
    END_BLOCK nameEnd=QID END
  ;

rawBlock
  :
    startToken = START_RAW sexpr END_RAW
    thenBody=body
    END_RAW_BLOCK nameEnd=QID END_RAW
  ;

// {{#each people as |person|}}
// ...
// {{/each}}
blockParams
  :
    AS PIPE QID+ PIPE
  ;

sexpr
  :
    QID param* hash*
  ;

elseBlock
  :
    elseStmt
  | elseStmtChain
  ;

elseStmt
  :
    (inverseToken=UNLESS | START inverseToken=ELSE) END unlessBody=body
  ;

// {{else condtion}} body
// {{^}} body
elseStmtChain
  :
    (inverseToken=UNLESS | START inverseToken=ELSE) sexpr blockParams? END unlessBody=body
  ;

unless
  :
    UNLESS sexpr blockParams? END
    body
    END_BLOCK nameEnd=QID END
  ;

// match  {{{ }}}
tvar
  :
   START_T sexpr END_T
  ;

// match  {{& }}
ampvar
  :
   START_AMP sexpr END
  ;

// match  {{ }}
var
  :
   START DECORATOR? sexpr END
  ;

delimiters
  :
    START_DELIM
    WS_DELIM*
    startDelim+=DELIM+
      {setStart(join($startDelim));}
    WS_DELIM+
    endDelim+=DELIM+
    WS_DELIM*
    END_DELIM
    {setEnd(join($endDelim));}
  ;

partial
  :
    START_PARTIAL pexpr END
  ;

partialBlock
  :
    START_PARTIAL_BLOCK pexpr END
    thenBody=body
    END_BLOCK nameEnd=QID END
  ;

pexpr
  :
    LP sexpr RP QID? hash*                            #dynamicPath
  | path = (QID|PATH) QID? hash*                      #staticPath
  | path = (DOUBLE_STRING | SINGLE_STRING) QID? hash* #literalPath
  ;

param
  :
    DOUBLE_STRING #stringParam
  | SINGLE_STRING #charParam
  | NUMBER           #numberParam
  | BOOLEAN       #boolParam
  | QID           #refParam
  | LP sexpr RP   #subParamExpr
  ;

hash
  :
    QID EQ param
  ;

comment
  : COMMENT;
```