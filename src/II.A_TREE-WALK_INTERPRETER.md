# II. A TREE-WALK INTERPRETER 基於樹遍歷的解釋器

> With this part, we begin jlox, the first of our two interpreters. Programming languages are a huge topic with piles of concepts and terminology to cram into your brain all at once. Programming language theory requires a level of mental rigor that you probably haven’t had to summon since your last calculus final. (Fortunately there isn’t too much theory in this book.)

在這部分中，我們開始學習jlox，這是我們兩個解釋器中的第一個。編程語言是一個巨大的話題，其中有大量的概念和術語需要一下子塞進你的大腦。編程語言理論需要一定程度的腦力投入，你可能自上次微積分期末考試後就沒這麼投入過了。(幸運的是，這本書沒有太多的理論。)

> Implementing an interpreter uses a few architectural tricks and design patterns uncommon in other kinds of applications, so we’ll be getting used to the engineering side of things too. Given all of that, we’ll keep the code we have to write as simple and plain as possible.

實現一個解釋器需要一些架構技巧和設計模式，這在其他類型的應用程序中是不常見的，所以我們也要習慣於工程方面的東西。考慮到這些，我們會盡可能地讓代碼簡單明瞭。

> In less than two thousand lines of clean Java code, we’ll build a complete interpreter for Lox that implements every single feature of the language, exactly as we’ve specified. The first few chapters work front-to-back through the phases of the interpreter—[scanning](http://craftinginterpreters.com/scanning.html), [parsing](http://craftinginterpreters.com/parsing-expressions.html), and [evaluating code](http://craftinginterpreters.com/evaluating-expressions.html). After that, we add language features one at a time, growing a simple calculator into a full-fledged scripting language.

在不到2000行簡潔的Java代碼中，我們將為Lox構建一個完整的解釋器，完全按照我們指定的方式實現該語言的每一個功能。前幾章從頭到尾介紹解釋器的各個階段——[掃描](http://craftinginterpreters.com/scanning.html)、[解析](http://craftinginterpreters.com/parsing-expressions.html)和[計算代碼](http://craftinginterpreters.com/evaluating-expressions.html)。之後，我們逐步添加語言特性，將一個簡單的計算器發展成一種成熟的腳本語言。

