---
tags: 
date: 2024-01-05
time: 11:02
---
# 安裝
必須要先裝有`java`。然後Mac的情況，直接再用`brew install antlr`安裝就好。
這樣還是不算完全裝好，後來是再補上這行在`.zshrc`後才應該沒問題了。

```shell
export CLASSPATH="/opt/homebrew/Cellar/antlr/4.13.1/antlr-4.13.1-complete.jar"
```

[參考](https://github.com/tunnelvisionlabs/antlr4/blob/master/doc/faq/installation.md)


# 術語
|  |  |
| ---- | ---- |
| 語言(language) | 合法子句的集合，子句可再由其子句組合，以此類推。 |
| 文法(grammar) | 文法定義了語言的語意規則(syntax rules) |
| 語意樹(syntax tree/parse tree) | 語句的結構。子樹的根節點代表了文法規則，葉節點代表tokens |
| 詞法符號(tokens) | 一個語言的基本詞彙、符號 |
| 詞法分析器、符號產生器(lexer, tokenizer) | 將數入字串分解成一系列tokens |


# `Tool & API`
ANTLR由兩個關鍵部分組成：
1. 本身分析文法的工具
2. 分析好後，lexer, parser所需要的`API`



# 自動生成的程式碼

寫好`.g4`檔之後，對其使用antlr：
```shell
# ArrayInit is an example from the book
antlr ArrayInit.g4
```
會自動生成以下檔案（省略前綴）：
1. Parser
2. Lexer
3. tokens
4. Lexer.tokens
5. Listener
6. BaseListener


# 整合到程式裡面

```
file -> AntlrInputStream -> XxxLexer -> CommonTokenStream -> XxxParser

-- begin parsing with 'init', which is the first rule in the grammar
parser.init();
```







# 左遞迴  section5.4 p.69