# III. A BYTECODE VIRTUAL MACHINE 字節碼虛擬機

> Our Java interpreter, jlox, taught us many of the fundamentals of programming languages, but we still have much to learn. First, if you run any interesting Lox programs in jlox, you’ll discover it’s achingly slow. The style of interpretation it uses—walking the AST directly—is good enough for some real-world uses, but leaves a lot to be desired for a general-purpose scripting language.

我們的Java解釋器jlox教會了我們許多編程語言的基礎知識，但我們仍然有許多東西需要學習。首先，如果你在jlox中運行任何Lox程序，你會發現它非常慢。它所使用的解釋方式——直接遍歷AST，對於某些實際應用來説已經足夠了，但是對於通用腳本語言來説還有很多不足之處。

> Also, we implicitly rely on runtime features of the JVM itself. We take for granted that things like instanceof in Java work somehow. And we never for a second worry about memory management because the JVM’s garbage collector takes care of it for us.

另外，我們隱式地依賴於JVM本身的運行時特性。我們想當然地認為像`instanceof`這樣的語句在Java中是可以工作的。而且我們從未擔心過內存管理，因為JVM的垃圾收集器為我們解決了這個問題。

> When we were focused on high-level concepts, it was fine to gloss over those. But now that we know our way around an interpreter, it’s time to dig down to those lower layers and build our own virtual machine from scratch using nothing more than the C standard library . . . 

當我們專注於高層次概念時，我們可以忽略這些。但現在我們已經對解釋器瞭如指掌，是時候深入到這些底層，從頭開始構建我們自己的虛擬機，只用C語言標準庫就可以了……