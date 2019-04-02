http://game.ioxapp.com/eye-test/game.html 測色弱

setInterval(function(){
	var test = document.querySelectorAll('#box>span');
	for(var i =0 ; i<test.length ; i++)
		test[i].click();
},10)