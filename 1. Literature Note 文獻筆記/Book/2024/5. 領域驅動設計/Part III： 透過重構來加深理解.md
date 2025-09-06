---
tags: []
date: 2024-11-06
time: 23:00
---
1. 複雜巧妙的領域模型是可以實作的，也值得我們花費力氣
2. 這樣麼模型離開「不斷的重構」是很難開發出來的，重構需要領域專家和熱愛學習領域知識的開發人員密切參與
3. 要實作並有效的運用模型，需要精通設計技巧

開發人員透過重構不僅能夠理解程式碼實作的功能，還能明白其中原因，並把他們與領域專家的交流連結起來。

作者常用貨櫃運送來舉例。一般直覺想到的建模方式，可能會馬上想到「船」。但實際開發出來之後，會發現重要的是「航程」，運輸工具本身並不是重點（可能有意外需要換）。
而且還有其他要關注的事情，例如「提貨單」，這是貨物交接相關的法律責任轉移。

明確反應領域的模型通常都具有「功能多樣、簡單易懂和解釋力強」的特性。

### 柔性設計
越需要修改的地方，就會在不斷重構的過程中，添加靈活性。

##  8. 突破
持續微小的重構，得到深層模型

這章用一個實際的範例：**聯合貸款 syndicated loan**
這是讓一家公司（例如Intel）需要很多錢蓋廠房時，讓他可以跟很多銀行借錢的功能。因為需要的錢很多，所以需要讓很多銀行分攤。

在重構的過程中，他們發圓餅圖很適合用來描述這些模型，也在這段期間發現Facility和Loan是不需要成正比的（修正了本來的認知）。

## 9. 將隱式概念轉變為顯示概念

### 概念挖掘
- 傾聽團隊語言
- 檢查設計的不足以及與專家觀點相互矛盾的地方
- 研究領域文獻
- 大量實驗

### 傾聽語言
有沒有一些術語能夠簡潔的表達出複雜的概念？
有沒有被領域專家糾正過用詞？

這邊舉了一個例子：Cargo and Itinerary
本來的設計只用Cargo跟資料庫的基本資料，要做一些應用的時候都會牽扯到資料庫。
但在跟專家討論後，發現航海日程 Itinerary 是個更重要的概念，有更多用途。

### 檢查不足之處
有時這很難意識到。也須物件能夠做到你要的功能，但是職責的實作卻很笨拙。
可以的話，讓專家一起思考、驗證。沒有的話，就得自行思索，再讓專家判斷是否認同。

### 如何為那些不太明顯的概念建模
#### 明確的約束
約束是模型概念中非常重要的類別。他們通常是隱含的，將他們明確地表現出來可以極大地提高設計品質。
```java
private void pureIn(float addedVolume) {
	float volumePresent = contents + addedVolume;
	contents = constrainedToCapacity(volumePresnet);
}
private float constrainedToCapacity(float volumePlacedIn) {
	if (volumePlacedIn > capacity) return capacity;
	return volumePlacedIn;
}
```
現在這個約束條件是「有名有姓」的概念了。

##### 約束的存在正在擾亂其宿主物件
1. 當評估約束時，需要「不符合這個物件定義」的資料
2. 相關規則在多個物件中出現，造成重複，或導致不屬於同一家族的物件產生繼承關係
3. 很多設計與討論都圍繞著這些約束，但他們卻隱藏在程序程式碼中（我覺得這裡的意思有點像是不該把約束當成私有函式）

### 將「過程」建模為領域物件
我們都不希望程序procedure 變成模型的主要部分。我們只要考慮物件的「目的」或「意圖」。

約束constraint和過程process是兩大類模型概念。

### 模式：SPECIFICATION

在*邏輯程式範式*中，謂詞是指計算結果boolean的函數，並且可以用運算子（如AND, OR）把他們連接，以表達更複雜的規格。

業務規則通常不適合作為Entity或Value Object，但也不可將之移出領域層。

Specification宣告的是限制另一個物件狀態的約束，可以檢驗物件是否滿足指定的標準。
```java
Invoice Delinquency
test(Invoice): boolean
```

只為了「特殊目的」來建立「謂詞形式」的顯示Value Object。可以用完就丟。
Specification就是一個謂詞，可以用來確定物件是否滿足某些標準。

### Specification的應用與實作
*p.231*
需要指定物件狀態時的使用情境：
1. 驗證物件，檢查他是否滿足某些需求
2. 從集合中選擇一個物件
3. 指定在建立新物件時必須滿足某種需求

#### 驗證
```java
Date tody = new Date();
Specification delinquentSpec = new DelinquentInvoiceSpecification(tody);
Iterator it = customer.getInvoices().iterator();

while(it.hasNext()) {
	Invoice candidate = (Invoice)it.next();
	if (delinquentSpec.isSatisfiedBy(candidate))
		return true;
}
return false;
```

#### 選擇或查詢 Selection or Querying
如果資料在記憶體時，就跟上面驗證用起來沒什麼區別。
但常用的場景可能是，資料在關聯是資料庫裡面。

我們想要充分利用關聯是資料庫的強大查詢能力，同時又保留Specification模型。

可以將SQL程式碼置於Repository中，而應該使用哪些查詢則由Specification來控制。
這樣Specification中沒有完整定義規則，但規則的核心已位於其中：指明了什麼條件「構成了拖欠（範例）」。

#### 根據要求建立
這種Specification的概念與驗證、選擇並無不同。都是在為尚未建立的物件指定標準。
但是Specification的實作則會大不相同。
我們可以用描述性的Specification來定義產生器的介面，這個介面就「顯示地」約束了產生器的「結果」。
根據要求來建立，可以是從頭建立全新物件，也可以是設定已有物件來滿足Specification。


## 10. 柔性設計 Supple Design
程式碼需要易於修改。好懂也就意味著易於修改。

### 模式：INTENTION-REVEALING INTERFACES
「沒有明確把計算邏輯表達出來」的程式碼是有問題的。

如果客戶開發人員需要深入研究物件的內部機制，就失去封裝的大部分價值了。

在命名類別和操作時，要描述他們的效果和目的，而不要透漏他們是透過何種方式達到目的。
這樣可以使客戶開發人員鼻必去理解內部細節。
在建立一個行為之前，先為他邊寫一個測試，這樣可以促使你站在客戶開發人員的角度上思考它。
```java
outPaint.mixIn(blue);
```

### 模式：SIDE-EFFECT-FREE FUNCTION
我們可以廣泛的把操作分成命令command和查詢query兩大類。

開發人員為了預測操作的結果，必須里接他的實作以及他所呼叫的其他方法的實作。如果開發人員不得不掀開介面的面紗，那麼介面的抽象作用就受到了限制。

- 確保「導致狀態改變的方法」不回傳領域資料，並保持簡單
- 在「不引起任何可觀測到的副作用的方法」之中執行所有的查詢和計算

如果一個操作把「邏輯或運算」與「狀態改變」混合在一起，那麼我們就應該把這個操作重構為兩個獨立的操作。

盡可能把邏輯放到函數中，因為函數只回傳結果，不產生明顯副作用；嚴格地把命令（引起狀態改變的方法）隔離到「不回傳領域資訊的、非常簡單的操作」之中，就可以把這個複雜邏輯移到Value Object中，進一步控制副作用。

```java
public class PigmentColor {
	public PigmentColor mixedWith(PigmentColor other, double ratio) {
		// 複雜的邏輯，回傳新的Value Object
	}
}

public class Paint {
	public void mixIn(Paint other) {
		volume = volume + other.getVolume();
		double ratio = other.getVolume() / volume;
		pigmentColor = pigmentColor.mixedWith(other.pigmentColor(), ratio);
	}
}
```


### 模式：ASSERTION
後置條件 post-condition 描述了一個操作的副作用，也就是呼叫一個方法之後「必然會發生的結果」。
前置條件 precondition 就像是合約條款，即為了滿足後直條件而必須要滿足的前置條件。

#### 把操作的後置條件和類別及Aggregate的固定規則陳述清楚。

測試首先設置「前置條件」，在執行之後，再檢查「後置條件」是否被滿足。

```java
public void testMixingVolume {
	PigmentColor yellow = new PigmentColor(0, 50, 0);
	PigmentColor blue = new PigmentColor(0, 0, 50);

	StockPaint paint1 = new StockPaint(1.0, yellow);
	StockPaint paint2 = new StockPaint(1.5, blue);
	MixedPaint mix = new MixedPaoint();

	mix.mixIn(paint1);
	mix.mixIn(paint2);
	assertEquals(2.5, mix.getVolume(), 0.01);
}
```


> [!NOTE] 例子間的差異
> 書中在示範這個例子之前，討論了上一個例子中「混合的油漆」是否應該把體積減少為0或是刪除。
> 我們的直覺是「混合之後的油漆總體積保持不變」。
> 但是程式原本的目的是幫助使用者搞清楚把哪幾種油漆混合。
> 或許不是一切的事物都是符合直覺，但現在的尷尬局面是概念缺失造成的。


**Intention Revealing Interface清楚地表明了用途，Side effect free function 和 Assertion 使我們能夠更準確地預測結果，因此封裝和抽象更加安全**


### 模式：CONCEPTUAL CONTOUR 概念輪廓

在做每個決定前，都要問自己：「這是根據當前模型和程式碼中的特定關係做出的權宜之計呢？還是反映了底層領域的某種輪廓？」

把設計專案（操作、介面、類別和Aggregate）翻解圍內聚的單元，在這個過程中，你對領域中的一切重要劃分的直覺認識也要考慮在內。在連續的重構過程中觀察「發生變化」和「保證穩定」的規律性，並尋找能狗「解釋」這些變化模式的底層Conceptual Contour。


### 模式：STANDALONE CLASS

低耦合是物件設計的一個基本要素，盡量保持低耦合。把其他所有無關概念提取到物件之外。這樣類別就變得完全獨立了，這能讓我們可以單獨的研究和理解他。每個這樣的獨立類別都極大地減輕了「因理解Module而帶來的負擔」。

我們的目標不是消除所有依賴，而是消除所有「不重要的依賴」。

獨立的類別是低耦合的極致。（如PigmentColor）

### 模式：CLOSURE OF OPERATION 閉合操作

在適當的情況下，在定義操作時讓他的回傳類型與其引述的類型相同。如果實作者的狀態在計算中會被用到，那麼實作者也是一個引述，因此引述和回傳值應該與實作者有相同類型。

這種模式更常用於Value Object的操作。

PigmentColor.mixedWith()就是種閉合操作。

從集合種選擇子集
```Smalltalk
employees := (some Set of Employee objects).
lowPaidEmployees := employees select:
	[:anEmployee | anEmployee salary < 40000].
```

### 宣告式設計

用聲明式的風格來擴展Specification

包容 Subsumption
NewSpec -> Old Spec
新規格為真，那舊規格

| 受 SPECIFICATION 約束的亞里斯多德                           |                                                                                                                                                             |
| -------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 所有人都是要死的（All men are mortal）                       | Specification manSpec = new ManSpecification();<br><br>Specification mortalSpec = new MortalSpecification!);<br><br>assert manSpec. subsumes (mortalSpec) ; |
| 亞里斯多德是一個人（Aristotle is a man）                      | Man aristotle = new Man) ;<br><br>assert manSpec. isSatisfiedBy(aristotle);                                                                                 |
| 因此，亞里斯多德會死<br><br>(Therefore, Aristotle is mortal) | assert mortalSpec.isSatisfiedBy(aristotle);                                                                                                                 |

### 切入問題的角度
#### 盡可能利用已有的形式
範例：把各種模式結合起來使用的「股份數學」

需求：當借貸方償還本金時，預設使「根據放貸方的股份」來分配這筆錢。

- 複雜的邏輯透過 **Side-Effect-Free Function** 被封裝到了專門的 Value Object 之中。由於Share Pie 是 Value Object ，因此數學運算可以建立新實例，我們可以用這些新實例來替換舊實例。Share Pie 的所有方法都不會修改任何現有物件，這使我們能夠自由使用 `plus()` `minus()` `prorated()` ，並組合他們實作預期效果，同時又不會產生其他副作用。
- 修改狀態的操作很簡單，而且使用Assertion來描述的。
- 模型概念解除了耦合；操作只涉及最少的其他模型。Share Pie 雖然不是閉合操作，但只增加極少的概念負擔。Share Pie 只與 Share 有密切互動。這樣 Share Pie 非常直接了當，易於理解和測試，也容易透過組合來產生宣告式的交易。這些特性都是從數學形式中繼承而來的。
- 熟悉的形式讓我們更容易掌握 protocol 。


## 11. 應用分析模式
**分析模式**是一本介紹業務建模中常見結構的概念集合的書。此章用範例演練應用的情境。

## 12. 將設計模式應用於模型

### 模式：STRATEGY（也稱Policy）
[guru 策略模式](https://refactoringguru.cn/design-patterns/strategy)

我們需要把過程中的「易變部分」提取到模型的一個單獨的「策略」物件之中。將規則與他所控制的行為分開。
按照Strategy設計模式來實作規則或可替換的過程。

#### 範例：路線尋找策略
Routing Service在尋找Itinerary時，實際上會計算Leg的規模。
```
RoutingService
find(Specification, LegMagnitudePolicy): Itinerary
```


### 樣式：COMPOSITE
[guru 組合模式](https://refactoringguru.cn/design-patterns/composite)

當巢套容器的關聯性沒有在模型中反映出來時，公共行為必然會在層次結構的每一層重複出現，而巢套也變得僵化


把設計模式用作領域模式的唯一要求是「這些模式能夠描述關於概念領域的一些事情」，而不僅僅作為「解決技術問題」的技術解決方案。





## 13. 透過重構得到更深層的理解

1. 以領域為本
2. 用一種不同的方式看待事物
3. 始終堅持與領域專家對話

### 探索團隊
不管問題的根源是什麼，下一步都是要尋找一種能夠使模型「表達變得更清楚和更自然」的改進方案。

邀請領域專家、與四到五人進行一場30~90分鐘的頭腦風暴。使用UML圖、演練場景。

### 借鑑先前的經驗
我們可以從書籍和領域本身的其他知識來源獲得想法。
當設計模式既符合實作需求、又符合魔性概念時，通常就可以在領域層中應用這些模式。

### 重構的時機
如果要等到「完全證明了修改的合理性」之後才去修改，那可能要等很久。

人們雖然覺得修改程式碼會有風險，卻不容易看到「維持一個拙劣設計」也有風險。

軟體發展不是一個可以完全預料後果的過程。我們無法準確計算哪些修改會帶來哪些好處，或是不做哪些修改會付出多大代價。

發生以下情況時，就該重構了。
- 設計沒有表達出團隊對領域的最新理解
- 概念被隱藏在設計之中了
- 發現了能令某個重要的設計部分變得更靈活的機會

### 危機就是轉機
在對模型進行一段時間「穩定的改進」後，你可能突然有所頓悟，而這會改變模型中的遺切。
這些突破不會每天發生，然而很大一部分的深層模型和柔性設計都來自這些突破。