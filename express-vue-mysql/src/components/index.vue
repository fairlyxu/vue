<template>
	<div>
		<h4>宣讲会</h4>
		<ul>

			<li>
				<span>姓名：</span>
				<input type="text" class="form-control" name="userName" id="userName" placeholder="请输入您的姓名" />
			</li>
			<li>
				<span>专业：</span>
				<input type="text" class="form-control" name="major" id="major" placeholder="请输入您的专业名称" />
			</li>
			<li>
				<span>学校：</span>
				<input type="text" class="form-control" name="school" id="school" placeholder="请输入您的学校名称" />
			</li>
			<li>
				<span>手机：</span>
				<input type="text" class="form-control" name="telephone" id="telephone" placeholder="请输入您的手机号码" />
			</li>

			<li class="onlineApply">
				<label for="onlineApply">是否已经网申：</label>
				<!--<input type="checkbox" id="onlineApply" name="onlineApply" checked/>-->
				<div>
					<span id="">是</span><input type="radio" name="onlineApply" value="true" checked="checked" />
				</div>
				<div>
					<span id="">否</span><input type="radio" name="onlineApply" value="false" />
				</div>

			</li>

			<li id="httpAddress">
				<span>http://zhaopin.hi-target.com.cn/</span>
			</li>
			<li>
				<span>宣讲地址:</span>
				<select id="address" class="form-control">
					<!--<option value="山东科技大学">山东科技大学</option>
					<option value="中国石油大学（华东）">中国石油大学（华东）</option>
					<option value="中国海洋大学">中国海洋大学</option>
					<option value="山东建筑大学">山东建筑大学</option>
					<option value="山东交通学院">山东交通学院</option>
					<option value="天津城建大学">天津城建大学</option>
					<option value="华北理工大学">华北理工大学</option>
					<option value="北京建筑大学">北京建筑大学</option>
					<option value="华北科技学院">华北科技学院</option>
					<option value="哈尔滨工程大学">哈尔滨工程大学</option>
					<option value="桂林电子科技大学">桂林电子科技大学</option>
					<option value="桂林理工大学">桂林理工大学</option>
					<option value="中南大学">中南大学</option>
					<option value="长沙理工大学">长沙理工大学</option>
					<option value="中南林业科技大学">中南林业科技大学</option>
					<option value="湖南科技大学">湖南科技大学</option>
					<option value="东华理工大学">东华理工大学</option>
					<option value="南昌工程学院">南昌工程学院</option>
					<option value="江西理工大学">江西理工大学</option>
					<option value="赣南师范大学">赣南师范大学</option>
					<option value="昆明理工大学">昆明理工大学</option>
					<option value="西南林业大学">西南林业大学</option>
					<option value="贵州大学">贵州大学</option>
					<option value="贵州师范大学">贵州师范大学</option>
					<option value="西南交通大学">西南交通大学</option>
					<option value="西南石油大学">西南石油大学</option>
					<option value="成都理工大学">成都理工大学</option>
					<option value="甘肃农业大学">甘肃农业大学</option>
					<option value="兰州交通大学博文学院">兰州交通大学博文学院</option>
					<option value="兰州理工大学技术工程学院">兰州理工大学技术工程学院</option>
					<option value="武汉大学">武汉大学</option>
					<option value="中国地质大学">中国地质大学</option>
					<option value="中国矿业大学">中国矿业大学</option>
					<option value="南京师范大学">南京师范大学</option>
					<option value="南京信息工程大学">南京信息工程大学</option>
					<option value="南京工业大学">南京工业大学</option>
					<option value="华南师范大学">华南师范大学</option>
					<option value="广东工业大学">广东工业大学</option>
					<option value="广州大学">广州大学</option>
					<option value="长安大学">长安大学</option>
					<option value="西安科技大学">西安科技大学</option>
					<option value="太原理工大学">太原理工大学</option>
					<option value="山西工程技术学院">山西工程技术学院</option>
					<option value="河南理工大学">河南理工大学</option>
					<option value="黄河水利职业技术学院">黄河水利职业技术学院</option>
					<option value="郑州水利水电大学">郑州水利水电大学</option>
-->				</select>
			</li>
			<li>
				<button class="btn" id="reset" @click="reset">重置</button>
				<button class="btn btn-primary" id="sendBtn" @click="send">提交</button>
			</li>

		</ul>
	</div>
</template>

<script>
	export default {
		methods: {
			send() {
				debugger;
				var $this = this;
				if($("#userName").val() === "") {
					alert("姓名不可为空，请重新输入");
					return;
				};
				if($("#major").val() === "") {
					alert("专业名称不可为空，请重新输入");
					return;
				};
				if($("#school").val() === "") {
					alert("学校名称不可为空，请重新输入");
					return;
				};
				if($("#telephone").val() === "") {
					alert("电话号码不可为空，请重新输入");
					return;
				}
				if(!(/^1[34578]\d{9}$/.test($("#telephone").val()))) {
					alert("手机号码格式有误，请重新输入");
					return;
				}
				var data = {};
				data["userName"] = $("#userName").val();
				data["major"] = $("#major").val();
				data["school"] = $("#school").val();
				data["telephone"] = $("#telephone").val();
				data["onlineApply"] = $("input[name='onlineApply']:checked").val();
				data["address"] = $("#address").val();
				var time = new Date().Formate("yyyy-MM-dd HH:mm:ss");
				data["time"] = time;
				//alert(JSON.stringify(data));
				data = JSON.stringify(data)

				$.post("api/add", {
						data: data
					}, function(result, textStatus, jqXHR) {
						console.log(typeof result);
						var bool = result.ok;
						if(bool) {
							alert(result.message);
							if($("input[name='onlineApply']:checked").val() === "true") {
								setTimeout(function() {
									$this.$router.push("/ok")
									document.title = "我刚刚参加了【中海达宣讲会】"
								}, 1000)
							} else {
								setTimeout(function() {
									window.location.href = "http://zhaopin.hi-target.com.cn/";
								}, 1000)

							}

						} else {
							alert(result.message)
						}
					}

				)

			},
			reset() {
				$("#userName").val("")
				$("#major").val("");
				$("#telephone").val("");
				$("#school").val("");
			}
		},
		mounted() {
			$.get("static/data/school.json", function(result, textStatus, jqXHR) {
				if(textStatus === "success") {
					for(var i = 0; i < result.length; i++) {
						$("<option/>").text(result[i].name).val(result[i].name).appendTo($("#address"));
					}

				} else {
					alert("您访问的文件不存在");
				}
			})
		}
	}
</script>

<style scoped="scoped">
	h4 {
		text-align: center;
		padding-top: 50px;
		padding-bottom: 20px;
		color: #0012ffd1;
	}
	
	ul {
		padding-left: 20px;
		padding-right: 20px;
		;
	}
	
	li {
		list-style: none;
		display: box;
		/* OLD - Android 4.4- */
		display: -webkit-box;
		/* OLD - iOS 6-, Safari 3.1-6 */
		display: -moz-box;
		/* OLD - Firefox 19- (buggy but mostly works) */
		display: -ms-flexbox;
		/* TWEENER - IE 10 */
		display: -webkit-flex;
		/* NEW - Chrome */
		display: flex;
		margin-bottom: 10px;
		margin-right: 20px;
	}
	
	li>button {
		width: 30%;
		margin: 0 10%;
	}
	
	li>span,
	li>label {
		/*flex: 0 0 120px;
				width: 120px;*/
		height: calc(2.25rem + 2px);
		padding: 0.375rem 0.75rem;
		font-size: 1rem;
		line-height: 1.5;
		display: inline-block;
	}
	
	li>div {
		line-height: 38px;
		height: 38px;
		margin-right: 20px;
	}
	
	li>div>span {
		padding-right: 10px;
	}
	
	.form-control {
		display: inline-block;
		-webkit-box-flex: 1;
		/* OLD - iOS 6-, Safari 3.1-6 */
		-moz-box-flex: 1;
		/* OLD - Firefox 19- */
		/* For old syntax, otherwise collapses. */
		-webkit-flex: 1;
		/* Chrome */
		-ms-flex: 1;
		/* IE 10 */
		flex: 1;
		/* NEW, Spec - Opera 12.1, Firefox 20+ */
	}
	
	input[type="checkbox"] {
		display: inline-block;
		height: 30px;
		line-height: 30px;
		font-size: 30px;
		flex: 0.5;
		margin: 0.375rem 0.75rem;
	}
	
	li:last-child {
		margin-top: 30px;
	}
	
	.onlineApply {
		margin-bottom: 0;
	}
	
	#httpAddress {
		display: none;
	}
</style>