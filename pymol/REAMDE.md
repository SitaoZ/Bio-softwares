## PyMOL 


## AlphaFold3
AlphaFold3预测的蛋白质之间的互作，使用PyMOL进行查看[example](https://www.bilibili.com/video/BV1Qt8iesE4e/?vd_source=16694f427952f2c01f3659ee0722320a)


- step 1  AlphaFold3预测   
AlphaFold3 预测互作，产生cif文件，一般选择model_0.cif(互作效果最好的)

- step 2  导入文件  
PyMOL导入cif文件，更改背景色 `Display` -> `Background` -> `White`

- step 3 更名和改色   
`Mouse` -> `Selection Mode` -> `Chains`
点选其中任意一条蛋白质链，选择之后，进行更名 `A` -> `rename selection` ,输入自己蛋白质的名字，紧接着改色`C` -> `color` -> `blue` (任意选一色)
将图层的状态变成非选；接着点击第二条链，重复 `A` -> `rename selection`，输入自己蛋白质的名字，紧接着改色`C` -> `color` -> `cyans` -> `cyan` (任意选一色)

- step 4 选择氢键
对任意（蛋白链二选一）图层操作即可，`A` -> `Find` -> `polar contacts` -> `to other atoms in object`
出现淡黄色的小棒，即氢键；接着标出氢键，首先显示出棍状结构，点击其中一个蛋白质的图层，选`S` -> `show sticks`，
接着选第二个蛋白图层，选`S` -> `show sticks`；然后将Chanins变成氨基酸残基Residuals, `Mouse` -> `Selection Mode` -> `Residuals`
;接着，放大，调整位置，选择氢键连接的末端的残基，放大缩小仔细查看，标记全部的氢键。最后隐藏两者的棍棒结构，`H` -> `hide sticks`, 两个图层均完同样的`hide sticks`;
发现Cartoon结构干扰视觉判断，选择`Setting` -> `Transparency` -> `Cartoon` -> `80%`,将透明度设为80%。选择氢键那个图层，选择`S` -> `sticks`

- step 5 标记位点
选择氢键图层，`L` -> `residuals`; 点击编辑操作`3-Button Viewing` -> `3-Button Editing`, 按住`Ctrl`键，长按鼠标左键可以对标签进行拖拉操作，
`Ctrl + z`取消操作。移动好之后，可以添加连接线`Setting` -> `Label` -> `Show Connectors`,这时候互作位点图片就做好了

- step 6 图片保存
全局图，局部图，变化角度保存即可




