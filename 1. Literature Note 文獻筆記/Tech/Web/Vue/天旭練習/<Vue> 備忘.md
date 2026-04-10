1. [Awesome Examples of Vue Router Transitions](https://learnvue.co/tutorials/vue-router-transitions)
2. [# A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
3. [相對位置說明: relative absolute](https://stackoverflow.com/questions/10487292/position-absolute-but-relative-to-parent)
4. 在ts class宣告的成員是來自pinia或是xstate時，不想使用any（畢竟沒有任何提示），不用額外導入文件，而是使用[[ReturnType]]


```html
// 播完動畫馬上關閉
<div
    class="show-score"
    v-show="showUpdateScore"
    @animationend="showUpdateScore = false"
>
    {{ scoreDeltaText }}
</div>
```
