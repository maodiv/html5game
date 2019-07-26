
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<title>Draw a rectangle!</title>
</head>

<body>

<style>
		body{
			margin:0px;
			padding:0px;
		}
		
		/*定义滚动条高宽及背景 高宽分别对应横竖滚动条的尺寸*/
		::-webkit-scrollbar
		{
			width: 6px;
			height: 6px;
			background-color: #F5F5F5;
		}
		/*定义滚动条轨道 内阴影+圆角*/
		::-webkit-scrollbar-track
		{
			-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
			border-radius: 10px;
			background-color: #F5F5F5;
		}
		/*定义滑块 内阴影+圆角*/
		::-webkit-scrollbar-thumb
		{
			border-radius: 10px;
			-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,.3);
			background-color: #555;
		}
	  
		.selection{
			display:inline-block;
			position:fixed;
			
		}
/*		.selection:hover .selection-options{
			display:block;
		}*/
		.selection-btn-arrow-hover{
			float: right;
			display: inline;
			position: relative;
			content: "";
			margin: 0px 0px 0px 4px;
			border-width: 5px;
			border-style: solid;
			top: 1px;
			border-color: transparent transparent #949494 transparent;
		}
		.selection .selection-btn{
			position: relative;
			display: inline-block;
			background-color: #f1f1f1;
			cursor: pointer;
			border: 1px solid #d2d1d1;
			text-align: center;
			font-size: 12px;
			padding: 2px 2px;
			vertical-align: middle;
		}
		.selection .selection-btn:focus{
			outline: none;
		}
		.selection .selection-btn p{
			float:left;
			margin:0px;
			padding:0px;
		}
		.selection-btn-arrow{
			float: right;
			display: inline;
			position: relative;
			content: "";
			top: 5px;
			margin: 0px 0px 0px 4px;
			border-width: 5px;
			border-style: solid;
			border-color: #949494 transparent transparent transparent;
		}
		.selection .selection-options{
			/*display: none;*/
			position: absolute;
			background-color: #f9f9f9;
			box-shadow: 3px 3px 9px 5px rgba(0,0,0,0.2);
			min-width: 110px;
			max-height: 300px;
			overflow: auto;
			font-size: 13px;
		}
		.selection .selection-options a{
			cursor: pointer;
			display: block;
			padding: 1px 2px;
		}
		.selection .selection-options a:not(:last-child){
			border-bottom:1px solid #d2d1d1;
		}
		.selection .selection-options a:hover{
			background-color:#848181;
			color:#f1f1f1;
		}
		.selection .selection-options a:active{
			background-color:black;
		}

.tag_select{
    width: 50px;
    height: 20px;
    background-color: red;
    display: inline-block;
    position: fixed;
}
</style>

<div id="canvasDiv" style="
	position:fixed;
	width:100%;
	height:100%;
	display:flex;
	align-items:center;
	justify-content:center;
	overflow:auto;
	">
	<div style="
	">
		<canvas id="canvas" style="cursor: crosshair;"></canvas>
	</div>
</div>

<script>
	initDraw(document.getElementById('canvas'));
	function initDraw(canvas) {
      canvas.style.display='none';
      var mouse = {
          x: 0,
          y: 0,
          startX: 0,
          startY: 0,
          press: -1
        },
        //,canvasDiv = document.getElementById('canvasDiv')
        cvMap = {},
        cvHoverKey = null,
        cvHoverKeys = [],
        CanvasRect = function CanvasRect(startX, startY, endX, endY) {
          this.startX = startX;
          this.startY = startY;
          this.endX = endX;
          this.endY = endY;
          this.isHover = false;
        },
        ctx = null,
        img = new Image(),
        //imgPath = "https://static.runoob.com/images/mix/paris.jpg";
        imgPath = "https://static.runoob.com/images/demo/demo4.jpg";
      img.onload = function() {
        console.log(" img onload ");
        canvas.style.display='block';
        canvas.getContext("2d").clearRect(0, 0, canvas.width, canvas.height);
        canvas.width = img.width;
        canvas.height = img.height;
        const pWidth = canvas.parentNode.offsetWidth;
        const pHeight = canvas.parentNode.offsetHeight;
        if (canvas.height > pHeight) {
          canvas.setAttribute("style", "box-shadow:4px 4px 8px 4px #9e9e9e;");
        } else {
          canvas.setAttribute(
            "style",
            "box-shadow:4px 4px 8px 4px #9e9e9e;position: absolute;top: 0;bottom: 0;left: 0;right: 0;margin: auto;"
          );
        }
        ctx = canvas.getContext("2d");
        var bg = ctx.createPattern(img, "no-repeat");
        ctx.fillStyle = bg;
        ctx.fillRect(0, 0, img.width, img.height);
        draw();
      }
      function setMousePosition(ev, thi, startState) {
        //mouse.x = ev.pageX - thi.offsetLeft - canvasDiv.offsetLeft;
        //mouse.y = ev.pageY - thi.offsetTop - canvasDiv.offsetTop;
        mouse.x =
          ev.pageX -
          thi.offsetLeft -
          thi.offsetParent.offsetLeft +
          thi.parentNode.scrollLeft;
        mouse.y =
          ev.pageY -
          thi.offsetTop -
          thi.offsetParent.offsetTop +
          thi.parentNode.scrollTop;
        if (startState == 0) {
          mouse.startX = null;
          mouse.startY = null;
        } else if (startState == 1) {
          mouse.startX = mouse.x;
          mouse.startY = mouse.y;
        }
      }

      function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        var bg = ctx.createPattern(img, "no-repeat");
        ctx.fillStyle = bg;
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.strokeStyle = "red";
		var z_i = 0;
        for (var key in cvMap) {
          var ele = cvMap[key];
          ctx.strokeStyle = key != null && key == cvHoverKey ? "yellow" : "red";
          ctx.strokeRect(
            ele.startX,
            ele.startY,
            ele.endX - ele.startX,
            ele.endY - ele.startY
          );
          if(key == 'live') {
            continue;
          }
			var options = [
				{id:1, name:'optops1'},
				{id:2, name:'optops2'},
				{id:3, name:'optops3'},
				{id:4, name:'optops4'}
			]
			var position = {
				x:(ele.startX > ele.endX ? ele.startX : ele.endX) - canvas.parentNode.scrollLeft + canvas.offsetParent.offsetLeft + canvas.offsetLeft + 10 + 'px',
				y:(ele.startY < ele.endY ? ele.startY : ele.endY) - canvas.parentNode.scrollTop + canvas.offsetParent.offsetTop + canvas.offsetTop + 'px'};
			var selecs = createSelection(key, position, options, null, 10000+z_i);
			z_i++;
		}
      }
	  
		function createSelection(idKey, pos, options, value, zIndex) {
		  var selection = document.getElementById('tag_select_' + idKey);
          if(selection == null) {
			var tag_select = document.getElementById('tag_select');
			if(tag_select == null) {
				tag_select = document.createElement('div')
				tag_select.id = 'tag_select';
				document.body.appendChild(tag_select);
			}

			selection = document.createElement('div')

			var selection_btn = document.createElement('div')
			selection_btn.className = 'selection-btn';
			selection_btn.addEventListener('click',function(){
					this.nextElementSibling.style.display = this.nextElementSibling.style.display == 'none' ? 'block' : 'none'
				},false);
			var p = document.createElement('p')
			p.innerHTML = "标签";
			selection_btn.appendChild(p);
			var selection_btn_arrow = document.createElement('div')
			selection_btn_arrow.className = 'selection-btn-arrow';
			selection_btn.appendChild(selection_btn_arrow);

			var selection_options = document.createElement('div')
			selection_options.className = 'selection-options';
			selection_options.style.display = 'none';
			for(var i in options){
				var a = document.createElement('a')
				a.dataset.id = options[i].id;
				a.innerHTML = options[i].name;
				if(value != null && value == options[i].id) {
					selection.dataset.value = a.dataset.id;
					p.innerHTML = options[i].name;
					a.style.backgroundColor = "#353535";
					a.style.color = "white";
				}
				a.addEventListener('click',function(){
					this.parentNode.parentNode.firstElementChild.firstElementChild.innerHTML = this.innerHTML;
					this.parentNode.parentNode.dataset.value = this.dataset.id;
					var childrens = this.parentNode.children;
					for(var j =0; j<childrens.length; j++) {
						childrens[j].style.backgroundColor = "#f1f1f1";
						childrens[j].style.color = "black";
					}
					this.style.backgroundColor = "#353535";
					this.style.color = "white";
					this.parentNode.style.display = 'none';
				},false);
				selection_options.appendChild(a);
			}
            
            selection.id = 'tag_select_' + idKey;
            selection.className = 'selection';
			selection.style.zIndex = zIndex;
			selection.addEventListener('mouseleave',function(){
				this.lastElementChild.style.display = 'none';
			},false);
			selection.appendChild(selection_btn);
			selection.appendChild(selection_options);
            tag_select.appendChild(selection);
          }
			selection.style.left = pos.x;
			selection.style.top = pos.y;
			return selection;
		}

		function removeSelection(id) {
			var tag_remove = document.getElementById(id);
			if(tag_remove != null) {
				tag_remove.parentNode.removeChild(tag_remove);
			}
		}

      img.src = imgPath;

      canvas.oncontextmenu = function(e) {
        return false;
      };

      canvas.onmousedown = function(e) {
        console.log("onmouseDown");
        mouse.press = e.button;
        setMousePosition(e, this, 1);
        console.log(e.button);
        if (e.button == 0) {
          console.log("鼠标左击了");
          if (cvHoverKey != null) {
          } else {
            cvMap["live"] = new CanvasRect(mouse.x, mouse.y, mouse.x, mouse.y);
          }
        } else if (e.button == 1) {
          console.log("鼠标中建了");
        } else if (e.button == 2) {
          console.log("鼠标右击了");
		  removeSelection("tag_select_" + cvHoverKey);
          delete cvMap[cvHoverKey];
          draw();
        }
      };
      canvas.onmouseup = function(e) {
        console.log("onmouseup");
        mouse.press = -1;
        setMousePosition(e, this, 0);
        if (cvMap["live"] != null) {
          if (
            Math.abs(cvMap["live"].startX - cvMap["live"].endX) >= 10 &&
            Math.abs(cvMap["live"].startY - cvMap["live"].endY) >= 10
          ) {
            cvMap[new Date().getTime()] = Object.assign({}, cvMap["live"]);
          }
          delete cvMap["live"];
        }
      };
      canvas.onmousemove = function(e) {
        var origX = mouse.startX;
        var origY = mouse.startY;
        setMousePosition(e, this, 1);
        var prec = 8;
        var hovered = false;
        for (var key in cvMap) {
          if (
            hovered ||
            mouse.press == 0 ||
            mouse.press == 1 ||
            mouse.press == 2
          ) {
            break;
          }
          cvHoverKeys = [];
          var ele = cvMap[key];
          if (
            mouse.y >= (ele.startY > ele.endY ? ele.endY : ele.startY) + prec &&
            mouse.y <= (ele.startY > ele.endY ? ele.startY : ele.endY) - prec
          ) {
            if (
              (mouse.x > ele.startX - prec && mouse.x < ele.startX + prec) ||
              (mouse.x > ele.endX - prec && mouse.x < ele.endX + prec)
            ) {
              canvas.style.cursor = "w-resize";
              hovered = true;
              cvHoverKey = key;
              if (mouse.x > ele.startX - prec && mouse.x < ele.startX + prec) {
                if (cvHoverKeys.indexOf("startX") < 0)
                  cvHoverKeys.push("startX");
              } else {
                if (cvHoverKeys.indexOf("endX") < 0) cvHoverKeys.push("endX");
              }
            }
          } else if (
            mouse.x >= (ele.startX > ele.endX ? ele.endX : ele.startX) + prec &&
            mouse.x <= (ele.startX > ele.endX ? ele.startX : ele.endX) - prec
          ) {
            if (
              (mouse.y > ele.startY - prec && mouse.y < ele.startY + prec) ||
              (mouse.y > ele.endY - prec && mouse.y < ele.endY + prec)
            ) {
              canvas.style.cursor = "n-resize";
              hovered = true;
              cvHoverKey = key;
              if (mouse.y > ele.startY - prec && mouse.y < ele.startY + prec) {
                if (cvHoverKeys.indexOf("startY") < 0)
                  cvHoverKeys.push("startY");
              } else {
                if (cvHoverKeys.indexOf("endY") < 0) cvHoverKeys.push("endY");
              }
            }
          } else if (
            (mouse.x > ele.startX - prec && mouse.x < ele.startX + prec) ||
            (mouse.x > ele.endX - prec && mouse.x < ele.endX + prec)
          ) {
            var x1 = null,
              y1 = null;
            if (mouse.y > ele.startY - prec && mouse.y < ele.startY + prec) {
              y1 = ele.endY;
              if (cvHoverKeys.indexOf("startY") < 0) cvHoverKeys.push("startY");
              if (mouse.x > ele.startX - prec && mouse.x < ele.startX + prec) {
                x1 = ele.endX;
                if (cvHoverKeys.indexOf("startX") < 0)
                  cvHoverKeys.push("startX");
              } else {
                x1 = ele.startX;
                if (cvHoverKeys.indexOf("endX") < 0) cvHoverKeys.push("endX");
              }
            } else if (mouse.y > ele.endY - prec && mouse.y < ele.endY + prec) {
              y1 = ele.startY;
              if (cvHoverKeys.indexOf("endY") < 0) cvHoverKeys.push("endY");
              if (mouse.x > ele.startX - prec && mouse.x < ele.startX + prec) {
                x1 = ele.endX;
                if (cvHoverKeys.indexOf("startX") < 0)
                  cvHoverKeys.push("startX");
              } else {
                x1 = ele.startX;
                if (cvHoverKeys.indexOf("endX") < 0) cvHoverKeys.push("endX");
              }
            }
            if (x1 != null && y1 != null) {
              hovered = true;
              cvHoverKey = key;
              if ((mouse.x - x1) * (mouse.y - y1) > 0) {
                canvas.style.cursor = "nw-resize";
              } else {
                canvas.style.cursor = "ne-resize";
              }
            }
          }
        }

        if (
          !hovered &&
          mouse.press != 0 &&
          mouse.press != 1 &&
          mouse.press != 2
        ) {
          cvHoverKey = null;
          canvas.style.cursor = "crosshair";
        }
        if (!hovered && cvMap["live"] != null) {
          cvMap["live"].endX = mouse.x;
          cvMap["live"].endY = mouse.y;
        } else {
          delete cvMap["live"];
        }
        if (cvHoverKey != null) {
          if (mouse.press == 1) {
            cvMap[cvHoverKey].startX += mouse.x - origX;
            cvMap[cvHoverKey].startY += mouse.y - origY;
            cvMap[cvHoverKey].endX += mouse.x - origX;
            cvMap[cvHoverKey].endY += mouse.y - origY;
          } else if (mouse.press == 0) {
            for (var k in cvHoverKeys) {
              var type = cvHoverKeys[k];

              cvMap[cvHoverKey][type] =
                type.indexOf("X") >= 0 ? mouse.x : mouse.y;
            }
          }
        }
        draw();
      };
    }
	
</script>

</body>
</html>
