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
```HTML
<a class='resetBtn' id='secretButton'>作弊</a>
```

![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.10.png)

```javascript
var secretButton = document.querySelector('#secretButton')
var gameBlock = document.querySelectorAll('#grid > div');

secretButton.addEventListener('click',mySecret)

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

![1 to 50](https://raw.githubusercontent.com/jj811208/htmlGameCheat/master/asset/1.8.gif)



如果我們可以用程式來模擬我們的點擊，不是很好嘛？

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

未完成