# craftinginterpreters_zh

[ [在線閲讀](https://readonly.link/books/https://raw.githubusercontent.com/GuoYaxiang/craftinginterpreters_zh/main/book.json) ]

手擼解釋器教程《Crafting Interpreters》中文翻譯。

這是一個已基本完成的翻譯項目，原項目是[craftinginterpreters](https://github.com/munificent/craftinginterpreters)，同時還有配套的英文書，可免費[在線閲讀](http://www.craftinginterpreters.com/)。

該書由一門小型的自創語言Lox開始，分別使用Java和C實現了兩種類型的解釋器，jlox和clox，其中前者是將語法解析成Java中的表示代碼，主要依賴Java本身的語法能力實現代碼的真正運行；後者則採用了類似編譯和虛擬機的機制，實現了一個看上去“更高效”的解釋器。

該書中並不是只灌輸概念或者只貼出代碼，相反，作者經過悉心拆解解釋器相關的概念，在每一章節中逐步進行講解和實現，並且保證每個章節結束之後都有一個可以運行的解釋器版本。內容上不會有太過深入的理論，對於普通編程愛好者也可以很容易地上手學習。

如果您的英語閲讀能力比較強，建議直接閲讀原文，同時也歡迎您參與本項目，分享自己學習的成果，幫助更多的人。

囿於本人能力限制，在譯文難免有錯漏或者含混之處，請積極留言，我會悉心聽取大家的意見，爭取可以讓這篇譯文幫助到更多人。

如果您覺得這篇譯文對您的學習有所幫助，可以獎勵作者一杯奶茶:)

<img src="http://img.codinghonest.space/donate/alipay.png" alt="支付寶" width="300" height="300" />                    <img src="http://img.codinghonest.space/donate/wechat.png" alt="微信支付" width="300" height="300" />

### 進度

| 章節序號 | 章節名                                                       | 內容簡介     | 完成情況 |
| -------- | ------------------------------------------------------------ | ------------ | -------- |
| I        | [WELCOME](./content/I.WELCOME.md)                            | 導讀         | 已完成   |
| 1        | [Introduction](./content/1.前言.md)                          | 前言         | 已完成   |
| 2        | [A Map of the Territory](./content/2.領土地圖.md)            | 解釋器簡介   | 已完成   |
| 3        | [The Lox Language](./content/3.Lox語言.md)                   | Lox語言介紹  | 已完成   |
| II       | [A TREE-WALK INTERPRETER](./content/II.A_TREE-WALK_INTERPRETER.md) | jlox介紹     | 已完成   |
| 4        | [Scanning](./content/4.掃描.md)                              | 掃描器相關   | 已完成   |
| 5        | [Representing Code](./content/5.表示代碼.md)                 | 表示代碼     | 已完成   |
| 6        | [Parsing Expressions](./content/6.解析表達式.md)             | 解析表達式   | 已完成   |
| 7        | [Evaluating Expressions](./content/7.表達式求值.md)          | 執行表達式   | 已完成   |
| 8        | [Statements and State](./content/8.表達式和狀態.md)          | 語句和狀態   | 已完成   |
| 9        | [Control Flow](./content/9.控制流.md)                        | 控制流       | 已完成   |
| 10       | [Functions](./content/10.函數.md)                            | 函數         | 已完成   |
| 11       | [Resolving and Binding](./content/11.解析和綁定.md)          | 解析和綁定   | 已完成   |
| 12       | [Classes](./content/12.類.md)                                | 類           | 已完成   |
| 13       | [Inheritance](./content/13.繼承.md)                          | 繼承         | 已完成   |
| III      | [A BYTECODE VIRTUAL MACHINE](./content/III.A_BYTECODE_VIRTUAL_MACHINE.md) | clox介紹     | 已完成   |
| 14       | [Chunks of Bytecode](./content/14.字節碼塊.md)               | 字節碼       | 已完成   |
| 15       | [A Virtual Machine](./content/15.虛擬機.md)                  | 虛擬機       | 已完成   |
| 16       | [Scanning on Demand](./content/16.按需掃描.md)               | 掃描         | 已完成   |
| 17       | [Compiling Expressions](./content/17.編譯表達式.md)          | 編譯表達式   | 已完成   |
| 18       | [Types of Values](./content/18.值類型.md)                    | 值類型       | 已完成   |
| 19       | [Strings](./content/19.字符串.md)                            | 字符串       | 已完成   |
| 20       | [Hash Tables](./content/20.哈希表.md)                        | 哈希表       | 已完成   |
| 21       | [Global Variables](./content/21.全局變量.md)                 | 全局變量     | 已完成   |
| 22       | [Local Variables](./content/22.局部變量.md)                  | 局部變量     | 已完成   |
| 23       | [Jumping Back and Forth](./content/23.來回跳轉.md)           | 來回跳轉     | 已完成   |
| 24       | [Calls and Functions](./content/24.調用和函數.md)            | 調用和函數   | 已完成   |
| 25       | [Closures](./content/25.閉包.md)                             | 閉包         | 已完成   |
| 26       | [Garbage Collection](./content/26.垃圾回收.md)               | 垃圾回收     | 已完成   |
| 27       | [Classes and Instances](./content/27.類與實例.md)            | 類和實例     | 已完成   |
| 28       | [Methods and Initializers](./content/28.方法和初始化器.md)   | 方法和初始化 | 已完成   |
| 29       | [Superclasses](./content/29.超類.md)                         | 超類         | 已完成   |
| 30       | [Optimization](./content/30.優化.md)                         | 優化         | 已完成   |
| ❧        | [BACKMATTER](./content/後記.md)                             | 後記         | 已完成   |
| A1       | [Appendix I: Lox Grammar](./content/附錄I.md)               | Lox語法      | 已完成   |
| A2       | [Appendix II: Generated Syntax Tree Classes](./content/附錄II.md) | 語法樹類     | 已完成   |



PS：

文本中使用了很多Typora功能語法，建議使用[Typora](https://typora.io/)閲讀，



### 特別鳴謝
感謝[xieyuheng](https://github.com/xieyuheng)提供的在線閲讀支持，為需要在線閲讀markdown文檔的同學推薦[read-only項目](https://github.com/readonlylink/readonlylink)，樣式簡約大方，值得一試。