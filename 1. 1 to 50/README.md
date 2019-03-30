#1 to 50

http://zzzscore.com/1to50/en/?ts=1553662600958


```HTML
<a class='resetBtn' id='secretButton'>作弊</a>
```

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


```javascript
var gameBlock = document.querySelectorAll('#grid > div');
var event = new Event('tap');
for(var y=1; y<=50 ; y++)
{
await new Promise((a)=>{
setTimeout(a,100)
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