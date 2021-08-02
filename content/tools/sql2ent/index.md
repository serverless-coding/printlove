---
title: "在线工具：SQL转entgo schema"
description: "无需下载，在线SQL转entgo schema，粘贴即可生成"
date: 2021-07-20T10:53:56+08:00
type: ext
layout: tools
---
{{< navmain `/tools/sql2ent`>}}
{{< html >}}
<div class="row"> 
  <div class="t-editarea col-lg-5 col-md-12" onpaste="setTimeout(convert,1)"> 
    <label class="col-form-label"> SQL </label> 
    <div id="input" class="t-textarea fullHeight fixed-size"></div> 
  </div>
  <div class="t-btn col-lg-1 col-md-12">
    <button class="btn"  id="btnExpan"> 转换 </button>
    <button class="btn btn-default" data-clipboard-action="copy" data-clipboard-target="#output"> 复制 </button>
    <button class="btn btn-default" onclick="cleanup()"> 清空 </button>

  </div> 
  <div class="t-editarea col-lg-6 col-md-12"> 
    <label class="col-form-label"> entgo schema</label>
    <div class="t-textarea fullHeight fixed-size" id="output"></div> 
</div>

  <script src="https://cdn.bootcss.com/clipboard.js/2.0.4/clipboard.min.js">
	</script> 
  <script src="/js/jquery.js"></script>
  <script src="/js/tools.js"></script>
  <script src="/layer/layer.js"></script>
  <script>
    document.getElementById("btnExpan").onclick = function() {
      convert()
    }

    let input = new highlight(
      document.getElementById("input"), 
      "sql", 
      initSQl
    )

    let output = new highlight(
      document.getElementById("output"), 
      "go", 
      '等待转化结果...'
    )
    
    function convert() {
      let sql = input.getValue()
      if (sql != "") {
        $.ajax({
          url: "/api/sql2ent",
          type: "post",
          data: {
            ddl: sql
          },
          success: function(res) {
            if (res.error != "") {
              layer.alert(res.error)
            } else {
              output.setValue(res.data)
            }
          } 
        })
      }
    }
    convert()
    listenMode(input, output)
	</script>
  {{< /html >}}
  {{< html >}}<div class="tool-info">{{< /html >}}
**说明：**
  
目前项目正处于完善阶段，如果您遇到任何问题，都可在下方留言，我看到都会及时回复，并且改进。


**进入开源：**

经过调研（手动找），市面上这个完善的工具还没有，因此计划将此项目着重开发并且开源，以供大家使用。

项目开源地址：[https://www.github.com/miaogaolin/sql2ent](https://www.github.com/miaogaolin/sql2ent)

{{< html >}}</div>{{< /html >}}