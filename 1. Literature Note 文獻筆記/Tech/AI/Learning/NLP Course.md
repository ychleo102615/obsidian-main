---
tags:
  - AI
date: 2023-09-04-週一
time: 16:59
---
[link](https://huggingface.co/learn/nlp-course/chapter1/2?fw=pt)

## 主要幾個具代表性的功能

1. 文本分類（例：是否為垃圾文章、兩個文章是否有關聯...）
2. 符號辨識（例：文本中詞性、人名地名....）
3. 文本生成
4. 文本總結
5. 猜克漏字
6. 閱讀測驗（提供文本，從中推出答案）
7. ...

## [[Transformer]]
參考[[self-attention]]架構

## Transfer Learning（遷移學習）
[link](https://huggingface.co/learn/nlp-course/chapter1/4?fw=pt#transfer-learning)

![](https://editor.analyticsvidhya.com/uploads/499849315476_1592890541_transfer.jpg)

> [!cite] 其他中文網站
> [TRANSFER LEARNING-了解深度學習的遷移學習](https://www.keywordseo.com.tw/blog1/understanding-transfer-learning-for-deep-learning/)

#### 從 [[Pretraining（預訓練）]]好的資料，繼續訓練（FineTuning）成目標模型。


---
## 如何使用Transformer
[course link](https://huggingface.co/learn/nlp-course/chapter1/3?fw=pt)

Hugging Face提供了許多基於Transformer架構的 api, model。
```shell
!pip install transformers
```


> [!Example] 
> ```python
> from transformers import pipeline
>
>classifier = pipeline("sentiment-analysis")
>classifier("I've been waiting for a HuggingFace course my whole life.")
>
># output
>[{'label': 'POSITIVE', 'score': 0.9598047137260437}]
> ```

*[Pipelines](https://huggingface.co/docs/transformers/main_classes/pipelines)*：一個簡單的api，可以快速地使用model來做推導。
- `feature-extraction` (get the vector representation of a text)
- `fill-mask`
- `ner` (named entity recognition)
- `question-answering`
- `sentiment-analysis`
- `summarization`
- `text-generation`
- `translation`
- `zero-shot-classification`


#### [Pipeline 底下真正在做的事](https://huggingface.co/learn/nlp-course/chapter2/2?fw=pt)

