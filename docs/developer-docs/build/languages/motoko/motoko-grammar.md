# Motoko grammar

This section describes the concrete syntax, or grammar, of Motoko. The specification is auto-generated with a tool.

``` bnf
<list(X, SEP)> ::=
    <empty>
    X
    X SEP <list(X, SEP)>

<list1(X, SEP)> ::=
    X
    X SEP <list(X, SEP)>

<obj_sort> ::=
    'object'
    'actor'
    'module'

<func_sort_opt> ::=
    <empty>
    'shared' 'query'?
    'query'

<shared_pat_opt> ::=
    <empty>
    'shared' 'query'? <pat_plain>?
    'query' <pat_plain>?

<typ_obj> ::=
    '{' <list(<typ_field>, ';')> '}'

<typ_variant> ::=
    '{' '#' '}'
    '{' <list1(<typ_tag>, ';')> '}'

<typ_nullary> ::=
    '(' <list(<typ_item>, ',')> ')'
    <id> ('.' <id>)* <typ_args>?
    '[' 'var'? <typ> ']'
    <typ_obj>
    <typ_variant>

<typ_un> ::=
    <typ_nullary>
    '?' <typ_un>

<typ_pre> ::=
    <typ_un>
    'async' <typ_pre>
    <obj_sort> <typ_obj>

<typ_nobin> ::=
    <typ_pre>
    <func_sort_opt> ('<' <list(<typ_bind>, ',')> '>')? <typ_un> '->' <typ_nobin>

<typ> ::=
    <typ_nobin>
    <typ> 'and' <typ>
    <typ> 'or' <typ>

<typ_item> ::=
    <id> ':' <typ>
    <typ>

<typ_args> ::=
    '<' <list(<typ>, ',')> '>'

<typ_field> ::=
    'var'? <id> ':' <typ>
    <id> ('<' <list(<typ_bind>, ',')> '>')? <typ_nullary> ':' <typ>

<typ_tag> ::=
    '#' <id> (':' <typ>)?

<typ_bind> ::=
    <id> '<:' <typ>
    <id>

<lit> ::=
    'null'
    <bool>
    <nat>
    <float>
    <char>
    <text>

<unop> ::=
    '+'
    '-'
    '^'

<binop> ::=
    '+'
    '-'
    '*'
    '/'
    '%'
    '**'
    '+%'
    '-%'
    '*%'
    '**%'
    '&'
    '|'
    '^'
    '<<'
    ' >>'
    '<<>'
    '<>>'
    '#'

<relop> ::=
    '=='
    '!='
    ' < '
    '<='
    ' > '
    '>='

<unassign> ::=
    '+='
    '-='
    '^='

<binassign> ::=
    '+='
    '-='
    '*='
    '/='
    '%='
    '**-'
    '+%='
    '-%='
    '*%='
    '**%='
    '&='
    '|='
    '^='
    '<<='
    '>>='
    '<<>='
    '<>>='
    '@='

<exp_obj> ::=
    '{' <list(<exp_field>, ';')> '}'

<exp_plain> ::=
    <lit>
    '(' <list(<exp>, ',')> ')'

<exp_nullary> ::=
    <exp_obj>
    <exp_plain>
    <id>

<exp_post> ::=
    <exp_nullary>
    '[' 'var'? <list(<exp_nonvar>, ',')> ']'
    <exp_post> '[' <exp> ']'
    <exp_post> '.'<nat>
    <exp_post> '.' <id>
    <exp_post> ('<' <list(<typ>, ',')> '>')? <exp_nullary>
    <exp_post> BANG

<exp_un> ::=
    <exp_post>
    '#' <id>
    '#' <id> <exp_nullary>
    '?' <exp_un>
    <unop> <exp_un>
    <unassign> <exp_un>
    'actor' <exp_plain>
    'not' <exp_un>
    'debug_show' <exp_un>
    'to_candid' '(' <list(<exp>, ',')> ')'
    'from_candid' <exp_un>

<exp_bin> ::=
    <exp_un>
    <exp_bin> <binop> <exp_bin>
    <exp_bin> <relop> <exp_bin>
    <exp_bin> 'and' <exp_bin>
    <exp_bin> 'or' <exp_bin>
    <exp_bin> ':' <typ_nobin>

<exp_nondec> ::=
    <exp_bin>
    <exp_bin> ':=' <exp>
    <exp_bin> <binassign> <exp>
    'return' <exp>?
    'async' <exp_nest>
    'await' <exp_nest>
    'assert' <exp_nest>
    'label' <id> (':' <typ>)? <exp_nest>
    'break' <id> <exp_nullary>?
    'continue' <id>
    'debug' <exp_nest>
    'if' <exp_nullary> <exp_nest>
    'if' <exp_nullary> <exp_nest> 'else' <exp_nest>
    'try' <exp_nest> <catch>
    'throw' <exp_nest>
    'switch' <exp_nullary> '{' <list(<case>, ';')> '}'
    'while' <exp_nullary> <exp_nest>
    'loop' <exp_nest>
    'loop' <exp_nest> 'while' <exp_nest>
    'for' '(' <pat> 'in' <exp> ')' <exp_nest>
    'ignore' <exp_nest>
    'do' <block>
    'do' '?' <block>

<exp_nonvar> ::=
    <exp_nondec>
    <dec_nonvar>

<exp> ::=
    <exp_nonvar>
    <dec_var>

<exp_nest> ::=
    <block>
    <exp>

<block> ::=
    '{' <list(<dec>, ';')> '}'

<case> ::=
    'case' <pat_nullary> <exp_nest>

<catch> ::=
    'catch' <pat_nullary> <exp_nest>

<exp_field> ::=
    'var'? <id> (':' <typ>)?
    'var'? <id> (':' <typ>)? '=' <exp>

<dec_field> ::=
    <vis> <stab> <dec>

<vis> ::=
    <empty>
    'private'
    'public'
    'system'

<stab> ::=
    <empty>
    'flexible'
    'stable'

<pat_plain> ::=
    '_'
    <id>
    <lit>
    '(' <list(<pat_bin>, ',')> ')'

<pat_nullary> ::=
    <pat_plain>
    '{' <list(<pat_field>, ';')> '}'

<pat_un> ::=
    <pat_nullary>
    '#' <id>
    '#' <id> <pat_nullary>
    '?' <pat_un>
    <unop> <lit>

<pat_bin> ::=
    <pat_un>
    <pat_bin> 'or' <pat_bin>
    <pat_bin> ':' <typ>

<pat> ::=
    <pat_bin>

<pat_field> ::=
    <id> (':' <typ>)?
    <id> (':' <typ>)? '=' <pat>

<dec_var> ::=
    'var' <id> (':' <typ>)? '=' <exp>

<dec_nonvar> ::=
    'let' <pat> '=' <exp>
    'type' <id> ('<' <list(<typ_bind>, ',')> '>')? '=' <typ>
    <obj_sort> <id>? '='? <obj_body>
    <shared_pat_opt> 'func' <id>? ('<' <list(<typ_bind>, ',')> '>')? <pat_plain> (':' <typ>)? <func_body>
    <shared_pat_opt> <obj_sort>? 'class' <id>? ('<' <list(<typ_bind>, ',')> '>')? <pat_plain> (':' <typ>)? <class_body>

<dec> ::=
    <dec_var>
    <dec_nonvar>
    <exp_nondec>

<func_body> ::=
    '=' <exp>
    <block>

<obj_body> ::=
    '{' <list(<dec_field>, ';')> '}'

<class_body> ::=
    '=' <id>? <obj_body>
    <obj_body>

<imp> ::=
    'import' <pat_nullary> '='? <text>

<prog> ::=
    <list(<imp>, ';')> <list(<dec>, ';')>
```
