#http://validform.rjboy.cn/ 官方网站
# jquery插件：一行代码搞定整站表单验证！
Validate all the forms through the site just need one line code! <br>

通用表单验证方法<br>
Validform version 5.3.2<br>
For more information, please visit <http://www.rjboy.cn><br>
By sean during April 7, 2010 - April 22, 2011


## 功能介绍：
1、支持一个页面多表单的检测。例如你给页面上的各form绑定同样的class名称“demoform”，只需在页面上写上一句 $(".demoform").Validform()，各表单便会独立检测；<br>
2、两种信息提示效果，一个是元素右侧出现提示信息，一个是弹出信息框。另外还附加了$.Showmsg()、$.Hidemsg()全局弹出/关闭信息框方法以便整站有一个统一的信息提示效果【只要引入了该js文件就能调用这两个全局方法】；<br>
3、指定表单下任一元素在单击时触发表单提交事件；<br>
4、支持ajax提交表单数据，也支持ajax实时反馈验证结果（如常见的用户注册表单下的用户名检测）；<br>
5、支持开启网速慢时的二次提交防御（有时连续的点击提交表单按钮会产生多次的表单提交结果）；<br>
6、可检测多个文本框内容是否一致（例如常见的两次密码输入确认）；<br>
7、囊括11种常见的格式验证形式。<br>

## 使用方法：
<pre>
$(".demoform").Validform({//$(".demoform")指明是哪一表单需要验证,名称需加在from表单上;
	btnSubmit:"#btn_sub", //#btn_sub是该表单下要绑定点击提交表单事件的按钮;如果form内含有submit按钮该参数可省略;
	tiptype:1, //可选项 1=>pop box,2=>side tip，默认为1;
	postonce:true, //可选项 是否开启网速慢时的二次提交防御，true开启，不填则默认关闭;
	ajaxurl:"ajax_post.php", //ajax提交表单数据;
	callback:function(data){
		//返回数据data是json格式，{"info":"demo info","status":"y"}
		//info: 输出提示信息;
		//status: 返回提交数据的状态,是否提交成功。如可以用"y"表示提交成功，"n"表示提交失败，在ajax_post.php文件返回数据里自定字符，主要用在callback函数里根据该值执行相应的回调操作;
		//你也可以在ajax_post.php文件返回更多信息在这里获取，进行相应操作；
			
		//这里执行回调操作;
	}
});
</pre>

## 参数说明： 【所有参数均为可选项】
必须是表单对象执行Validform方法，示例中“.demoform”就是绑定在form元素上的class名称；<br><br>
<strong>btnSubmit：</strong>指定表单下的哪一个按钮触发表单提交事件，如果表单下有submit按钮可以省略。示例中“.btn_sub”是该表单下要绑定点击提交表单事件的按钮，程序会在btnSubmit所在表单下查找该对象;<br><br>
<strong>tiptype：</strong>指定提示效果，可选值 1 | 2, 默认为1。 1=&gt;弹出提示框,2=&gt;表单元素右侧提示；<br><br>
<strong>postonce：</strong>指定是否开启网速慢时的二次提交防御，true开启，不指定则默认关闭；<br><br>
<strong>ajaxurl：</strong>指定处理ajax表单数据的后台文件【表单数据是以POST方式提交】，注意处理完数据后输出Json格式的反馈信息，info值就是表单提交后前台页面所看到的反馈信息。【不传入该参数就会以正常方式提交表单】<br><br>
<strong>callback：</strong>在使用ajax提交表单数据时，数据提交后的回调函数。返回数据data是Json格式，{"info":"demo info","status":"y"}，info: 输出提示信息，status: 返回提交数据的状态,是否提交成功，如可以用"y"表示提交成功，"n"表示提交失败，在ajax_post.php文件返回数据里自定字符，主要用在callback函数里根据该值执行相应的回调操作。你也可以在ajax_post.php文件返回更多信息在这里获取，进行相应操作；<br>


## 怎样给表单元素绑定验证类型？

示例代码：<br>
<pre>
&lt;!--ajax实时验证用户名--&gt;
&lt;input type="text" value="" name="name" datatype="s5-16" ajaxurl="valid.php" nullmsg="请输入用户名！" errormsg="昵称至少5个字符,最多16个字符！" /&gt;

&lt;!--密码--&gt;
&lt;input type="password" value="" name="userpassword" datatype="*6-15" errormsg="密码范围在6~15位之间,不能使用空格！" /&gt;
&lt;!--确认密码--&gt;
&lt;input type="password" value="" name="userpassword2" datatype="*" recheck="userpassword" errormsg="您两次输入的账号密码不一致！" /&gt;

&lt;!--默认提示文字--&gt;
&lt;textarea tip="请在这里输入您的意见。" errormsg="很感谢您花费宝贵时间给我们提供反馈，请填写有效内容！"  datatype="s" altercss="gray" class="gray" name="msg" value=""&gt;请在这里输入您的意见。&lt;/textarea&gt;

&lt;!--单选按钮--&gt;
&lt;input type="radio" value="1" name="gender" id="male" datatype="radio" errormsg="请选择性别！" /&gt;&lt;label for="male"&gt;男&lt;/label&gt;
&lt;input type="radio" value="2" name="gender" id="female" /&gt;&lt;label for="female"&gt;女&lt;/label&gt;

&lt;!--复选框--&gt;
&lt;input name="shoppingsite2" id="shoppingsite21" type="checkbox"  value="1" datatype="checkbox" errormsg="请选择您常去的购物网站！" /&gt;&lt;label for="shoppingsite21"&gt;淘宝网&lt;/label&gt;
&lt;input name="shoppingsite2" id="shoppingsite22" type="checkbox"  value="2" /&gt;&lt;label for="shoppingsite22"&gt;当当网&lt;/label&gt;

&lt;!--下拉框--&gt;
&lt;select name="province" id="province" datatype="select" errormsg="请选择省份！" &gt;&lt;option value=""&gt;--请选择省份--&lt;/option&gt;&lt;option value="1"&gt;江西省&lt;/option&gt;&lt;/select&gt;
</pre>

## 说明：
凡要验证格式的元素均需添加datatype属性，datatype可选值目前有11类，用来指定不同的验证格式【如果还不能满足您的验证需求，可以自行在regcheck方法中添加】。<br>

<strong>datatype：</strong>* | *6-16 | n | s | s6-18 | p | m | e | radio | checkbox | select<br>

*：检测是否有输入，可以输入任何字符，不留空即可通过验证；<br>

*6-16：检测是否为6到16位任意字符；<br>

n：数字类型；<br>

s：字符串类型；<br>

s6-18：6到18位字符串；<br>

p：验证是否为邮政编码；<br>

m：手机号码格式；<br>

e：email格式；<br>

radio：如果要验证的元素为单选框，datatype设置为radio；<br>

checkbox：如果要验证的元素为复选框，datatype设置为checkbox；<br>

select：如果要验证的元素为下拉框，datatype设置为select。<br>

注意radio，checkbox，select的value值为空时不能通过检测，要非空值才能通过。radio和checkbox元素只需给该组的第一个元素绑定datatype属性即可，请参看上面的示例代码。<br>

## 其他的附加属性：
<strong>nullmsg：</strong>是指定没有填入内容时出现的提示信息，不指定默认是“请填入信息！”，另外当datatype为radio、checkbox或select时，因为这三种类型只要为空值就表示出错，提示errormsg所指定信息，所以这三类不需要绑定该属性；<br>

<strong>errormsg：</strong>是指定验证格式不符时出现的提示信息，不指定默认是“请输入正确信息！”；<br>

<strong>ignore：</strong>绑定ignore="ignore"的表单元素，当有输入时会验证所填数据是否符合datatype所指定数据类型（格式不对不能通过验证），当没有输入数据时也可以通过验证；<br>

<strong>recheck：</strong>是用来指定两个表单元素值一致性检测的另外一个对象，赋给它另外一个对象的name属性值即可；<br>

<strong>tip：</strong>是指定表单元素的提示信息;指定后该元素会有focus时提示信息消去，没有输入内容blur时出现提示信息的效果，请参看demo页的“备注”效果；<br>

<strong>altercss：</strong>是指定有tip属性的元素默认提示文字显示时的样式，当该元素focus时程序会把这个样式去掉，blur时如果值为空或者跟提示文字一样则再加上该样式；<br>

<strong>ajaxurl：</strong>指定ajax实时验证的后台文件路径，给需要后台数据库验证信息的对象绑定该属性。注意该文件输出的内容就是前台显示的验证出错的反馈信息，如果验证通过请输出小写字母"y"。后台页面如valid.php文件中可以用 $_POST["param"] 接收到值，Ajax中会POST过来变量param。<br>