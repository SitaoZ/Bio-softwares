## PyMOL 

## PyMol概述
- Pymol名字的来源：“Py”表示该软件基于python计算机语言，“Mol”则是英文分子（molecule）的缩写，表示该软件用来显示分子结构
- 主要功能：创作高品质的小分子或是生物大分子（特别是蛋白质）的三维结构图像
- 软件的作者宣称，在所有正式发表的科学文献中的蛋白质结构图像中，有四分之一是使用PyMOL来制作
- 网站：http://www.pymol.org/
- DOC: https://pymol.org/dokuwiki/doku.php?id=command:zoom

### PyMol 语法

- Action
- Show
- Hide
- Label
- Color

### PymMol 操作

- 显示所有残基编号
```bash
# 为每个氨基酸的α碳（CA）位置标记上该残基的编号
label name CA, resi

# 去除编号
label name CA, ""
```

- 选择选定的残基
鼠标单击残基，在sele栏目选择L，选择residual


- 显示亲水和疏水氨基酸
```bash
# 疏水氨基酸有9个：Gly,Ala,Val,Leu,Ile,Pro,Phe,Met,Trp
# 非电极性（亲水）氨基酸有6个：Ser,Thr,Cys,Asn,Gln,Tyr
# 命令行输入如下命令
color yellow, resn Gly+Ala+Val+Leu+Ile+Pro+Phe+Met+Trp
as sphere, resn Gly+Ala+Val+Leu+Ile+Pro+Phe+Met+Trp
as sphere,   resn Ser+Thr+Cys+Asn+Gln+Tyr+Asp+Glu+Arg+Lys+His
color blue,  resn Ser+Thr+Cys+Asn+Gln+Tyr+Asp+Glu+Arg+Lys+His
```

- 移动标签  
将模式切换至3-Button Editing, 按住Ctrl， 鼠标拖动标签字符即可

- 切换白色背景  
Display -> Background -> White

- 显示序列
File -> Get PDB -> PDB ID : 1gtf -> Download
点击SEQ显示序列

- 放大缩小 （Zoom In/Out）  
单击鼠标左键，按住Ctrl, 滚动鼠标滑轮。
```bash
zoom  
zoom complete=1 
zoom 142/, animate=3 
zoom (chain A) 
```

- 显示表面   
show -> surface
Setting -> Transparency -> Surface -> 80%

- 发表模式   
Action -> present -> publication


### AlphaFold3
AlphaFold3预测的蛋白质之间的互作，使用PyMOL进行查看[example](https://www.bilibili.com/video/BV1Qt8iesE4e/?vd_source=16694f427952f2c01f3659ee0722320a)


- step 1  AlphaFold3预测   
[AlphaFold3](https://alphafoldserver.com/) 预测互作，产生cif文件，一般选择model_0.cif(互作效果最好的)

- step 2  导入文件  
[PyMOL](https://pymol.org/)导入cif文件，更改背景色 `Display` -> `Background` -> `White`

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



### 查看AlphaFold3预测的两个蛋白质互作结果
[refer](https://zhuanlan.zhihu.com/p/662394976)

- 1.打开名字为0.cif的文件,点击右侧的S按钮可以改变显示的模式  
- 2.菜单栏Displaced->sequence，显示sequence  
- 3.在命令行键入命令，修改链的颜色（如果是两条蛋白序列，默认的名称是A和B）
```bash
sele Chain A                   #select Chain A
set_name sele,seleA            #rename Chain A

sele Chain B                   #select Chain B
set_name sele,seleB            #rename Chain B    
```
之后，右侧面板会增加两个object，seleA，seleB    
点击C按钮，更改seleA和seleB的颜色，分别改为green和blue  

- 4.查看互作区域
下载这个脚本保存到本地，命名为InterfaceResidues.py  
```bash
from pymol import stored
 
def interfaceResidues(cmpx, cA='c. A', cB='c. B', cutoff=1.0, selName="interface"):
	"""
	interfaceResidues -- finds 'interface' residues between two chains in a complex.
 
	PARAMS
		cmpx
			The complex containing cA and cB
 
		cA
			The first chain in which we search for residues at an interface
			with cB
 
		cB
			The second chain in which we search for residues at an interface
			with cA
 
		cutoff
			The difference in area OVER which residues are considered
			interface residues.  Residues whose dASA from the complex to
			a single chain is greater than this cutoff are kept.  Zero
			keeps all residues.
 
		selName
			The name of the selection to return.
 
	RETURNS
		* A selection of interface residues is created and named
			depending on what you passed into selName
		* An array of values is returned where each value is:
			( modelName, residueNumber, dASA )
 
	NOTES
		If you have two chains that are not from the same PDB that you want
		to complex together, use the create command like:
			create myComplex, pdb1WithChainA or pdb2withChainX
		then pass myComplex to this script like:
			interfaceResidues myComlpex, c. A, c. X
 
		This script calculates the area of the complex as a whole.  Then,
		it separates the two chains that you pass in through the arguments
		cA and cB, alone.  Once it has this, it calculates the difference
		and any residues ABOVE the cutoff are called interface residues.
 
	AUTHOR:
		Jason Vertrees, 2009.		
	"""
	# Save user's settings, before setting dot_solvent
	oldDS = cmd.get("dot_solvent")
	cmd.set("dot_solvent", 1)
 
	# set some string names for temporary objects/selections
	tempC, selName1 = "tempComplex", selName+"1"
	chA, chB = "chA", "chB"
 
	# operate on a new object & turn off the original
	cmd.create(tempC, cmpx)
	cmd.disable(cmpx)
 
	# remove cruft and inrrelevant chains
	cmd.remove(tempC + " and not (polymer and (%s or %s))" % (cA, cB))
 
	# get the area of the complete complex
	cmd.get_area(tempC, load_b=1)
	# copy the areas from the loaded b to the q, field.
	cmd.alter(tempC, 'q=b')
 
	# extract the two chains and calc. the new area
	# note: the q fields are copied to the new objects
	# chA and chB
	cmd.extract(chA, tempC + " and (" + cA + ")")
	cmd.extract(chB, tempC + " and (" + cB + ")")
	cmd.get_area(chA, load_b=1)
	cmd.get_area(chB, load_b=1)
 
	# update the chain-only objects w/the difference
	cmd.alter( "%s or %s" % (chA,chB), "b=b-q" )
 
	# The calculations are done.  Now, all we need to
	# do is to determine which residues are over the cutoff
	# and save them.
	stored.r, rVal, seen = [], [], []
	cmd.iterate('%s or %s' % (chA, chB), 'stored.r.append((model,resi,b))')
 
	cmd.enable(cmpx)
	cmd.select(selName1, None)
	for (model,resi,diff) in stored.r:
		key=resi+"-"+model
		if abs(diff)>=float(cutoff):
			if key in seen: continue
			else: seen.append(key)
			rVal.append( (model,resi,diff) )
			# expand the selection here; I chose to iterate over stored.r instead of
			# creating one large selection b/c if there are too many residues PyMOL
			# might crash on a very large selection.  This is pretty much guaranteed
			# not to kill PyMOL; but, it might take a little longer to run.
			cmd.select( selName1, selName1 + " or (%s and i. %s)" % (model,resi))
 
	# this is how you transfer a selection to another object.
	cmd.select(selName, cmpx + " in " + selName1)
	# clean up after ourselves
	cmd.delete(selName1)
	cmd.delete(chA)
	cmd.delete(chB)
	cmd.delete(tempC)
	# show the selection
	cmd.enable(selName)
 
	# reset users settings
	cmd.set("dot_solvent", oldDS)
 
	return rVal
 
cmd.extend("interfaceResidues", interfaceResidues)
```
点击菜单栏file->run script -> InterfaceResidues.py, 运行脚本。    
之后，在命令行键入命令(your_projec_name替换成你的projectname)    
这里换成fold_2025_04_12_14_54_ampka_hspa9   
```bash
interfaceResidue your_projec_name, Chain A, Chain B
```
之后，右侧面板多了一个interface object, 这个里面是互作区域。  
修改个interface object的颜色为red, 可以看到红色的为互作区域    

修改显示模式，点击all->H->hide everything，all->S->sticks  
或者
修改显示模式，点击all->H->hide everything，all->S->spheres, 红色为互作区域   
在sequence panel可以看到具体哪些氨基酸互作（红色的为互作氨基酸）   

- 5.查看极性共价键     
修改显示模式为sticks，点击all->H->hide everything，all->S->sticks  

点击其中一条链的A->find->polor contacts->to any atoms, 可以看查看极性键，  

点击S->lables, 可以显示共价键的键长，单位是Å。  
