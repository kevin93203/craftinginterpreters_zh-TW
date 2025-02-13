# Appendix II 附錄II

> For your edification, here is the code produced by [the little script we built](http://www.craftinginterpreters.com/representing-code.html#metaprogramming-the-trees) to automate generating the syntax tree classes for jlox.

為了方便你們學習，下面是我們為自動生成jlox語法樹類而[構建的小腳本](http://www.craftinginterpreters.com/representing-code.html#metaprogramming-the-trees)所產生的代碼。

> ## A2 . 1 Expressions

## A2.1 表達式

> Expressions are the first syntax tree nodes we see, introduced in “[Representing Code](http://www.craftinginterpreters.com/representing-code.html)”. The main Expr class defines the visitor interface used to dispatch against the specific expression types, and contains the other expression subclasses as nested classes.

表達式是我們看到的第一個語法樹節點，在“表示代碼”中介紹過。主要的Expr類定義了用於針對特定表達式類型進行調度的訪問者接口，並將其它表達式子類作為嵌套類包含其中。

*<u>lox/Expr.java，創建新文件：</u>*

```c
package com.craftinginterpreters.lox;

import java.util.List;

abstract class Expr {
  interface Visitor<R> {
    R visitAssignExpr(Assign expr);
    R visitBinaryExpr(Binary expr);
    R visitCallExpr(Call expr);
    R visitGetExpr(Get expr);
    R visitGroupingExpr(Grouping expr);
    R visitLiteralExpr(Literal expr);
    R visitLogicalExpr(Logical expr);
    R visitSetExpr(Set expr);
    R visitSuperExpr(Super expr);
    R visitThisExpr(This expr);
    R visitUnaryExpr(Unary expr);
    R visitVariableExpr(Variable expr);
  }

  // Nested Expr classes here...

  abstract <R> R accept(Visitor<R> visitor);
}
```

### A2 . 1 . 1 Assign expression

> Variable assignment is introduced in “[Statements and State](http://www.craftinginterpreters.com/statements-and-state.html#assignment)”.

變量賦值在“表達式與狀態”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class Assign extends Expr {
    Assign(Token name, Expr value) {
      this.name = name;
      this.value = value;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitAssignExpr(this);
    }

    final Token name;
    final Expr value;
  }
```

> ### A2 . 1 . 2 Binary expression

### A2.1.2 Binary表達式

> Binary operators are introduced in “[Representing Code](http://www.craftinginterpreters.com/representing-code.html)”.

二元運算符在“表示代碼”中介紹過。

*<u>lox/Expr.java，嵌套在類Expr中：</u>*

```c
  static class Binary extends Expr {
    Binary(Expr left, Token operator, Expr right) {
      this.left = left;
      this.operator = operator;
      this.right = right;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitBinaryExpr(this);
    }

    final Expr left;
    final Token operator;
    final Expr right;
  }
```

### A2 . 1 . 3 Call expression

> Function call expressions are introduced in “[Functions](http://www.craftinginterpreters.com/functions.html#function-calls)”.

函數調用語句在“函數”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class Call extends Expr {
    Call(Expr callee, Token paren, List<Expr> arguments) {
      this.callee = callee;
      this.paren = paren;
      this.arguments = arguments;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitCallExpr(this);
    }

    final Expr callee;
    final Token paren;
    final List<Expr> arguments;
  }
```

### A2 . 1 . 4 Get expression

> Property access, or “get” expressions are introduced in “[Classes](http://www.craftinginterpreters.com/classes.html#properties-on-instances)”.

屬性訪問，或者説“get”表達式，在“類”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class Get extends Expr {
    Get(Expr object, Token name) {
      this.object = object;
      this.name = name;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitGetExpr(this);
    }

    final Expr object;
    final Token name;
  }
```

### A2 . 1 . 5 Grouping expression

> Using parentheses to group expressions is introduced in “[Representing Code](http://www.craftinginterpreters.com/representing-code.html)”.

使用括號進行分組的表達式在“表示代碼”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class Grouping extends Expr {
    Grouping(Expr expression) {
      this.expression = expression;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitGroupingExpr(this);
    }

    final Expr expression;
  }
```

### A2 . 1 . 6 Literal expression

> Literal value expressions are introduced in “[Representing Code](http://www.craftinginterpreters.com/representing-code.html)”.

字面量值表達式在“表示代碼”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class Literal extends Expr {
    Literal(Object value) {
      this.value = value;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitLiteralExpr(this);
    }

    final Object value;
  }
```

### A2 . 1 . 7 Logical expression

> The logical `and` and `or` operators are introduced in “[Control Flow](http://www.craftinginterpreters.com/control-flow.html#logical-operators)”.

邏輯運算符`and`和`or`在“控制流”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class Logical extends Expr {
    Logical(Expr left, Token operator, Expr right) {
      this.left = left;
      this.operator = operator;
      this.right = right;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitLogicalExpr(this);
    }

    final Expr left;
    final Token operator;
    final Expr right;
  }
```

### A2 . 1 . 8 Set expression

> Property assignment, or “set” expressions are introduced in “[Classes](http://www.craftinginterpreters.com/classes.html#properties-on-instances)”.

屬性賦值，或者叫“set”表達式，在“類”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class Set extends Expr {
    Set(Expr object, Token name, Expr value) {
      this.object = object;
      this.name = name;
      this.value = value;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitSetExpr(this);
    }

    final Expr object;
    final Token name;
    final Expr value;
  }
```

### A2 . 1 . 9 Super expression

> The `super` expression is introduced in “[Inheritance](http://www.craftinginterpreters.com/inheritance.html#calling-superclass-methods)”.

`super`表達式在“繼承”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class Super extends Expr {
    Super(Token keyword, Token method) {
      this.keyword = keyword;
      this.method = method;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitSuperExpr(this);
    }

    final Token keyword;
    final Token method;
  }
```

### A2 . 1 . 10 This expression

> The `this` expression is introduced in “[Classes](http://www.craftinginterpreters.com/classes.html#this)”.

`this`表達式在“類”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class This extends Expr {
    This(Token keyword) {
      this.keyword = keyword;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitThisExpr(this);
    }

    final Token keyword;
  }
```

### A2 . 1 . 11 Unary expression

> Unary operators are introduced in “[Representing Code](http://www.craftinginterpreters.com/representing-code.html)”.

一元運算符在“表示代碼”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class Unary extends Expr {
    Unary(Token operator, Expr right) {
      this.operator = operator;
      this.right = right;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitUnaryExpr(this);
    }

    final Token operator;
    final Expr right;
  }
```

### A2 . 1 . 12 Variable expression

> Variable access expressions are introduced in “[Statements and State](http://www.craftinginterpreters.com/statements-and-state.html#variable-syntax)”.

變量訪問表達式在“語句和狀態”中介紹過。

*<u>lox/Expr.java，嵌套在Expr類中：</u>*

```c
  static class Variable extends Expr {
    Variable(Token name) {
      this.name = name;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitVariableExpr(this);
    }

    final Token name;
  }
```

> ## A2 . 2 Statements

## A2.2 語句

> Statements form a second hierarchy of syntax tree nodes independent of expressions. We add the first couple of them in “[Statements and State](http://www.craftinginterpreters.com/statements-and-state.html)”.

語句形成了獨立於表達式的第二個語法樹節點層次。我們在“聲明和狀態”中添加了前幾個。

*<u>lox/Stmt.java，創建新文件：</u>*

```c
package com.craftinginterpreters.lox;

import java.util.List;

abstract class Stmt {
  interface Visitor<R> {
    R visitBlockStmt(Block stmt);
    R visitClassStmt(Class stmt);
    R visitExpressionStmt(Expression stmt);
    R visitFunctionStmt(Function stmt);
    R visitIfStmt(If stmt);
    R visitPrintStmt(Print stmt);
    R visitReturnStmt(Return stmt);
    R visitVarStmt(Var stmt);
    R visitWhileStmt(While stmt);
  }

  // Nested Stmt classes here...

  abstract <R> R accept(Visitor<R> visitor);
}
```

### A2 . 2 . 1 Block statement

> The curly-braced block statement that defines a local scope is introduced in “[Statements and State](http://www.craftinginterpreters.com/statements-and-state.html#block-syntax-and-semantics)”.

在“語句和狀態”中介紹過的花括號塊語句，可以定義一個局部作用域。

*<u>lox/Stmt.java，嵌套在Stmt類中：</u>*

```c
  static class Block extends Stmt {
    Block(List<Stmt> statements) {
      this.statements = statements;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitBlockStmt(this);
    }

    final List<Stmt> statements;
  }
```

### A2 . 2 . 2 Class statement

> Class declarations are introduced in, unsurprisingly, “[Classes](http://www.craftinginterpreters.com/classes.html#class-declarations)”.

類聲明是在“類”中介紹的，毫不意外。

*<u>lox/Stmt.java，嵌套在Stmt類中：</u>*

```c
  static class Class extends Stmt {
    Class(Token name,
          Expr.Variable superclass,
          List<Stmt.Function> methods) {
      this.name = name;
      this.superclass = superclass;
      this.methods = methods;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitClassStmt(this);
    }

    final Token name;
    final Expr.Variable superclass;
    final List<Stmt.Function> methods;
  }
```

### A2 . 2 . 3 Expression statement

> The expression statement is introduced in “[Statements and State](http://www.craftinginterpreters.com/statements-and-state.html#statements)”.

表達式語句在“語句和狀態”中介紹過。

*<u>lox/Stmt.java，嵌套在Stmt類中：</u>*

```c
  static class Expression extends Stmt {
    Expression(Expr expression) {
      this.expression = expression;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitExpressionStmt(this);
    }

    final Expr expression;
  }
```

### A2 . 2 . 4 Function statement

> Function declarations are introduced in, you guessed it, “[Functions](http://www.craftinginterpreters.com/functions.html#function-declarations)”.

函數聲明是在“函數”中介紹的。

*<u>lox/Stmt.java，嵌套在Stmt類中：</u>*

```c
  static class Function extends Stmt {
    Function(Token name, List<Token> params, List<Stmt> body) {
      this.name = name;
      this.params = params;
      this.body = body;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitFunctionStmt(this);
    }

    final Token name;
    final List<Token> params;
    final List<Stmt> body;
  }
```

### A2 . 2 . 5 If statement

> The `if` statement is introduced in “[Control Flow](http://www.craftinginterpreters.com/control-flow.html#conditional-execution)”.

`if`語句在“控制流”中介紹過。

*<u>lox/Stmt.java，嵌套在Stmt類中：</u>*

```c
  static class If extends Stmt {
    If(Expr condition, Stmt thenBranch, Stmt elseBranch) {
      this.condition = condition;
      this.thenBranch = thenBranch;
      this.elseBranch = elseBranch;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitIfStmt(this);
    }

    final Expr condition;
    final Stmt thenBranch;
    final Stmt elseBranch;
  }
```

### A2 . 2 . 6 Print statement

> The `print` statement is introduced in “[Statements and State](http://www.craftinginterpreters.com/statements-and-state.html#statements)”.

`print`語句在“語句和狀態”中介紹過。

*<u>lox/Stmt.java，嵌套在Stmt類中：</u>*

```c
  static class Print extends Stmt {
    Print(Expr expression) {
      this.expression = expression;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitPrintStmt(this);
    }

    final Expr expression;
  }
```

### A2 . 2 . 7 Return statement

> You need a function to return from, so `return` statements are introduced in “[Functions](http://www.craftinginterpreters.com/functions.html#return-statements)”.

你需要一個函數才能返回，所以`return`語句是在“函數”中介紹的。

*<u>lox/Stmt.java，嵌套在Stmt類中：</u>*

```c
  static class Return extends Stmt {
    Return(Token keyword, Expr value) {
      this.keyword = keyword;
      this.value = value;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitReturnStmt(this);
    }

    final Token keyword;
    final Expr value;
  }
```

### A2 . 2 . 8 Variable statement

> Variable declarations are introduced in “[Statements and State](http://www.craftinginterpreters.com/statements-and-state.html#variable-syntax)”.

變量聲明在“語句和狀態”中介紹過。

*<u>lox/Stmt.java，嵌套在Stmt類中：</u>*

```c
  static class Var extends Stmt {
    Var(Token name, Expr initializer) {
      this.name = name;
      this.initializer = initializer;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitVarStmt(this);
    }

    final Token name;
    final Expr initializer;
  }
```

### A2 . 2 . 9 While statement

> The `while` statement is introduced in “[Control Flow](http://www.craftinginterpreters.com/control-flow.html#while-loops)”.

`while`語句在“控制流”中介紹過。

*<u>lox/Stmt.java，嵌套在Stmt類中：</u>*

```c
  static class While extends Stmt {
    While(Expr condition, Stmt body) {
      this.condition = condition;
      this.body = body;
    }

    @Override
    <R> R accept(Visitor<R> visitor) {
      return visitor.visitWhileStmt(this);
    }

    final Expr condition;
    final Stmt body;
  }
```