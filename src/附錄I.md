# Appendix I 附錄I

> Here is a complete grammar for Lox. The chapters that introduce each part of the language include the grammar rules there, but this collects them all into one place.

這裏有一份Lox的完整語法。介紹語言每個部分的章節中都包含對應的語法規則，但這裏將它們全部收錄在一起了。

> ## A1 . 1 Syntax Grammar

## A1.1 語法

> The syntactic grammar is used to parse the linear sequence of tokens into the nested syntax tree structure. It starts with the first rule that matches an entire Lox program (or a single REPL entry).

語法用於將詞法標識（token）的線性序列解析為嵌套的語法樹結構。它從匹配整個Lox程序（或單條REPL輸入）的第一個規則開始。

```
program        → declaration* EOF ;
```

> ### A1 . 1 . 1 Declarations

### A1.1.1 聲明

> A program is a series of declarations, which are the statements that bind new identifiers or any of the other statement types.

一個程序就是一系列的聲明，也就是綁定新標識符或其它statement類型的語句。

```
declaration    → classDecl
               | funDecl
               | varDecl
               | statement ;

classDecl      → "class" IDENTIFIER ( "<" IDENTIFIER )?
                 "{" function* "}" ;
funDecl        → "fun" function ;
varDecl        → "var" IDENTIFIER ( "=" expression )? ";" ;
```

> ### A1 . 1 . 2 Statements

### A1.1.2 語句

> The remaining statement rules produce side effects, but do not introduce bindings.

其餘的語句規則會產生副作用，但不會引入綁定。

```
statement      → exprStmt
               | forStmt
               | ifStmt
               | printStmt
               | returnStmt
               | whileStmt
               | block ;

exprStmt       → expression ";" ;
forStmt        → "for" "(" ( varDecl | exprStmt | ";" )
                           expression? ";"
                           expression? ")" statement ;
ifStmt         → "if" "(" expression ")" statement
                 ( "else" statement )? ;
printStmt      → "print" expression ";" ;
returnStmt     → "return" expression? ";" ;
whileStmt      → "while" "(" expression ")" statement ;
block          → "{" declaration* "}" ;
```

> Note that `block` is a statement rule, but is also used as a nonterminal in a couple of other rules for things like function bodies.

請注意，`block`是一個語句規則，但在其它規則中也作為非終止符使用，用於表示函數體等內容。

> ### A1 . 1 . 3 Expressions

### A1.1.3 表達式

> Expressions produce values. Lox has a number of unary and binary operators with different levels of precedence. Some grammars for languages do not directly encode the precedence relationships and specify that elsewhere. Here, we use a separate rule for each precedence level to make it explicit.

表達式會產生值。Lox有許多具有不同優先級的一元或二元運算符。一些語言的語法中沒有直接編碼優先級關係，而是在其它地方指定。在這裏，我們為每個優先級使用單獨的規則，使其明確。

```
expression     → assignment ;

assignment     → ( call "." )? IDENTIFIER "=" assignment
               | logic_or ;

logic_or       → logic_and ( "or" logic_and )* ;
logic_and      → equality ( "and" equality )* ;
equality       → comparison ( ( "!=" | "==" ) comparison )* ;
comparison     → term ( ( ">" | ">=" | "<" | "<=" ) term )* ;
term           → factor ( ( "-" | "+" ) factor )* ;
factor         → unary ( ( "/" | "*" ) unary )* ;

unary          → ( "!" | "-" ) unary | call ;
call           → primary ( "(" arguments? ")" | "." IDENTIFIER )* ;
primary        → "true" | "false" | "nil" | "this"
               | NUMBER | STRING | IDENTIFIER | "(" expression ")"
               | "super" "." IDENTIFIER ;
```

> ### A1 . 1 . 4 Utility rules

### A1.1.4 實用規則

> In order to keep the above rules a little cleaner, some of the grammar is split out into a few reused helper rules.

為了使上面的規則更簡潔一點，一些語法被拆分為幾個重複使用的輔助規則。

```
function       → IDENTIFIER "(" parameters? ")" block ;
parameters     → IDENTIFIER ( "," IDENTIFIER )* ;
arguments      → expression ( "," expression )* ;
```

> ## A1 . 2 Lexical Grammar

## A1.2 詞法

> The lexical grammar is used by the scanner to group characters into tokens. Where the syntax is [context free](https://en.wikipedia.org/wiki/Context-free_grammar), the lexical grammar is [regular](https://en.wikipedia.org/wiki/Regular_grammar)—note that there are no recursive rules.

詞法被掃描器用來將字符分組為詞法標識（token）。語法是[上下文無關](https://en.wikipedia.org/wiki/Context-free_grammar)的，詞法是[正則](https://en.wikipedia.org/wiki/Regular_grammar)的——注意這裏沒有遞歸規則。

```
NUMBER         → DIGIT+ ( "." DIGIT+ )? ;
STRING         → "\"" <any char except "\"">* "\"" ;
IDENTIFIER     → ALPHA ( ALPHA | DIGIT )* ;
ALPHA          → "a" ... "z" | "A" ... "Z" | "_" ;
DIGIT          → "0" ... "9" ;
```