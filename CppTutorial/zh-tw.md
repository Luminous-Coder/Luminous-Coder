---
title: C++教學
description: C++基礎教學
tags: Tutorial
lang: zh-tw
breaks: false
---

# 序

C\+\+是一個強大的程式語言，儘管名字上相似，也有歷史淵源，但C\+\+並非C的超集，如同Javascript之於Java，應該作為不同的語言看待。
其能夠在兼顧高效能的同時表達高階概念，輕鬆撰寫出跨平台的程式碼，因而歷久不衰。
無論是初學者，抑或已經掌握其他語言的程式設計師都適合學習。

由於從完整而全面的角度描述難以同時進行從零開始的教學，因此在許多章節會有「可跳過的細節」區塊，在閱讀到更後面時再回來看看吧！
移除這些區塊是今後改善的目標。

## 致謝

感謝一路上幫助我的人們，在我曾經迷茫無知的時候伸出援手，沒有他們我不可能變成現在的樣子。
希望這份教學可以帶領更多人，在資訊的世界翱遊，而不迷失方向。

# 入門

C\+\+是一種預先編譯的語言，這表示你必須先把你的程式碼（原始碼）*編譯*成執行檔。如此一來，若你想要分享你的程式，可以直接發送執行檔而不是要求其他人安裝執行環境（例如Python）。

這個章節中，我們將討論如何安裝必要的工具，以及撰寫第一個程式。

## 安裝

為了撰寫程式，你至少需要：

- 編輯器（editor）
- 編譯器（compiler）

如果你正在進行一個大型專案，你甚至需要更多工具！（當然你也可以靠自己的大腦）

編輯器就是任何可以編輯檔案的應用程式，例如記事本；編譯器則是「將原始碼翻譯成電腦可以執行的0和1」的程式。

所以，你可以使用Windows的記事本來寫程式，但那很不方便，因此開發者通常會使用整合開發環境（integrated development environment，IDE），一個好的IDE甚至可以讓你開發得更有效率。
我推薦使用JetBrains的[CLion](https://www.jetbrains.com/clion/)[^CLion]，但你也可以使用其他的，像Microsoft Visual Studio等。

IDE通常有許多強大的輔助功能，但那不是我們要討論的。
因此，這裡將（假設你）使用一個普通的文字編輯器和終端來手動編譯，當然你也可以使用IDE直接透過GUI操作，通常可以在他們的網站上找到教學。

CLion允許你選擇想要的編譯器實現，Windows中可以安裝[clang](https://github.com/llvm/llvm-project/releases)，Linux則可以使用[g++](https://gcc.gnu.org/)。
安裝完成後，打開CLion的設定頁面，如果toolchain沒有自動偵測到，請手動指定。

## 程式進入點

要定義一個函式（function），包含四個部分：回傳型別（return type）、名稱（name）、參數（parameter）、主體（body）。
這裡的函式比起數學上的函數，稱作子程式可能更爲恰當，你可以傳入引數（argument）來呼叫函式，並得到回傳值，但有時更重要的是函式的副作用（side effect），這也是函式與數學函數最大的差異；例如我們常常要在螢幕上顯示文字，那就可以把這個動作寫成一個函式，傳入要顯示的文字，如此一來就只要呼叫這個函式就好，而這個函式的回傳並不那麼重要，它不計算什麼值。

進入點（entry point）是一個會在程式執行時，被系統呼叫的函式。在C\+\+中這個函式通常是一個名稱為`main`，會回傳一個`int`，也就是整數的函式。
這個整數會回傳給函式的呼叫者——系統，通常以0表示程式成功執行完畢，其他數值的含義則由系統決定。

所以，下面的範例是一個程式的進入點，作為一個函式，有回傳型別`int`、名稱`main`、參數（不接收參數），以及主體。
主體以花括號包裹，裡面則是多個述句（statement）。
範例中只有一個述句：`return 0;`，也就是回傳`0`。

<pre>
<span class="token keyword">int</span> <span class="token function">main</span>() {
    <span class="token keyword">return</span> <span class="token number">0</span>;
}
</pre>

## 編譯並執行

打開文字編輯器，輸入上面的程式碼（原始的程式碼通常稱作原始碼（source code））並儲存成`main.cpp`。然後打開終端（像Windows的Power Shell），輸入：

<pre>
<span class="token function">g++</span> main.cpp <span class="token param">-o</span> main
<span class="token function">./main</span>
</pre>

此教學將使用C\+\+17標準，因此你也可以加上`-std=c++17`來指定編譯器使用的標準。

注意指令會隨著shell和編譯器不同，請自行查找使用方式。

:::info
儘管在一些平台上，副檔名並非必須的，然而為了方便知道檔案的類型還是建議加上。

C\+\+原始碼有幾種常見的副檔名如`.cpp`或`.cc`。
:::

## Hello World

<pre>
<span class="token keyword">#include</span> <span class="token string">&lt;iostream&gt;</span>

<span class="token keyword">int</span> <span class="token function">main</span>() {
    <span class="token namespace">std</span>::<span class="token gvariable">cout</span> << <span class="token string">"Hello World!"</span>;
    <span class="token keyword">return</span> <span class="token number">0</span>;
}
</pre>

前置處理器會在編譯之前處理前置處理指令（preprocessor directive），也就是井號開頭的行。
`#include`指令能要求前置處理器找到指定的檔案，然後把裡面的內容貼上到你的檔案。
這裡，我們include了C\+\+標準庫中的`iostream`，這個檔案裡有一些輸出輸入相關的東西。
通常這些檔案被稱作標頭檔（header file）。

`std`是一個命名空間，標準庫的東西都在這個命名空間中，如此一來就可以防止「撞名」。
例如假如有兩個地方都叫紐約，說「美國，紐約」就可以知道是哪個紐約了。
`::`這個運算子能夠從命名空間中取得東西，所以`std::cout`就是「`std`裡的`cout`」的意思。

`cout`的意思是character output，是標準輸出輸出流（standard output stream），通常會輸出到終端。

如果你會其他語言的話，或許會覺得`<<`很怪，那看起來是個位元左移運算子。
事實上，那是多載過的運算子，運算子就只是個函式，但讓程式碼更清楚（例如可以使用`one < another`而不用像`one.isLessThan(another)`這樣）。
在這裡，`<<`是「流出」，它將右方的值放到左方的流中。

而`"Hello World!"`是一個字串字面值（literal）。
在C\+\+中，字串必須使用雙引號包裹。

## 註解

註解（comment）是程式中的「筆記」，能夠讓人更快速的瞭解程式的意圖，而編譯器會忽略這些部分。

可以使用兩個斜線來標記註解的開始，直到該行結束都會被編譯器忽略。
從`/*`到第一個`*/`為止的內容也都會被忽略。
然而為了統一風格，Google style建議只用其中一種，而不要混用。

<pre>
<span class="token comment">// 這是一行註解。</span>

<span class="token comment">/* 這是一「塊」註解。 */</span>
</pre>

:::info
註解的習慣十分重要！良好的註解可以讓其他人更快讀懂程式的意圖，也可以讓未來的自己更好維護。
:::

# 變數

當需要儲存一個值時，可以使用變數（variable）。
對於大多數如C\+\+一樣的命令式語言來說，變數和數學上的變數並不一樣，更像是一個在代表記憶體上特定的空間的名字。
最大的差異便是它是可變的（mutable）。

<pre>
<span class="token keyword">int</span> variable = <span class="token number">0</span>;
</pre>

例如上面的程式碼定義了一個名為`variable`的變數，其型別為`int`，也就是說它是一個整數。
在C\+\+中型別決定了能做的運算，例如對整數可以進行加法。

區域變數，也就是在函式主體內定義的變數，若是內建型別的話，在沒有初始化的情況下，嘗試取得資料是未定義行為（undefined behavior，UB）。
因此建議初始化所有變數。

## 內建型別

C\+\+提供的內建型別（built-in type）包含了算術型別和一些特別的型別，算術型別中又有許多整數型別（integral type）。

### 整數型別

基礎的整數型別是`int`，標準保證至少有16位元長，可以使用以下修飾符（modifier）：

- 有號性
  - `signed` - 有號，預設的有號性。
  - `unsigned` - 無號，即只能表示0和正數。
- 大小（通常會省略`int`）
  - `short` - 至少16位元。
  - `long` - 至少32位元。
  - `long long` - 至少64位元。

#### 字元型別

`char`則是字元型別，但也是整數型別的一種。
然而並不建議用來當作整數運算，因為型別對程式設計師來說也決定了預期的資料類型，例如一個印出內容的函式可能會將字元型別的參數作為字元印出而非整數。

`char`也可以使用`signed`和`unsigned`修飾，但如同前面所述，並不建議將其看作數字，若需要一個小的整數可以使用`std::int8_t`和`std::uint8_t`。
預設的有號性是實作定義的。

寬字元（`wchar_t`）有著能夠儲存支援的任何字元編碼的碼點大小。

`char8_t`、`char16_t`、`char32_t`則分別儲存UTF-8、UTF-16、UTF-32編碼下的一個編碼單元。
這表示除了`char32_t`，其他兩個型別可能不代表一個字元。

#### 布林型別

`bool`表示一個布林值（boolean），即只有「是」和「否」兩種狀態的型別，也可以用0和非零值表示。

### 浮點數型別

`float`、`double`、`long double`分別是不同精度的浮點數（single-precision、double-precision和extended-precision floating-point），浮點數是以二進位方式表示實數的近似值，因此存在誤差。

`float`的精度最差，但所佔空間也較小，運算速度也較快，然而由於現代電腦效能的提升，這些差異有時並不明顯。

### Void型別

還有一個特殊的型別：`void`。
其並不能作為變數的型別，用途也很少，最常見的用法是作為回傳值型別表示沒有回傳。

和一些語言中的`Unit`或`()`（空元組）不同，`void`是一個沒有值的型別。

### Size-of運算子

為了知道型別的大小可以使用`sizeof`運算子，例如`sizeof(int)`在一些機器上會回傳4，也就是一個`int`有四個`char`的大小。

## 參考

參考（reference）是一個物件的「別名」，本身並不是一個物件，使用方式如下：

<pre>
<span class="token keyword">int</span> i = <span class="token number">0</span>;
<span class="token keyword">int</span>&amp; ref = i;
</pre>

當定義一個參考變數時，必須將其繫結（bind）到一個變數，也就是告訴編譯器這個參考是哪個變數的別名，之後無法再改變繫結的對象。
對`ref`的所有操作都等同於對`i`進行的。

## 指標

指標（pointer）是一種儲存著記憶體位址（address）的變數，為了取得位址可以使用取址運算子（address-of operator）`&`：

<pre>
<span class="token keyword">int</span> i = <span class="token number">0</span>;
<span class="token keyword">int</span>* ptr = &amp;i;
</pre>

在上面的程式碼中，`*`表示`ptr`是一個指標，並且初始化為`i`的位址。
`void*`是一個特殊的指標型別，表示不知道指向的地方有什麼（即不指定型別）。

若要獲得指標指向的（位於儲存的位址上的）物件，要使用間接取值運算子（indirection operator）`*`。
然而若直接對`ptr`進行取值，這個程式無法成功編譯。
原因是我們並未指定`ptr`指向了什麼東西，由於型別決定能做的運算，也決定了物件的大小，電腦也就不知道要怎麼取得指向的物件。
要解決這個問題可以改為`int *ptr`，這表示`ptr`是指向一個`int`。

<pre>
<span class="token keyword">int</span>* ptr = &amp;i;
(*ptr) = <span class="token number">10</span>;
</pre>

:::info
所有指標都應該初始化，否則其值為未定義，若不小心進行取值可能造成嚴重錯誤。
:::

---

指標本身也能夠做運算，例如`ptr + 1`表示`ptr`指向的位址後面一個物件，往後多少位元組取決於`ptr`指向物件的型別。
然而這麼做有可能會產生迷途指標（dangling pointer，又稱懸空指標、野指標），表示指標儲存的位址指向的東西是無效的，就好像迷途了一樣。

所謂無效就是像下面的範例這樣：

<pre>
<span class="token keyword">#include</span> <span class="token string">&lt;iostream&gt;</span>

<span class="token keyword">int</span> <span class="token function">main</span>() {
    <span class="token keyword">int</span> i = <span class="token number">0</span>;
    <span class="token keyword">int</span>* ptr = &amp;i;
    <span class="token namespace">std</span>::<span class="token gvariable">cout</span> << *(ptr + 1);
    
    <span class="token keyword">return</span> <span class="token number">0</span>;
}
</pre>

問題出在，`ptr + 1`代表`ptr`後面一個位址，然而後面是什麼東西？

### 指標的指標

指標是一個物件，有自己的記憶體位置，當然可以有指向指標的指標，如`int**`是指向一個「指向一個`int`的指標」的指標。
如果說`*`表示指標，用英語從右往左唸的話便是「pointer to pointer to `int`」。

### 指標的參考

雖然參考不是一個物件，因此沒有參考的指標，但指標是一個物件當然也可以有繫結到指標的參考，也就是如`int*&`的東西，由右往左唸是「reference to pointer to `int`」。

### 空指標

如果一個指標不指向任何東西，或者說指向「沒有東西」，可以使用字面值`nullptr`，這個特殊的值可以隱式轉換成任何型別的指標。
如此一來，便可以用`if (ptr)`等方式來檢查，而不會有未定義的指標的問題。

嘗試從「沒有東西」取值是未定義行為。

## 陣列

陣列是一種使用一個變數來存取多個物件的方式，也就是說，可以只用一個陣列變數來表示一連串同型別的資料，而不用多個變數。

```cpp
int arr[3]; // `arr`有3個整數元素。
```

如果有初始化，也可以讓編譯器自行推導陣列長度：

```cpp
int arr[] = {10, 20, 30}; // `arr`的長度為3。
```

然而傳統陣列也有許多缺點，例如無法一次存取整個陣列：

```cpp
int a[] = {10, 20, 30};
int b[] = a;            // 錯誤。
a = {50, 60, 70};       // 錯誤。
```

要存取陣列中的元素，可以使用下標運算子（subscript operator）`[]`。
值得注意的是索引（index）是從0開始的。

```cpp
std::cout << arr[0];
```

---

版權所有 (c) 2022 Luminous-Coder  
所有內容在 [CC「姓名標示—非商業性—同方式分享」4.0 國際公眾授權條款](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode.zh-Hant) 下提供。

{%hackmd @Luminous-Coder/dark-theme %}

[^CLion]: CLion需要付費，但如果你是學生便可以申請教育方案，免費使用JetBrains的各種IDE。