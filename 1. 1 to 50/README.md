# 1 to 50

## 遊戲介紹
![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.1.png)

遊戲網址：[1 to 50](http://zzzscore.com/1to50/en/?ts=1553662600958)

1 to 50 是一個考驗眼明手快的小遊戲，玩法是從數字 1 開始點擊，依照順序一直點到數字 50 ，點完後會出現你這次的點擊所花費的秒數，即為你的成績。

>建議讀者可以先玩玩看這個遊戲，了解遊戲的內容，以便理解稍後要講述的內容。

## 目標
* 實作出類似大家來找碴的提示按鈕
* 達成作弊般的成績


## 關注的知識點
* 什麼是變數
* 資料型態是什麼， number , string 又是什麼
* 如何使用 for 迴圈  
* if 是做什麼用的
* 如何透過 javascript 選取一個 html 的元素
* EventListener是什麼


## 教學

第一次進入遊戲

![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.2.gif)

我經過一番努力，得到的成績為：

![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.3.png)


...

~~這樣下去是不行的，這種成績沒辦法po到facebook炫耀~~

### 思考邏輯

一般來說在撰寫程式的之前，要先思考現在要完成的這個功能，需要怎麼做，如何做，需要什麼樣的資訊才能夠做，我們回顧一下第一個目標：實作出類似大家來找碴的提示按鈕

1 to 50 這款遊戲，是從 1 開始點到 50 ，點完後的數字會消失，我們可以發現，**我們每次要點擊的位置 就是盤上最小的數字**，我們能夠簡單的分析出待會程式的行為

	點擊按鈕 > 找最小的數字 > 對最小數字的格子提示特效

所以我們要做的事情有兩個

	1.在畫面上放一個按鈕
	2.給予這個按鈕，找最小的數字並且顯示提示特效的能力

我們可以開啟開發人員工具來觀察這個遊戲的html

![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.4.png)

首先需要找到可以放按鈕的地方，這邊我發現遊戲中有一個reset按鈕，等等提示的按鈕可以放到它旁邊，按鈕的樣式他都寫好了，可以偷懶一下直接拿他的來用

![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.5.png)

接著再繼續觀察，可以發現整個遊戲盤都被裝在`<div class="grid x5" id="grid">`裡面

![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.6.png)

點開它底下的div就可以看到棋盤上的數字了，

![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.7.png)

其實到了這邊，我們就已經整理出所有我們需要的資訊了，可以開始實作我們的程式碼

### 實作

首先先在開發人員工具上的`<div class="description">`按右鍵，點擊 Edit as HTML 在`<a class="resetBtn" href="javascript:;">Restart</a>`的下方輸入 `<a class='resetBtn' id='secretButton'>作弊</a>`這樣即可在畫面上看到我們的按鈕。
>這一邊的class叫作resetbtn的原因是因為，這樣可以直接偷Restart的按鈕樣式來用，
>而id的功用在這邊只是幫他取名字，等等javascript才方便把提示的能力指定給它。

![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.10.png)
▲成功的話應該會在Restart旁邊看到我們的按鈕

按鈕出來了以後就要開始進到javascript的部分了，首先必須要讓javascript能夠找到按鈕以及遊戲盤上所有的格子，這邊我們可以使用 document.querySelector 以及 document.querySelectorAll 這兩個瀏覽器提供的能力來選擇html上的元素(注意大小寫)

```javascript
var secretButton = document.querySelector('#secretButton')
var gameBlock = document.querySelectorAll('#grid > div');
```

>當你今天只要拿一個東西的時候就用 querySelector ，而你要取得很多東西的時候就用 querySelectorAll 

接著要給予按扭提示的能力，在網頁的世界中，你要在一個東西上做一件事來觸發一個行為的話，就要幫它加上Event Listener

> 一個東西上做一件事來觸發一個行為
> 
> 一個東西：	按鈕
> 一件事：		點擊       
> 一個行為：	提示

這裡的程式碼也很直覺

```javascript
var secretButton = document.querySelector('#secretButton')
var gameBlock = document.querySelectorAll('#grid > div');

secretButton.addEventListener('click',/*提示功能*/)
```

> addEventListener('click',xxxx) 意思就是點擊(click)的時候會觸發xxxx

這樣寫提示功能上去當然是沒有效果的，程式語言沒有這種黑魔法，功能的邏輯要靠我們自己去實作的，這邊我們可以寫入我們之前想要達到的程式行為：找最小的數字並且顯示提示特效

```javascript
var secretButton = document.querySelector('#secretButton')
var gameBlock = document.querySelectorAll('#grid > div');

secretButton.addEventListener('click', mySecret)

function mySecret(){
    var minBlock = null;
    for(var i =0; i<=24; i++)
    {
        if(minBlock==null)
        {
            minBlock = gameBlock[i];
        }

        if(parseInt(gameBlock[i].innerText) < parseInt(minBlock.innerText))
        {
            minBlock = gameBlock[i];
        }
    } 
    minBlock.style.color='red';
    setTimeout(function(){minBlock.style.color='white'},400)
}
```

提示的功能完成！！！

![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.8.gif)

......

完成提示的功能後，才發現分數幾本上完全不會進步。原因是這個遊戲並不像大家來找碴一樣，提示按鈕在這款遊戲其實沒什麼屁用，點提示按鈕的步驟，實在是太拖台錢...

但是既然我們的程式能夠知道現在應該點哪裡，那如果我們可以用程式來模擬我們的點擊，不是就可以很快的通關了嘛？！

可以，只要我們能夠去模擬點擊遊戲格子的動作就很簡單，以下程式碼有興趣的讀者在自行去研究即可。

```javascript
var gameBlock = document.querySelectorAll('#grid > div');
var event = new Event('tap');

for(var y=1; y<=50 ; y++)
{
	await new Promise((a)=>{
		setTimeout(a,100);
	})
 
   for(var i =0; i<=24; i++)
   {
       if(gameBlock[i].innerText==y)
       {
       	gameBlock[i].dispatchEvent(event);
       }
   }
}
```
![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.9.gif)
▲有了這支程式，終於可以分享FB
