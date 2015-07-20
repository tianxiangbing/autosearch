# autosearch
自动搜索
例子见[自动搜索框例子](http://www.lovewebgames.com/jsmodule/autosearch.html "自动搜索框例子")
![效果图](example/autosearch.jpg)

#例1：
    <input type="text"  class="autosearch"><input type="hidden" name="hd_id" id="hd_id">
	<script src="../src/jquery-1.11.2.js"></script>
	<script src="../src/autosearch.js"></script>
	<script>
	$.get('data.txt',function(result){
		 var input = $('.autosearch');
		 var autosearch = new AutoSearch();
		 autosearch.init({input:input,autoShow:true,data:result,valueObj:'#hd_id',valueName:"id"});
	},'json')
	</script>
`直接的调用,使用静态固定的数据源`

#例2：
	<!-- ajax请求 -->
	<input type="text"  class="autosearch2">
	<script>
		 var input = $('.autosearch2');
		 var autosearch = new AutoSearch();
		 autosearch.init({input:input ,autoShow:false,data:function(callback){
				$.get('data.txt',{key:input.val()},function(result){
		 		callback(result);
		 		},'json');
	 		}
	 	});
	</script>
` 数据源会变化`
#例3：
	<!-- 多个 -->
	<input type="text"  class="autosearch3">
	<script>
	$.get('data.txt',function(result){
		 var input = $('.autosearch3');
		 var autosearch = new AutoSearch();
		 autosearch.init({input:input,autoShow:false,data:result,mutil:true
		 	});
	},'json')
	</script>

#属性

##input: [DOM]
	输入框,jquery DOM对象
##data:[obj|function]
	数据源，这里可以传入数据源数组，也可以传入一个方法作为回调返回数据，如果传入的是数组，将作为静态过滤筛选，如果是传入的方法，每次都会调用该方法进来过滤。
##autoShow:[bool]
	是否在获得焦点时就显示数据,默认为false
##valueObj:[DOM]
	赋值框，jquery DOM对象
##filterColumn:[array string]
	过滤的字段列，默认为['name'],可以同时对多个数据列过滤
##column:[array string]
	显示的列，默认为['name']，如果想定义显示项，可以配置回调方法format:function(item)来返回显示内容
##mutil:[bool]
	选多个，默认为false
#回调方法
##callback :function(data)
	选中的回调，data为当前选中的数据项.可以用于扩展选中后的显示效果
##focusCallback:function(input)
	获取焦点
##blurCallback:function(input)
	离开焦点
##showCallback:function(input,content)
	显示后的回调