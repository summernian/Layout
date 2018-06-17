# Layout
### css经典布局
根据DOM结构编写CSS，实现三栏水平布局,中间宽度自适应且优先渲染,left宽200px,right宽300px
```

<div class='container'>
	<div class="main">#主体</div>
	<div class="left">#左边框</div>
	<div class="right">#右边框</div>
</div>

```
	
#### 圣杯布局
 - 设置基本样式，为了高度保持一致分别给三个元素设置最小宽；
```
	.left,.main,.right {
		min-height: 100px;
	}
	.left {
		background: green;
		width: 200px;	
	}
	.main {
		background: blue;
	}
	.right {
		background: red;
		width: 300px;
	}
```
 - 设置父元素container的位置，并在左右分别空出200px和300px区域；
```
	.container {
		padding: 0 300px 0 200px;
	}

```
 - 将主体的三个子元素都设置为左浮动，此时main在最左侧，left居中，right在右；
```
	.left,.main,.right {
		min-hight: 300px;
		float: left;
	}
```
 - 设置main的宽度为100%，让其单独占满一行；
```
	.main {
		background: blue;
		width: 100%;
	}

```
 - 设置left和right的负margin;
> 我们的目标是让left、main、right依次并排，但设置main的宽度为100%后，left和right会被挤到下一行，这里使用的就是margin-left的负属性；
```
	.left {
		margin-left: -100%;
		background: green;
		width: 200px;
	}
	.right {
		margin-left: -300px;
		background: red;
		width: 300px;
	}
```
> 负的margin-left会让元素沿文档流向左移动，如果数值较大就会移动至上一层。设置left的margin-left为-100%，就会使left向左移动一整行的宽度，由于左边是父级元素的边框，所以left会跳到上一行后再进行左移，一直移到上一行的开头。left移动后right就会移动到该行的开头，这时候只要给right设置margin-left的负宽就会移动到上一行的末尾。

 - 此时left和right依然是覆盖在main的主体上方，可使用相对定位，将left和right分别移动到之前container预留的padding位置就可以了；
```
	.left,.main,.right {
		position: relative;
		min-hight: 300px;
		float: left;
	}
	
	.left {
		left: -200px;
		margin-left: -100%;
		background: green;
		width: 200px;
	}
	.right {
		right: -300px;
		margin-left: -300px;
		background: red;
		width: 300px;
	}
```
 - 完整代码见html文件；
