response2=await fetch(newUrl,{
	method:'POST',
	mode:"cors",
	headers:{
		"Content-Type": "application/json; charset=UTF-8",
		Accept: 'application/json, text/javascript, */*',
		"Authorization":"Bearer "+token,
	},
	body:JSON.stringify({...data,sign}),

});

newResult=await response2.json();

content-type==json==>body以json格式提交
authorization

#### 跨域：
mode：cors 后端要进行相应配置，
简单请求：
	get、post、head 请求类型
		不要设置列表之外的header（如： user-agent）
	Content-Type 只能是：
	application/x-www-from-urlencoded
	multipart/from-data
	text/plain

非简单请求的CORS请求，会在正式通信之前，增加一次HTTP查询请求，称为"预检"请求（preflight）method==options。

浏览器先询问服务器，当前网页所在的域名是否在服务器的许可名单之中，以及可以使用哪些HTTP动词和头信息字段。只有得到肯定答复，浏览器才会（自动）发出正式的XMLHttpRequest请求，否则拦截请求。

cors请求时，getResponseHeader()只能获得6个基本字段，其余自定义头必须通过Access-Control-Expose-Headers指定。