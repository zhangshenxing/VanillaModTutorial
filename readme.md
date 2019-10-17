原版模组入门教程
===

1. [简介](#§1-简介)
2. [数据包](§2-数据包)
3. [资源包](§3-资源包)
4. [规划](§4-规划)
5. [合成](§5-合成)
6. [熔炼和酿造](§6-熔炼和酿造)
7. [交易](§7-交易)
8. [探测与触发](§8-探测与触发)
9. [机器实例](§9-机器实例)
10. [ 随机结构](§10-随机结构)
11. [种植](§11-种植)
12. [连锁挖矿](§12-连锁挖矿)
13. [§13 磁力效果](§13-磁力效果)

阅读时请注意内容的适用版本，有任何错误和疑问请联系我，谢谢！

***注意：由于论坛原因，本帖中的代码直接复制可能会有特殊的字符导致无法使用！***

## §1简介
原版模组(vanilla mod)一般指在不修改Minecraft游戏本体的前提下，通过命令方块、一键命令(OOC)、数据包(datapack)、资源包(resourcepack)等方式对游戏的可玩性做出修改。而自Minecraft Java版1.13起的数据包概念问世之后，原版模组的制作已变得十分便捷。然而纵观论坛，原版模组仍然不够繁荣。因此我将为首次接触此概念的玩家做一个简单的入门，以期抛砖引玉。

部分段落常为部分读者所熟知，若如此可直接跳至自己所需段落。对于首次接触者，请耐心阅读。

本文适用 Minecraft Java 版 1.13 及更高版本。系统环境为 Windows10，其它环境下有较小的差异。

### §1.1 新人指引
本文并非命令的入门教程，不会对命令部分做过多的详解。若你对命令尚不了解，可先依次通过如下链接学习并了解：

+ **命令手册**
	+ [命令 - Minecraft Wiki，最详细的官方我的世界百科](https://minecraft-zh.gamepedia.com/%E5%91%BD%E4%BB%A4)
	+ [新人手册-MC命令方块资源](https://commandtutorials.neocities.org/)
	+ [命令进阶](http://mc-command.oschina.io/command-tutorial/)
+ **记分板和nbt手册**
	+ [记分板 - Minecraft Wiki，最详细的官方我的世界百科](https://minecraft-zh.gamepedia.com/%E8%AE%B0%E5%88%86%E6%9D%BF)
	+ [区块格式 - Minecraft Wiki，最详细的官方我的世界百科](https://minecraft-zh.gamepedia.com/%E5%8C%BA%E5%9D%97%E6%A0%BC%E5%BC%8F)
	+ [Player.dat格式 - Minecraft Wiki，最详细的官方我的世界百科](https://minecraft-zh.gamepedia.com/Player.dat%E6%A0%BC%E5%BC%8F)

可先熟悉各项命令后，再学习记分板和nbt相关命令。实体和方块nbt亦可通过在游戏中使用`data get entity/block`命令来获取，以避免记忆大量的nbt。

若你已对1.12或以下的命令较为熟悉，可直接查看

+ [1.13页面](https://minecraft-zh.gamepedia.com/1.13)
+ [1.14页面](https://minecraft-zh.gamepedia.com/1.14)
+ [1.15页面](https://minecraft-zh.gamepedia.com/1.15)

了解命令改动之处。

### §1.2 工具准备
#### 文本编辑器
我们所涉及的所有文本文件，包括函数文件(.mcfunction)、JSON文件(.json, .mcmeta)，均需使用 UTF-8 编码格式。以下列出的文本编辑器默认均为 UTF-8 编码，可以在编辑页面的右下角状态栏看到。

+ **[VS Code](https://code.visualstudio.com/)** 下载安装后，可以安装如下插件：
	+ *Chinese (Simplified) Language Pack for Visual Studio Code* 支持中文语言
	+ *datapack helper plus (JSON)* 支持 JSON 语法补全，高亮等
	+ *language-mcfunction* 支持 mcfunction 语法和高亮
	+ *mcfunction* 支持 mcfunction 语法和高亮
+ **记事本** 为 Windows 系统自带。Windows10 最新版本的记事本已经默认是 UTF-8 编码了。点击`查看->状态栏`可以在右下角状态栏看到，因此可以正常使用。旧版本的记事本仍然不是，请勿使用。
+ **[Notepad++](https://notepad-plus-plus.org/)**
可从 [mcfunction 的语言样式和自动补全](http://www.mcbbs.net/thread-806816-1-1.html)帖中下载相关文件并导入，另外请将 Notepad++ 中`设置->首选项->其它->自动检测字符编码`选项关闭。

右下角也可以看到LF或CRLF，分别表示两种换行符，二者均可正常使用，建议使用LF。

注意不要误选了 UTF-8 with BOM 格式。

#### 压缩工具
数据包和资源包均可以为文件夹或 zip 压缩文件格式。游戏本体和模组本体的 jar 文件也需要压缩工具来打开。
+ **Windows 资源管理器** Windows10 系统自带 zip 格式的压缩和解压缩。zip 格式可以直接打开，压缩则用`选择->右键->发送到->压缩文件夹`。
+ **[7-zip](http://www.7-zip.org/)** 免费软件。
+ **winrar** 付费软件。

jar 文件可以通过重命名为 zip 文件直接用 Windows 资源管理器打开。显然，这不如`右键->7-zip->打开压缩包`方便。

#### nbt工具
推荐使用 [nbtexplorer](http://www.mcbbs.net/thread-735265-1-1.html) 来打开 dat 和其它 nbt 格式文件。

#### 绘图工具
推荐使用 Photoshop 或其它绘图工具，而非 Windows 自带的画图，来绘制材质。

### §1.3 文件类型
我们先熟悉下所涉及的文件类型，具体用途见后文。为便于查看文件后缀，请将`文件->文件夹选项->查看->隐藏已知文件类型的扩展名`选项去掉勾选。前三者为纯文本文件，可通过新建文本文件并修改后缀来创建。

+ `.json` 进度、战利品表、标签、模型、语言文件、断言、配方均为该格式。
+ `.mcmeta` 格式与 json 相同，仅用于记录资源包和数据包的信息(版本和描述)。
+ `.mcfunction` 即函数文件，每一行都是一条单独的可执行的命令。
+ `.nbt .mca` 使用 nbt 查看器打开，打开后为树状结构。世界生成、玩家、结构、地图等信息均为 nbt 格式，区块为 mca 格式。
+ `.png` 材质文件格式必须为png。
+ `.zip` 双击打开或右键选择使用压缩工具打开，通常是资源包和数据包。
+ `.jar` 右键选择使用压缩工具打开，通常是 Minecraft 或 mod 本体。下面是快照 18w31a 的游戏本体 jar 文件的文件内容。
![](https://i.loli.net/2018/08/03/5b63c9784b438.png)

### §1.4 文件结构
打开`.minecraft`所在的文件夹，这通常位于你的启动器目录下。如果启动器中设置为各版本独立，则类似的文件结构位于`versions/版本号`下。

+ `assets` Minecraft 的资源文件。可在此找到所有游戏内翻译文本的键和翻译，之后便可通过加载资源包来修改。打开 indexes 中对应的 JSON 文件，查找 zh_cn 对应的 hash 值，然后在 objects 中找到相应文件，用文本编辑软件打开即可看到相应的文本。
+ `resourcepacks` 资源包文件夹，每个子文件夹或 zip 对应一个资源包。
+ `screenshots` 游戏截图。
+ `logs` 日志信息。可打开 `latest.log` 来查看加载资源包和数据包时的错误信息，包括错误的文件名称、位置、错误的行列数等，这对于我们开发原版模组是十分重要的。
+ `options.txt` 游戏设置，诸如音量、视距等。

![](https://i.loli.net/2018/08/03/5b63c978482ce.png)

+ `saves` 地图存档，我们从网上下载的地图一般就是解压到该文件夹。
	+ `advancements` 玩家进度和完成时间。
	+ `playerdata` 玩家属性，可修改玩家的位置、复活点、飞行速度等。
	+ `stats` 玩家统计信息。
	+ `data` 地图、记分板、村庄等内容。
		+ `idcounts.dat` 记录了当前已使用的地图数量，修改后新打开的空地图会以此开始计数，这可以避免模组自定义的地图被玩家无意修改。
		+ `map_数字.dat` 相应的地图信息。
		+ `scoreboard.dat` 记分板、记分板的值、组。
		+ `command_storage_命名空间` 存取玩家自定义存储区 (storage) 的nbt。
		+ `village, stronghold, mineshaft, raids` 村庄、要塞、废弃矿井、袭击的信息。
	+ `datapacks` 数据包文件夹，每个子文件夹或 zip 对应一个数据包。
	+ `DIM1、DIM-1、region` 末地、下界和主世界的区块信息。.mca文件可用 nbtexplorer 打开并修改相应的区块内容，但是极为不便。建议使用 mcedit 等工具来编辑。
	+ `level.dat` 世界信息，包含了种子、生成类型、难度、出生点、世界边界、游戏规则等内容。
	+ `generated` 手动保存的结构，保存后将其移动至数据包内方可使用。

![](https://i.loli.net/2018/08/03/5b63ca2a6698d.png)

## §2 数据包
数据包文件层次为
```
datapacks
	数据包名称或数据包名称.zip
		pack.mcmeta
		data
			命名空间
				advancements
				functions
				loot_tables
				recipes
				structures
				tags
					blocks
					items
					fluids
					functions
					entity_types
```
`data` 下所有文件和文件夹需使用小写英文、数字或-,_来命名，**不可使用大写字母**，所有文本文件使用 UTF-8 编码。数据包可以为文件夹格式或 zip 格式，发布时可将所有内容压缩为一个 zip 文件。

压缩和解压的时候，注意文件层次，应当打开 zip 文件就可以看到数据包的 mcmeta 文件和 data 文件夹。稳妥的做法是`打开文件夹->全选->右键->发送到->压缩文件夹`。

游戏内输入 `\datapack list` 可以列出所有的数据包。

**原版数据包 (Vanilla)** Minecraft 本体文件(`版本号/版本号.jar`)中的 data 文件结构与数据包下 data 文件结构相同，其中包含了原版进度、配方、结构、战利品表等内容。这也是制作数据包的文件样板。

进度、战利品表、标签、模型、语言文件、断言、配方均为 JSON 格式文件。JSON 文件包括一对根括号{}，包含类似 `"abc":"def"` (`键:值`)的对。相同的键后者会覆盖前者。键为需引号圈住的字符串，值可以为

+ **布尔型** 例如 
	+ `"is_on_fire": false` 
	+ `"is_baby": true`
+ **数值** 例如 
	+ `"count": 2`
	+ `"chance": 0.025`
+ **字符串** 使用双引号圈住，可以使用颜色代码如§6、换行符\n。例如 
	+ `"item": "minecraft:shears"`
	+ `"condition": "minecraft:match_tool"`
	+ `"layer0": "cpp:crop/bauhinia_seeds"`
	+ `"description": "§6更多的合成 1.10\n§6by ruhuasiyu"`
+ **列表** 使用中括号圈住，例如 
	+ `"chances": [0.05, 0.0625, 0.083333336, 0.1]`
	+ `"items": [{"item": "minecraft:zombie_head"}, {"item": "minecraft:skeleton_skull"}, {"item": minecraft:wither_skeleton_skull"}, {"item": "minecraft:creeper_head"}]`
	+ `"requirements":[["wing_of_sky", "heart_of_crystal", "nova_of_fire"]]`
+ **JSON 对象** 使用大括号圈住，例如
	+ `"count": { "min": 1, "max": 2 }`
	+ `"modifiers": [{"name": "legs_armor", "attribute": "generic.armor", "operation": "addition", "amount": 4, "slot": "legs" }]`

编写时，使用空格或制表符(Tab)缩进，以便于查看括号匹配和层次。`.mcmeta` 文件也是 JSON 文件，所以格式是相同的。

wiki 上有关页面使用了 NBT 的数据类型标注，但其实并不适用于 JSON 格式。

### §2.1 `pack.mcmeta`
Minecraft 通过该文件来识别数据包，因此该文件是不可或缺的。例：
```
{
	"pack": {
		"pack_format": 4,
		"description": "§6数据包名称\n§a简要介绍 §6by 某某作者"
	}
}
```
+ `pack_format` 为数据包版本，必须为4。
+ `description` 为数据包描述，可以是单个的字符串或一个 raw json 对象。在输入 `/datapack list` 命令后，鼠标移至数据包名称上会显示 `description` 信息。

### §2.2 命名空间
命名空间(namespace)为玩家自定义的、可操作的空间。使用独立的命名空间也有利于解决和他人的冲突。

数据包下可以有多个命名空间，如果不同数据包中有相同的命名空间，则其中相同的文件名内容会根据加载先后顺序被覆盖。特别地，原版内容被保存在 `minecraft` 命名空间，想要修改和替换原版的内容只需在你的数据包内建立 `minecraft` 命名空间和相应的同名文件并修改即可。

标签文件，即 `tags` 中的文件内容默认追加而不是覆盖。因此标签文件是用来解决数据包冲突、联动的有力工具。

数据包加载顺序并不固定，因此不要在不同数据包中同一命名空间下使用相同的文件名。原版 `minecraft` 下内容总是最先被加载。可以在游戏内通过手动开启/关闭来调整加载次序。

进度、战利品表、函数、结构、标签、断言等文件的调用格式均为`命名空间:文件夹/文件名`对应`命名空间/xxx/文件夹/文件名.后缀`文件，`xxx` 为 `advancements, loot_tables, functions, strutures, tags/blocks, tags/items` 等。

若命名空间为 `minecraft`，则可直接省略 `minecraft:`。

### §2.3 进度
可参考
+ [【烯方的那一套理论】猴子都能学会的自定义advancement！](http://www.mcbbs.net/thread-685310-1-1.html)
+ [进度 - Minecraft Wiki，最详细的官方我的世界百科](https://minecraft-zh.gamepedia.com/%E8%BF%9B%E5%BA%A6)

进度(advancements)为游戏内检测玩家行为，触发后完成进度并执行奖励的系统。游戏内按 L 即可查看。

该文件夹或子文件夹下每一个 `root.json` 文件都对应一个进度页面选项卡，因此可通过文件夹来分离不同的选项卡。

例：
```
{
	"display": {
		"icon": {
			"item": "minecraft:carrot_on_a_stick",
			"nbt": "{CustomModelData:10}"
		},
		"title":{
			"translate": "advancements.cpp.root.title"
		},
		"description": {
			"translate": "advancements.cpp.root.description"
		},
		"frame": "goal",
		"background": "cm:bg.png"
	},
	"criteria": {
		"dream_wand": {
			"trigger": "minecraft:inventory_changed",
			"conditions":{
				"items":[
					{
						"nbt":"{id:\"cpp:dream_wand\"}"
					}
				]
			}
		}
	},
	"rewards": {
		"function": "cpp:adv/root",
		"recipes": ["minecraft:crafting_table","cpp:strange_block"],
		"experience": 200
	}
}
```

该例子进度
+ 图标为胡萝卜钓竿的自定义模型数据为10的模型
+ 标题为翻译文本 `advancements.cpp.root.title`
+ 描述为翻译文本 `advancements.cpp.root.description`
+ 样式为圆形边框
+ 背景为资源包中 `cm/textures/bg.png` 文件
+ 检测条件为玩家背包含有 `tag:{id:"cpp:dream_wand"}` 的物品
+ 奖励包括函数 `cpp:adv/root`，200点经验，解锁配方 `"minecraft:crafting_table"` 和 `"cpp:strange_block"`。

具体含义为
+ `display` 进度的样式。若无，则该进度不会出现在进度页面。
	+ `icon` 进度的图标。
	+ `item` 图标物品名称。
	+ `nbt` 图标物品 `nbt`，物品的材质模型可能会根据 `nbt` 不同而不同。
+ `title` 进度的名称，可以是单个的字符串或一个 raw json 对象，样例中 `translate` 文本是会随着语言改变的文本，参考[§3 资源包](#§3-资源包)。
+ `description` 进度的描述，和进度的名称格式相同。
+ `frame` 进度的类型，分为 `task`(任务 方形边框)，`challenge`(挑战 尖形边框)，`goal`(目标 圆形边框)。
+ `background` 仅根进度有，决定该选项卡的背景图，值为资源包内图片，可以为 `minecraft` 自带或其它资源包。
+ `parent` 除根进度外的进度，记录其父进度。
+ `criteria` 判据，其下为判据名称、触发器和触发器的条件。判据可以有多个。
+ `requirements` 判据的条件格式，缺省时默认所有条件都需要满足。格式为一些或的与(合取范式)，例如 `"requirements": [["a","b"],["c","d"]]` 表示当 `a` 和 `b` 至少有一个满足且 `c` 和 `d` 至少有一个满足时，会成功触发。
+ `rewards` 奖励
	+ `function` 奖励函数，完成进度时执行之。不可为函数标签。
	+ `loot` 奖励战利品表。
	+ `recipes` 解锁配方。配方也需要有相应进度来解锁，通常检测玩家拥有配方材料后触发，参考[§2.5 配方](#§2.5-配方)。
	+ `experience` 奖励经验，建议仅在高难度进度完成时给予。

进度配合奖励函数剥夺玩家该进度，则该进度可反复触发。可用于诸如检测玩家生物群系、饮食等需要循环检测的情形。

游戏内或函数内使用 `advancement` 命令来手动给予或剥夺进度。

### §2.4 函数
函数(functions)的文件后缀为 `mcfunction`，每一行表示一个单独的命令，无需/开头。执行时会按顺序依次执行，使用`#`开头的行为注释。

函数可
+ 在游戏内或函数文件中使用诸如 `function namespace:foo/bar` 命令来依次执行函数的每一条命令。
+ 在进度完成后奖励函数。

### §2.5 战利品表
可参考
+ [[CBL∫2b]Loottable - 创造一个看脸讲玄的世界 总索引](http://www.mcbbs.net/thread-619468-1-1.html)
+ [【CBL｜SPG】［1.14］战利品表：从入门到重新入门](http://www.mcbbs.net/thread-831542-1-1.html)
+ [战利品表 - Minecraft Wiki，最详细的官方我的世界百科](https://minecraft-zh.gamepedia.com/战利品表)

战利品表(loot_tables)用于实体的掉落物、方块的掉落物、钓鱼、箱子的随机物品等。

例：`minecraft/loot_tables/entities/cow.json`
```
{
	"type": "minecraft:entity",
	"pools": [
		{
			"rolls": 1,
			"entries": [
				{
					"type": "minecraft:item",
					"name": "minecraft:leather",
					"functions": [
						{
							"function": "minecraft:set_count",
							"count": {
								"min": 0,
								"max": 2
							}
						},
						{
							"function": "minecraft:looting_enchant",
							"count": {
								"min": 0,
								"max": 1
							}
						}
					]
				}
			]
		},
		{
			"rolls": 1,
			"entries": [
				{
					"type": "minecraft:alternatives",
					"children": [
						{
							"conditions": [
								{
									"condition": "minecraft:entity_properties",
									"entity": "this",
									"predicate": {
										"flags": {
											"is_on_fire": false
										}
									}
								}
							],
							"type": "minecraft:item",
							"name": "minecraft:beef",
							"functions": [
								{
									"function": "minecraft:set_count",
									"count": {
										"min": 1,
										"max": 3
									}
								},
								{
									"function": "minecraft:looting_enchant",
									"count": {
										"min": 0,
										"max": 1
									}
								}
							]
						},
						{
							"type": "minecraft:item",
							"name": "minecraft:cooked_beef",
							"functions": [
								{
									"function": "minecraft:set_count",
									"count": {
										"min": 1,
										"max": 3
									}
								},
								{
									"function": "minecraft:looting_enchant",
									"count": {
										"min": 0,
										"max": 1
									}
								}
							]
						}
					]
				}
			]
		},
		{
			"conditions": [
				{
					"condition": "minecraft:killed_by_player"
				},
				{
					"condition": "minecraft:random_chance_with_looting",
					"chance": 0.025,
					"looting_multiplier": 0.01
				}
			],
			"rolls": 1,
			"entries": [
				{
					"type": "minecraft:loot_table",
					"name": "cpp:limb_of_ridge"
				}
			]
		},
		{
			"conditions": [
				{
					"condition": "minecraft:killed_by_player"
				},
				{
					"condition": "minecraft:random_chance_with_looting",
					"chance": 0.025,
					"looting_multiplier": 0.01
				}
			],
			"rolls": 1,
			"entries": [
				{
					"type": "minecraft:loot_table",
					"name": "cpp:cow_head"
				}
			]
		}
	]
}
```
该例子战利品表表示牛死亡时
+ 掉落`0-(2+抢夺等级)`个皮革
+ 掉落`1-(3+抢夺等级)`个牛肉，着火则掉落熟牛肉
+ 被玩家杀死时，有`(2.5+抢夺等级)%`几率掉落战利品表 `cpp:limb_of_ridge` 的物品
+ 被玩家杀死时，有`(2.5+抢夺等级)%`几率掉落战利品表 `cpp:cow_head` 的物品

在 `minecraft` 命名空间下，记录了实体的默认掉落物、方块的掉落物、钓鱼和箱子战利品的战利品表，玩家可通过 `jar` 文件查看其文件结构。若要修改之，在数据包中创建 `minecraft` 命名空间以及同名文件来覆盖之。

战利品表可以以如下等方式调用
+ `setblock ~ ~ ~ minecraft:chest{LootTable:"cpp:chests/something"}`
+ `give @s minecraft:chest{BlockEntityTag:{LootTable:"cpp:chests/something"}}`
+ `summon minecraft:bat ~ ~ ~ {DeathLootTable:"cpp:chests/something"}`
+ `loot spawn ~ ~ ~ loot foo:bar`

战利品表除上述常规用途外，还可用于
+ 生成随机数，见[战利品表随机数](https://www.mcbbs.net/thread-900914-1-1.html)。
+ 修改玩家背包物品，见[修改玩家背包物品信息](https://www.mcbbs.net/thread-860954-1-1.html)，[戴帽子](https://www.mcbbs.net/thread-879073-1-1.html)。
+ 将特定物品输出至容器内，见[物品分类器](https://www.mcbbs.net/thread-898170-1-1.html)。

### §2.5 配方
配方(recipes)包括工作台合成、切石机合成、熔炉烧炼、高炉烧炼、烟熏炉烧炼、营火烧炼，**不支持带 nbt 标签。具体格式见[§5 合成](#§5-合成)。想要实现带 nbt 的合成需要藉由其它方式，见[§5 合成](#§5-合成)。

在默认情形(限制配方关闭)下，玩家总是可以使用所有的配方，但是未获得的不会在配方书中显示，因此建议为你的自定义配方添加合适的进度来获取该配方。

### §2.6 结构
可参考
+ [建筑党也能愉快享用结构方块-图文并茂教会你使用结构方块](http://www.mcbbs.net/thread-652937-1-1.html)
+ [如何使用结构方块](http://www.mcbbs.net/thread-801350-1-1.html)
+ [结构方块 - Minecraft Wiki，最详细的官方我的世界百科](https://minecraft-zh.gamepedia.com/结构方块)

结构(structures)文件为 nbt 文件，后缀为 `nbt`。结构存储了一个长方体区域的方块和实体信息，玩家可以创建、保存、调用这样的结构。

在游戏中获得结构方块(structure_block)后，放置好所需要的方块结构和实体，然后放置结构方块，设置为保存模式，调整好大小，输入名称，点保存即可（注意区分是否需要实体）。然后从 `generated` 文件夹复制到数据包内，在结构方块中输入"命名空间:文件夹/文件"格式加载（注意区分是否需要实体）。

我们也可以在函数中加载，先放置结构方块，然后放置并清除红石块即可。这个技巧配合战利品表等，可用于随机在世界生成结构。

例：
```
setblock ~ ~ ~ minecraft:structure_block{posX:-1,posY:0,posZ:-1,name:"cpp:build/enchanting_room",mode:"LOAD"}
setblock ~ ~1 ~ minecraft:redstone_block
setblock ~ ~1 ~ minecraft:air
```

### §2.7 标签
标签(tags)根据子文件夹不同分为5种。Minecraft 中有很多内容都叫做标签，注意区分它们。

例如方块标签 `cpp/tags/blocks/fluid.json`
```
{
	"replace": false,
	"values": [
		"minecraft:air",
		"minecraft:cave_air",
		"minecraft:void_air",
		"minecraft:bubble_column",
		"minecraft:water",
		"minecraft:lava"
	]
}
```
表示空气、气泡柱、水、熔岩。

标签中 `replace` 可以为
+ `false` 表示追加当前 `values` 至该标签
+ `true` 表示覆盖之前原版和其它数据包添加至该标签的内容。

默认为 `false`。其它标签也是如此。

标签中亦可引用其它标签，例如
`minecraft/tags/blocks/logs.json`
```
{
	"values": [
		"#minecraft:dark_oak_logs",
		"#minecraft:oak_logs",
		"#minecraft:acacia_logs",
		"#minecraft:birch_logs",
		"#minecraft:jungle_logs",
		"#minecraft:spruce_logs"
	]
}
```
就包含了所有6种原木、木头、去皮原木、去皮木头。

#### §2.7.1 方块标签
位于 `tags/blocks` 文件夹下，用于在命令中用于检测/调用多个方块。例：当玩家眼睛位置不是流体(空气、水等)时，输出 I'm stucked!

并执行命令
```
execute as @a at @s anchored eyes unless block ^ ^ ^ #cpp:fluid run say I'm stucked!
```
因为命令执行地点为实体的脚，所以我们使用 `anchored eyes` 来使得局部坐标的位置变为玩家的眼睛。


调试模式(F3)下，玩家指向方块时会显示含有该方块的所有方块标签；

#### §2.7.2 物品标签
位于 `tags/items` 文件夹下，用于
+ 在 `clear` 命令中用于清除多个不同 `id` 物品
+ 在配方文件中表示合成/熔炼时所需的物品可以为标签中的任一种
+ 进度判定
+ 战利品表类型

#### §2.7.3 函数标签
位于 `tags/functions` 文件夹下，用于在 `function` 命令中一次性按次序执行多个函数。

#### §2.7.4 实体类型标签
位于 `tags/blocks` 文件夹下，用于在选择器 `@e` 的选项 `type` 中指定多种不同实体，例如 `@e[type=#cpp:hostiles]`。

#### §2.7.5 流体标签
位于 `tags/blocks` 文件夹下。

#### §2.7.6 预设标签
`minecraft` 命名空间中预设了一些标签。其中
+ `minecraft/tags/functions/load.json` 中的函数会在加载时被执行一次，我们常称之为加载函数、load函数。用于初始化的函数应当添加至该标签。
+ `minecraft/tags/functions/tick.json` 中的函数每刻会被执行一次，我们常称之为循环函数、主函数、tick函数。需要高频执行的函数应当添加至该标签。

利用预设标签还可以实现更多燃料、改变植物种植所需的方块，甚至改变水和熔岩的性质，可参见[minecraft预设tag以及实现随机方块功能](http://www.mcbbs.net/thread-811990-1-1.html)以及[标签 - Minecraft Wiki，最详细的官方我的世界百科](https://minecraft-zh.gamepedia.com/%E6%A0%87%E7%AD%BE)。

例如：让末影人无法拿起任何方块。

创建文件 `minecraft/tags/blocks/enderman_holdable`
```
{
	"replace": true,
	"values": [
	]
}
```

## §3 资源包
资源包可以极大地提升原版模组的美观程度，因此现在大部分原版模组都需要使用配套的资源包。
资源包文件层次为
```
resourcepacks
	资源包名称或资源包名称.zip
		pack.mcmeta
		pack.png
		assets
			命名空间
				lang
					zh_cn.json
					zh_tw.json
					en_us.json
				models
				textures
```
其中 `assets` 的文件结构和 [§1.4 文件结构](#§1.4-文件结构)中版本 `.jar/assets` 的结构是一样的。

`assets` 下所有文件和文件夹需使用小写英文、数字或-,_来命名，**不可使用大写字母**，所有文本文件为使用 UTF-8 编码的 JSON文件，图片使用 `png` 格式。发布时可将所有内容压缩为一个 zip 文件。

压缩和解压的时候，注意文件层次，应当打开 zip 文件就可以看到数据包的 pack.mcmeta、pack.png 和 assets 文件夹。稳妥的做法是`打开文件夹->全选->右键->发送到->压缩文件夹`。

在资源包菜单中，加载次序由下至上，因此上方的资源包内容会覆盖下方的资源包同名内容。由于原版模组往往会修改原版物品模型，因此同时安装多个原版模组的资源包时，很容易出现文件冲突，此时需要玩家手动合并资源包方可使用。具体而言，对比两个资源包的同名文件，将相同的模型文件的 `overrides` 合并，其它内容选择需要的留下即可。

在存档内的 `resources.zip` 资源包会在进入存档时自动加载(最后加载)。

本文中我们仅对资源包做简单介绍，更详细的文件说明请参阅[资源包 - Minecraft Wiki，最详细的官方我的世界百科](https://minecraft-zh.gamepedia.com/%E8%B5%84%E6%BA%90%E5%8C%85)或论坛材质资源版相关内容。

材质包和资源包是不同的东西，目前 Minecraft Java 只有资源包，请不要使用错误的名称。

### §3.1 `pack.mcmeta` 和 `pack.png`

Minecraft 通过 `pack.mcmeta` 来识别资源包，因此该文件是不可或缺的。例如：
```
{
	"pack": {
		"pack_format": 4,
		"description": "§6资源包名称\n§a简要介绍 §6by 某某作者"
	},
	"language": {
		"zh_cn":{
			"name": "简体中文",
			"region": "中国大陆",
			"bidirectional": false
		},
		"en_us":{
			"name": "English",
			"region": "United States",
			"bidirectional": false
		},
		"zh_tw":{
			"name": "繁体中文",
			"region": "中国台湾",
			"bidirectional": false
		}
	}
}
```
+ `pack_format` 为资源包版本，必须为4。
+ `description` 为资源包描述，可以是单个的字符串或一个 raw json 对象。资源包菜单中可以看到。

资源包可以包含一个 `pack.png`，它是大小为16*16的图片，用于在资源包菜单中显示。

### §3.2 命名空间
命名空间(namespace)为玩家自定义的、可操作的空间。不同资源包中相同的命名空间下相同的文件名内容会根据加载先后顺序被覆盖。特别地，原版内容被保存在 `minecraft` 命名空间，想要修改和替换原版的模型材质只需在你的数据包内建立 `minecraft` 命名空间和相应的同名文件并修改即可。

模型和材质的调用格式均为`命名空间:文件夹/文件名`对应`命名空间/xxx/文件夹/文件名.后缀`文件，`xxx` 为 `models` 或 `textures`。

若命名空间为 `minecraft`，则可直接省略 `minecraft:`。

建议和数据包使用相同的命名空间名。

### §3.3 语言文件
语言文件可以放在任一命名空间下的 `lang` 文件夹下。语言文件中可以使用样式代码来实现彩色文字。

建议至少支持中文简体(`zh_cn`)、繁体(`zh_tw`)和英文(`en_us`)三种语言。建议所有物品、进度、游戏提示等文本均采用 `translate` 文本。

例如：`assets/命名空间/lang/zh_cn.json`
```
{
	"item.cpp.magnet":"§r磁铁",
	...
}
```
`assets/命名空间/lang/en_us.json`
```
{
	"item.cpp.magnet":"§rMagnet",
	...
}
```
也可以用此方法修改物品的默认名称等内容。例如：

`assets/命名空间/lang/zh_cn.json`
```
{
	"item.minecraft.potion.effect.empty": "§r神秘药水",
	...
}
```
则未知的药水的名称不再是`不可合成的药水`，而是`神秘药水`。

`translate` 还有个有趣但不一定实用的用法。
```
{
	"The":"§a原版模组《更多的合成》已成功加载,",      
	"resourcepack":"版本",
	"does":"§a1.9.1§a.",
	"not":"§a更多内容请",
	"Install":"§e点击此处进入wiki.",
	"correctly":"§a作者:",
	"or":"§aruhuasiyu,",
	"Launch":"§aRubberTree",
	...
}
```
则在数据包中输出相应文本时，若无资源包或资源包错误，则会显示
```
The resourcepack does not Installl correctly or Launch.
```
以提示玩家资源包未加载。

### §3.4 `CustomModelData` 物品模型
由于1.14添加了 `CustomModelData`，我们可以拥有几乎无穷多的物品模型。为了便于他人整合，我们建议将 `custom_model_data` 的前四位确定模组的独有区段，后四位作为模组不同模型的值，例如 `12970000-12979999` 之间。此外，建议 `custom_model_data` 不要超过 `16777216`，原因见[custom_model_data的使用限制](https://www.mcbbs.net/thread-867051-1-1.html)。

我们会给出一个例子来说明实现流程。

首先在 `minecraft` 下的胡萝卜钓竿物品模型中添加额外的模型(`overrides`)，并引用我们自定义的模型

`assets/minecraft/models/item/carrot_on_a_stick.json`
```
{
	"parent": "item/handheld",
	"textures": {
		"layer0": "item/carrot_on_a_stick"
	},
	"overrides": [
		{ "predicate": { "custom_model_data": 12970001 }, "model": "cpp:element/blue_force_of_sky"},
		{ "predicate": { "custom_model_data": 12970002 }, "model": "cpp:element/green_force_of_water"},
		{ "predicate": { "custom_model_data": 12970003 }, "model": "cpp:element/cyan_force_of_mountain"},
		{ "predicate": { "custom_model_data": 12970004 }, "model": "cpp:element/orange_force_of_dirt"},
		{ "predicate": { "custom_model_data": 12970005 }, "model": "cpp:element/yellow_force_of_earth"},
		{ "predicate": { "custom_model_data": 12970006 }, "model": "cpp:element/red_force_of_fire"}
	]
}
```
注意 `custom_model_data` 需要按照从小往大的次序，否则会导致后面的覆盖前面的。

然后创建自定义的模型

`assets/cpp/models/element/red_force_of_fire.json`
```
{
	"parent": "item/handheld",
	"textures": {
		"layer0": "cpp:element/red_force_of_fire"
	}
}
```

最后绘制材质，并将其保存为

`assets/craftingpp/textures/element/red_force_of_fire.png`

这样我们就设计好了这个物品模型，在[§4.4 物品设计](#§4.2-物品设计)我们将会说明如何使用该模型。

### §3.5 模型语法
模型本身只是一个 JSON 文件，只有 `minecraft` 命名空间下特定名称的文件才对应特定的物品/方块模型。例如 `minecraft/models/item/carrot_on_a_stick.json` 表示胡萝卜钓竿的物品模型，`minecraft/models/block/stone.json` 表示石头的方块模型。

模型可以理解成一些可以旋转的长方体的拼接，每个长方体的若干个面贴上了材质图案。长方体的厚度可以为0，材质也可以只贴若干个面。

我们通过几个例子来理解下模型文件的语法。这个例子使用的是 Minecraft 自带的物品模型，并修改了在部分位置的显示：
```
{
	"parent": "item/generated",
	"display": {
		"thirdperson_righthand": {
			"rotation": [ 0, -90, 55 ],
			"translation": [ 0, 4.0, 0.5 ],
			"scale": [ 0.85, 0.85, 0.85 ]
		},
		"thirdperson_lefthand": {
			"rotation": [ 0, 90, -55 ],
			"translation": [ 0, 4.0, 0.5 ],
			"scale": [ 0.85, 0.85, 0.85 ]
		},
		"firstperson_righthand": {
			"rotation": [ 0, -90, 25 ],
			"translation": [ 1.13, 3.2, 1.13 ],
			"scale": [ 0.68, 0.68, 0.68 ]
		},
		"firstperson_lefthand": {
			"rotation": [ 0, 90, -25 ],
			"translation": [ 1.13, 3.2, 1.13 ],
			"scale": [ 0.68, 0.68, 0.68 ]
		}
	}
}
```
我们可以看到，它继承了模型 `minecraft:item/generated`
```
{
	"parent": "builtin/generated",
	"display": {
		"ground": {
			"rotation": [ 0, 0, 0 ],
			"translation": [ 0, 2, 0],
			"scale":[ 0.5, 0.5, 0.5 ]
		},
		"head": {
			"rotation": [ 0, 180, 0 ],
			"translation": [ 0, 13, 7],
			"scale":[ 1, 1, 1]
		},
		"thirdperson_righthand": {
			"rotation": [ 0, 0, 0 ],
			"translation": [ 0, 3, 1 ],
			"scale": [ 0.55, 0.55, 0.55 ]
		},
		"firstperson_righthand": {
			"rotation": [ 0, -90, 25 ],
			"translation": [ 1.13, 3.2, 1.13],
			"scale": [ 0.68, 0.68, 0.68 ]
		},
		"fixed": {
			"rotation": [ 0, 180, 0 ],
			"scale": [ 1, 1, 1 ]
		}
	}
}
```
最后这个 `builtin/generated` 是 Minecraft 中内建的模型，不能修改。

如果我们想要立体的模型，我们可以继承 `minecraft:block/block` 或者其中很多的方块模型模板，也可以自行撰写。我们来看一个自定义模型的例子。
```
{
	"parent": "block/block",
	"display": {
		"head": {
			"scale": [ 3.28, 3.28, 3.28 ]
		},
		"gui": {
			"rotation": [ 30, 225, 0 ],
			"translation": [0, -2, 0],
			"scale": [ 1.6, 1.6, 1.6 ]
		},
		"ground": {
			"rotation": [ 0, 0, 0 ],
			"translation": [ 0, 3, 0],
			"scale":[ 0.64, 0.64, 0.64 ]
		},
		"fixed": {
			"rotation": [ 0, 0, 0 ],
			"translation": [ 0, 0, 0],
			"scale":[ 1.28, 1.28, 1.28 ]
		},
		"thirdperson_righthand": {
			"rotation": [ 75, 45, 0 ],
			"translation": [ 0, 2.5, 0],
			"scale": [ 0.96, 0.96, 0.96 ]
		},
		"firstperson_righthand": {
			"rotation": [ 0, 45, 0 ],
			"translation": [ 0, 0, 0 ],
			"scale": [ 1.02, 1.02, 1.02 ]
		},
		"firstperson_lefthand": {
			"rotation": [ 0, 225, 0 ],
			"translation": [ 0, 0, 0 ],
			"scale": [ 1.02, 1.02, 1.02 ]
		}
	},
	"textures": {
		"particle": "entity/rabbit/brown",
		"layer": "entity/rabbit/brown"
	},
	"elements": [
		{
			"from": [ 5.5, 6, 5.5 ],
			"to": [ 10.5, 10, 10.5 ],
			"faces": {
				"east":	{ "uv": [ 8, 2.5, 9.25, 4.5 ], "texture": "#layer" },
				"north":{ "uv": [ 9.25, 2.5, 10.5, 4.5 ], "texture": "#layer"},
				"west":	{ "uv": [ 10.5, 2.5, 11.75, 4.5 ], "texture": "#layer" },
				"south":{ "uv": [ 11.75, 2.5, 13, 4.5 ], "texture": "#layer" },
				"up":	{ "uv": [ 9.25, 0, 10.5, 2.5 ], "texture": "#layer", "rotation": 180},
				"down":	{ "uv": [ 10.5, 0, 11.75, 2.5 ], "texture": "#layer" }
			}
		},
		{
			"from": [ 7.5, 7.5, 5 ],
			"to": [ 8.5, 8.5, 6 ],
			"faces": {
				"east":	{ "uv": [ 8, 5, 8.25, 5.5 ], "texture": "#layer" },
				"north":{ "uv": [ 8.25, 5, 8.5, 5.5 ], "texture": "#layer"},
				"west":	{ "uv": [ 8.5, 5, 8.75, 5.5 ], "texture": "#layer" },
				"south":{ "uv": [ 8.75, 5, 9, 5.5 ], "texture": "#layer" },
				"up":	{ "uv": [ 8.25, 4.5, 8.5, 5 ], "texture": "#layer", "rotation": 180},
				"down":	{ "uv": [ 8.5, 4.5, 8.75, 5 ], "texture": "#layer" }
			}
		},
		{
			"from": [ 5.5, 10, 9.5 ],
			"to": [ 7.5, 15, 10.5 ],
			"rotation": {
				"origin": [6.5, 10, 10], "axis": "y", "angle": -22.5
			},
			"faces": {
				"east":	{ "uv": [ 14.5, 0.5, 14.75, 3 ], "texture": "#layer" },
				"north":{ "uv": [ 14.75, 0.5, 15.25, 3 ], "texture": "#layer"},
				"west":	{ "uv": [ 15.25, 0.5, 15.5, 3 ], "texture": "#layer" },
				"south":{ "uv": [ 15.5, 0.5, 16, 3 ], "texture": "#layer" },
				"up":	{ "uv": [ 14.75, 0, 15.25, 0.5 ], "texture": "#layer", "rotation": 180},
				"down":	{ "uv": [ 15.25, 0, 15.75, 0.5 ], "texture": "#layer" }
			}
		},
		{
			"from": [ 8.5, 10, 9.5 ],
			"to": [ 10.5, 15, 10.5 ],
			"rotation": {
				"origin": [9.5, 10, 10], "axis": "y", "angle": 22.5
			},
			"faces": {
				"east":	{ "uv": [ 13, 0.5, 13.25, 3 ], "texture": "#layer" },
				"north":{ "uv": [ 13.25, 0.5, 13.75, 3 ], "texture": "#layer"},
				"west":	{ "uv": [ 13.75, 0.5, 14, 3 ], "texture": "#layer" },
				"south":{ "uv": [ 14, 0.5, 14.5, 3 ], "texture": "#layer" },
				"up":	{ "uv": [ 13.25, 0, 13.75, 0.5 ], "texture": "#layer", "rotation": 180},
				"down":	{ "uv": [ 13.75, 0, 14.25, 0.5 ], "texture": "#layer" }
			}
		}
	]
}
```
我们先继承了 `minecraft:block/block` 中 `display` 的设定，然后修改模型在头部和背包的放缩和位移。

具体的语法如下，见[模型 - Minecraft Wiki，最详细的官方我的世界百科](https://minecraft-zh.gamepedia.com/模型)
+ `parent` 表示继承的模型，可以没有该项，若有则相当于将其文件内容复制到该位置。例如物品的平面模型、方块模型、玻璃板模型等，我们都可以直接调用而无需自己编写。或者需要多次使用的模型，我们也可以写好后在其它模型中直接调用。例子中继承的模型 `minecraft:item/handheld` 为手持物品的平面模型，这样我们可以免去调整物品在背包和展示框内的显示。
+ `display` 确定物品在不同位置
	+ `ground` 掉落物
	+ `head` 头部
	+ `thirdperson_righthand` 第三人称右手
	+ `thirdperson_lefthand` 第三人称左手
	+ `firstperson_righthand` 第一人称右手
	+ `firstperson_lefthand` 第一人称左手
	+ `fixed` 物品展示框
	+ `gui` 背包或容器
		+ 放缩(`scale`)
		+ 旋转(`rotation`)
		+ 平移(`translation`)
	
	注意这些数值均有范围限制，例如`scale`至多为4。
+ `textures` 确定模型使用的材质文件位置，这里 `#layer` 被赋值为 `entity/chicken` 这个材质。直接把 `#layer` 换成 `entity/chicken` 也是可以的，但是使用 `#layer` 更便于修改。如果模型文件作为模板使用，可以不写 	`textures`，而是在其它模型引用它时再指定以确定最终的样子。
	+ `particle` 表示方块被破坏/物品被消耗时的粒子效果采用的材质。
+ `elements`
	+ `from` 和 `to` 确定长方体的范围。`from` 和 `to` 中的 `x,y,z` 范围为`-16`到`32`之间，不做放缩时，`0~16`即一个方块的完整大小。
	+ `rotation` 旋转这个长方体
		+ `origin` 旋转中心
		+ `axis` 沿哪个轴旋转
		+ `angle` 旋转的角度，只能是`0, 22.5, 45, -22.5, -45`
	+ `faces` 为方块的6个面材质信息。我们放置方块时，离我们最近的为方块的北方(north)，然后站在方块的视角按前北后南(z轴)，左西右东(x轴)确定其6个面的朝向。
		+ `texture` 确定了所使用的材质。我们建议按次序东北西南上下的次序写以便于想象。可以在材质文件中按照 ![](https://i.loli.net/2019/05/24/5ce786a746fe972611.png) 的相对位置来绘制材质，也可以分为6个单独的材质。
		+ `uv` 确定了选取材质的哪一部分。将材质划分为16×16个区域，该数值指定了便是所选的区域。例如材质文件为`64×64`大小，则`"uv": [ 3.5, 3, 4, 4 ]`使用的是横向`14-16`纵向`12-16`的`2×4`个像素。
		+ `rotation` 旋转材质，值为`0,90,180,270`。

由于 `scale` 至多为`4`，而 `from to` 至多为`-16`到`32`，因此模型最多可以放大至`12`倍。想要更大的模型可以通过分段来旋转拼接而成，参阅
+ [因为不知道发到哪里只好发过来了 也不知道火没火星 毕竟我没有画材质的朋友。。。](https://www.mcbbs.net/thread-637959-1-1.html)
+ [四十米长的大刀？我在minecraft里做1200米的！](https://www.bilibili.com/video/av24626290)
+ [【魔改材质包】数体积专用-3轴标尺](https://www.bilibili.com/video/av39646162)

模型在不同位置仅有放缩旋转平移的差别，想要实现视觉上的明显不同，可参阅[【1.14】物品头部/背包/手持显示不同材质/模型](https://www.mcbbs.net/thread-833056-1-1.html)。

方块状态我们一般不会用到，而且语法比较简单，可直接参阅 wiki，这里不做赘述。

### §3.6 材质
材质的绘制需要用到诸如 Photoshop 之类的画图软件，具体请参考材质版或网络上的相关教程。

当模型调用的材质不存在时，会显示紫黑色的材质。如果模型是正确的，你仍然可以看出正确的模型样子。

材质可以是动态的。材质的高度为宽度的x倍时，动态材质可以有x帧，分别对应材质自上而下划分的x个块。动态材质还需要一个 `mcmeta` 文件，例如 `foo.png` 对应 `foo.png.mcmeta`，内容为
```
{
  	"animation": {
    	"interpolate": false,
    	"frametime": 4,
		"frames": [
			0,
			1,
			2,
			3,
			{"index":4,"time": 2},
			5
		]
  	}
}
```
这里
+ `interpolate` 是否需要插值过渡。可以省略。
+ `frametime` 每一帧的默认时长(刻)。
+ `frames` 指定播放帧的次序
	+ `数字` 从0开始
	+ `index` 和 `time` 可以单独指定这一帧的时长(刻)

### §3.7 声音
音效文件为 `assets/命名空间/sounds.json`，它调用的是 `assets/命名空间/sounds` 文件夹下的 `ogg` 文件。例如：
```
{
    "juicer": {
        "category": "block",
        "sounds": [
            "rf:juicer"
        ]
    },
	"swing": {
		"sounds": [
			"rf:lightsaber/swing1",
			"rf:lightsaber/swing2",
			"rf:lightsaber/swing3",
			"rf:lightsaber/swing4"
		],
		"category": "hostile"
	}
}
```
其中自定义名称下包括
+ `replace` 是否覆盖原有的声音信息，默认为`false`，即不覆盖。
+ `sounds` 音效文件列表，触发时会随机选择一个播放。
+ `subtitle` 显示的字幕。
+ `category` 种类，在`选项->音乐和声音中`可以选择开启/关闭特定种类的声音。

### §3.8 字体
添加 `assets/minecraft/font/default.json` 文件可以追加/覆盖特殊字符的字体显示，例如
```
{
	"providers": [
		{
			"type": "bitmap",
			"file": "minecraft:font/mana0.png",
			"height": 91,
			"ascent": 85,
			"chars": ["\ue010"]
		},
		{
			"type": "bitmap",
			"file": "minecraft:font/mana1.png",
			"height": 91,
			"ascent": 85,
			"chars": ["\ue011"]
		}
	]
}
```
我们追加了字符 `\ue010` 和 `\ue011` 的材质，其中
+ `file` 指定了所用的材质，这里调用了 `minecraft/textures/font/mana0.png` 等材质
+ `height` 该字符的高度
+ `ascent` 该字符向上移动的长度
+ `chars` 对应的字符列表

我们可以用 `\u` 开头来表示不容易打出的字符，参见[Unicode® Character Table](https://unicode-table.com)。

利用这种方式，我们可以做到在成书、玩家快捷栏上方、聊天区域、物品名称等地方显示图片，见[【1.13】如何添加图片?](https://www.mcbbs.net/thread-835539-1-1.html)。特别地，如果可以包含了使用负长度的空格的字体，还可以实现更为炫酷的效果，例如[字体黑科技 —— 潜影盒内容预览](https://www.bilibili.com/video/av67508247)。

### §3.9 着色器
着色器可以对游戏内的视觉效果进行修改，目前可以通过
+ 旁观特定生物，可使用 `/spectate` 命令强制旁观；
+ 屏幕中有发光的实体
两种情形来达成。

着色器文件为位于 `assets/minecraft/shaders/program` 下方的 `fsh` 文件，具体用法可参考[原版着色器指导](https://www.mcbbs.net/thread-916150-1-1.html)和[几个原版着色器示例](https://www.mcbbs.net/thread-917679-1-1.html)。


## §4 规划
当我们有了一定的命令基础和数据包与资源包的相关知识之后，我们可以开始考虑做一个模组了。模组的目的是在原版的基础上做出一定的修改，模组的核心是内容，命令和技巧都只是为实现这一目的的手段。通常的设计路线如下图所示：
[align=center][img]https://i.loli.net/2018/05/01/5ae7f0a5105f4.png[/img][/align]平衡性可以从合成难度和触发条件等方面来调整。

原版模组不比基于 Forge/Liteloader API 的模组，在实现效率上一般会有所欠缺，因此我们在制作和测试过程中，应当优先保证流畅度，再考虑内容的充实性。

模组的整个生命周期中，所有内容都应当有完整的文档记录，以便于随时查看和修改。

为你的模组设定合理的版本号管理方式，例如。

使用 Git 来管理你的模组，有利于保存模组的所有历史版本。这可以减少因误操作导致的损失。

### §4.1 名称设计
模组的所有内容都应当被合理地命名，尽量采用简洁且有意义的命名，同时便于他人处理数据包冲突。这些内容包括数据包下所有的文件和文件夹名以及记分板、标签、组的名称等。建议各种名称均使用大驼峰、小驼峰或下划线记法。

+ **数据包名称** 建议使用模组全名，空格和特殊字符使用下划线代替或忽略，也可使用中文名称。例如 `craftingpp、更多的合成v1.10、CraftingPlusPlus` 等。
+ **命名空间** 由于需要频繁使用，不建议使用过长的字符串，过短则容易冲突，可使用模组名称的全程或缩写来表示。命名空间必须由小写或下划线组成。建议整个模组使用一个命名空间，或若干相同前缀的命名空间。例如 `craftingpp、cpp、fisma、mek` 等。
+ **物品名称** 建议使用物品英文名称对应的小写+下划线写法作为物品id，具体设计见下一节。例如 `cpp:red_force_of_fire`。
+ **记分板、组** 建议使用命名空间为前缀的驼峰记法，因为记分板名称长度不可超过16。长度允许的话，使用下划线记法也可以。例如 `cppValue、cppCraft、cppTicks、cpp_health`。
+ **实体标签** 建议使用命名空间为前缀。例如 `cpp_entities_checker、cpp_generate_dead、cpp_machines_marker、cppDarkAnimals`。
+ **tick函数** 即 `minecraft/tags/functions/tick.json` 下添加的函数，我们建议使用 `_main.mcfunction、tick.mcfunction、loop.mcfunction` 等名称。有时候我们简称
+ **load函数** 即 `minecraft/tags/functions/load.json` 下添加的函数，我们建议使用 `load.mcfunction、_init.mcfunction、root.mcfunction` 等名称。
如果模组包含多个模块，可以在不同数据包下使用相同的命名空间、不同的文件夹，来分门别类。

### §4.3 调试
自1.13起，加载中出现的错误一般会在 `logs/latest.log` 中提示。测试时，打开这个文件，可以看到具体是哪个文件的哪个位置发生了错误。必要时，可添加适当的tellraw命令来查看断点或记分板值等。资源包的错误也可在该文件中查看。

### §4.3 前置与附属
使用他人已写好的前置可以在减少自己的工作量，例如

+  (https://www.mcbbs.net/thread-900914-1-1.html]战利品表随机数]
+  (https://www.mcbbs.net/thread-916294-1-1.html]方块通用处理]
+  (https://github.com/ruhuasiyu/CraftingPlusPlus/tree/master/other_datapacks/%E5%90%88%E6%88%90%E9%80%9A%E7%94%A8%E5%A4%84%E7%90%86]合成通用处理]
+  (https://github.com/ruhuasiyu/CraftingPlusPlus/tree/master/other_datapacks/%E5%8E%9F%E7%89%88%E6%A8%A1%E7%BB%84%E5%AE%B9%E5%99%A8%E6%89%A9%E5%B1%95]原版模组容器扩展]

这些前置已经包含了诸如生成随机数、处理模组方块、合成、支持mod容器等内容，这样开发者就不用再花费精力在这些事件的处理上，只需要调用它们提供的接口即可。

如果你所使用的前置里面有诸如
`foo:bar`
```
scoreboard players set #datapack_foobar value 1```
之类的函数的话，你可以在你的数据包中的load函数中添加
```
scoreboard players set #datapack_foobar value 0
function foo:bar
execute if score #datapack_foobar value matches 0 run tellraw @a {"text":"[XX模组]：缺少必要的数据包前置[YY模组]！"}
```
来缺少前置时提醒使用者。

附属也是类似的，例如在你的模组中添加了一种机器，里面对物品进行了一些处理，例如
```
execute if block ~ ~ ~ barrel{Items:[{Slot:3b,id:"minecraft:mycelium"},{Slot:12b,id:"minecraft:dirt"}]} run replaceitem block ~ ~ ~ container.15 minecraft:mycelium
function #cpp:item_processer```
那么其它开发者就可以通过在函数标签#cpp:item_processer中添加相应的函数命令来实现更多的机器配方。

### §4.2 物品设计
由于原版模组从不添加原版不存在的物品，所以我们需要采取一些办法来区分。通常，我们建议使用id来作为物品的唯一标记，CustomModelData确定物品的材质模型。
**例** 添加物品“红色火之力”，命名空间为cpp，英文名称为Red Force of Fire，不可叠加，效果为右键执行若干命令。
我们可使用
```
minecraft:carrot_on_a_stick{id:"cpp:red_force_of_fire",CustomModelData:12970013,display:{Name:'{"translate":"item.cpp.red_force_of_fire"}'}}
```
物品原型为胡萝卜钓竿(carrot_on_a_stick)，这样可以便于右键检测。

+ 物品模组id为cpp:red_force_of_fire。建议使用模组对应的“命名空间:物品名称”来表示，以与其它模组的物品区分。
+ 使用胡萝卜钓竿的第12970013个custom_model_data模型。建议前4位数字为模组固定的编号，以与其它模组区分以便于整合，后4位表示该模组下同种原版物品对应的不同材质模型。在资源包中添加相应的模型。使用时注意(thread-867051-1-1.html]custom_model_data的使用限制]。
+ 显示名称为 item.cpp.red_force_of_fire 对应的翻译文本。在资源包中添加相应的翻译文本。

此外，我们还可以使用byte型nbt来标记物品的类别，以便于探测；使用List型nbt来标记诸如属性之类的内容，以及需要探测是否处于该类别的物品。

对于科技类的模组，我们推荐使用(https://www.mcmod.cn/post/927.html]原版模组矿物辞典]来便于不同的原版模组/插件引用。

建议为模组添加的所有物品添加相应的loot_table来便于获取/修改/合成等。
**例** craftingpp/data/cpp/loot_tables/red_force_of_fire.json
```
{
	"pools": [
		{
			"rolls": 1,
			"entries": [
				{
					"type": "item",
					"name": "minecraft:carrot_on_a_stick",
					"functions": [
						{
							"function": "set_nbt",
							"tag": "{display:{Name:'{\"translate\":\"item.cpp.red_force_of_fire\"}'},id:'cpp:red_force_of_fire',CustomModelData:12970006}"
						}
					]
				}
			]
		}
	]
}
```然后，我们需要在资源包中添加相应模型
assets/minecraft/models/item/carrot_on_a_stick.json
```
{
	"parent": "item/handheld",
	"textures": {
		"layer0": "item/carrot_on_a_stick"
	},
	"overrides": [
		...
		{ "predicate": { "custom_model_data": 12970006 }, "model": "cpp:element/red_force_of_fire"},
		...
	]
}
```assets/cpp/models/element/red_force_of_fire.json
```
{
	"parent": "item/handheld",
	"textures": {
		"layer0": "cpp:element/red_force_of_fire"
	}
}
```并添加相应材质assets/cpp/textures/element/red_force_of_fire.png。

烟火之星等受颜色控制而改变、具有双层模型的物品，若相应CustomModelData的模型也是双层的，是可以根据颜色而变化的。但是像盾牌受图案模式改变，其含有CustomModelData的对应物品并不会受到这些NBT影响。

建议

+ 需要右键互动的使用胡萝卜钓竿(carrot_on_a_stick)的物品模型；
+ 无互动功能的可使用烟火之星的物品模型。
+ 与土交互的(如花)，可使用树苗的模型，并移除其原有模型。
+ 与耕地交互的(如作物)，可使用小麦种子的模型，并移除其原有模型。
+ 食物，可使用面包、苹果、曲奇等物品的模型。
+ 有药水效果的食物，可使用蜜汁炖菜(也可使用普通食物，配合进度来实现药水效果)，注意会剩下碗。
+ 头饰：使用雕刻过的南瓜，但是需要清除雕刻过的南瓜戴在头上的视野限制效果。如果想实现背包与实际物品材质不同，可参考(http://www.mcbbs.net/thread-833056-1-1.html]物品头部/背包/手持显示不同材质/模型]。
+ 彩色物品：可使用自带色彩的物品，诸如烟火之星、皮革盔甲、药水(喷溅、滞留)，配合其自身颜色nbt可以实现彩色物品图案。但是这些物品除了烟火之星外均不能堆叠，且有独特性质，因此使用时要加以注意。
+ 可用于酿造，使用兔子腿(因为无其他合成用途)。
+ 盔甲：可以使用盔甲改材质，但是无法修改穿戴在身上时的显示材质。
+ 饮品，可使用药水材质模型修改。
+ 画等装饰，可以使用物品展示框修改模型，然后展示框带有实体tag，例如```
{
	"pools": [
		{
			"rolls": 1,
			"entries": [
				{
					"type": "item",
					"name": "minecraft:item_frame",
					"functions": [
						{
							"function": "set_nbt",
							"tag": "{display:{Name:'{\"translate\":\"item.cpp.classical_painting\"}'},id:'cpp:classical_painting',CustomModelData:12970002,EntityTag:{Item:{id:'minecraft:firework_star',Count:1b,tag:{CustomModelData:12974001,isMachineBg:1b}},Tags:['cpp_item_frame_classical_painting','cpp_special_item_frame']}}"
						}
					]
				}
			]
		}
	]
}
```
此外，自定义的玩家头颅的样式极为丰富，而且无需绘制材质即可使用，但是注意需要联网使用。以下两个网站列出了大量可用的头颅样式
(https://heads.freshcoal.com/maincollection.php]Freshcoal]
(https://minecraft-heads.com/custom/heads]Minecraft Heads]
这些头颅类别丰富，且均为可放置的方块(玩家头颅)，因此在模组应用中十分常见。另外还可将图片上传至minecraft.net域名下，以实现自定义头颅图案，参见(http://www.mcbbs.net/thread-824528-1-1.html]自定义方块(玩家头颅)]。

自定义地图可用来显示自定义的图案，这个方法可避免使用资源包，但需将data文件与数据包一同发布。首先确定好长宽比例，然后可使用(https://mc-map.djfun.de]该网站]在线转换。注意，请先在Settings将地图中心设置足够远以避免玩家会刷新地图图案，例如将X center和Z center设置为10240000。另外在Step 5输出时，选择一个较大的地图data，例如10000，为玩家正常使用地图预留足够的空间。最后将其放入"世界名称/data"文件夹，并与数据包一同发布。使用如下命令获取：
```
give @s minecraft:filled_map{map:10000}
```选择负数的自定义地图的编号，或者手动将data文件夹中的idcounts调大，也可避免冲突。

### §4.4 发布
当你设计并制作好全部内容且通过测试后，将你的数据包以及其它可能的内容，如地图、data文件、资源包等一同发布。采用合适的版本号管理，并在发布时注明你所使用的命名空间、记分板、组、标签、地图区段、资源包等内容，以便于其他开发者整合或避免冲突。

[page]
从此处起，我们将通过一系列的例子来说明常见的效果时如何实现的，这些例子大部分来自于(http://www.mcbbs.net/thread-696861-1-1.html]更多的合成]，大家可以自行拆包查看。
## ### ## ### §5 合## 成
### ## ### ## ### §5.1 原版有序合成
原版的合成、烧炼使用json即可实现，较为简单，但是无法识别nbt，因此只能实现原版物品的合成和烧炼。同时模组若使用了相关物品，则相应的模组物品亦可代替原物品进行合成。
**例** 使用羊毛+鸡蛋有序合成两个羊刷怪蛋。
cpp/recipes/sheep_spawn_egg.json
```
{
		"type": "crafting_shaped",
		"pattern": [
				"###",
				"#*#",
				"###"
		],
		"key": {
				"*": {
						"item": "minecraft:egg"
				},
				"#": {
						"tag": "cpp:wools"
				}
		},
		"result": {
				"item": "minecraft:sheep_spawn_egg",
				"count":2
		}
}
```"type": "crafting_shaped"表示有序合成，pattern表示合成的样式，*和#分别表示两件物品(或物品tags)，key表明了*代表鸡蛋、#代表物品标签cpp:wools（包含了所有羊毛，需在标签中定义），result表示产物，"count"若没有则默认为1。

### ## ### ## ### §5.2 原版无序合成
**例** 使用2沙子+红石=2红沙。
cpp/recipes/red_sand.json
```
{
		"type": "crafting_shapeless",
		"ingredients": [
				{
								"item": "minecraft:sand"
				},
				{
								"item": "minecraft:sand"
				},
				{
								"item": "minecraft:redstone"
				}
		],
		"result": {
				"item": "minecraft:red_sand",
				"count":2
		}
}
```"type": "crafting_shapeless"表示无序合成，ingredients表示配方，配料可以重复。单个物品请使用有序合成而不是无序合成。

### ## ### ## ### §5.3 切石机配方
例如使用切石机切割木板：
```
{
	"type": "stonecutting",
	"ingredient": {
		"item": "minecraft:oak_planks"
	},
	"result": "minecraft:oak_slab",
	"count": 2
}
```
### ### ## ### ## ### §5.4 覆盖原版配方
如果想要修改原版的合成或熔炼配方，先使用诸如7-zip打开版本.jar文件，依次打开data/minecraft/recipes，找到相应的json，然后在自己的数据包中的相同位置(必然是minecraft命名空间)放入同名json即可覆盖默认的配方。
**例** 将橡木台阶合成数量改为8。
minecraft/recipes/oak_stairs.json
```
{
		"type": "crafting_shaped",
		"group": "wooden_stairs",
		"pattern": [
				"#  ",
				"## ",
				"###"
		],
		"key": {
				"#": {
						"item": "minecraft:oak_planks"
				}
		},
		"result": {
				"item": "minecraft:oak_stairs",
				"count": 8
		}
}

```**例** 将原版白色床+墨囊=黑色床的合成配方修改为任意床+墨囊=黑色床。
先定义标签 cpp/tags/items/beds.json
```
{
		"replace": false,
		"values": [
				"minecraft:white_bed",
				"minecraft:orange_bed",
				"minecraft:magenta_bed",
				"minecraft:light_blue_bed",
				"minecraft:yellow_bed",
				"minecraft:lime_bed",
				"minecraft:pink_bed",
				"minecraft:gray_bed",
				"minecraft:light_gray_bed",
				"minecraft:cyan_bed",
				"minecraft:purple_bed",
				"minecraft:blue_bed",
				"minecraft:brown_bed",
				"minecraft:green_bed",
				"minecraft:red_bed",
				"minecraft:black_bed"
		]
}
```minecraft/recipes/black_bed_from_white_bed.json```
{
		"type": "crafting_shapeless",
		"group": "dyed_bed",
		"ingredients": [
				{
						"tag": "cpp:beds"
				},
				{
						"item": "minecraft:black_dye"
				}
		],
		"result": {
				"item": "minecraft:black_bed"
		}
}
```如果需要删除原版配方，可使用生存无法获得的方块如基岩、屏障、结构空位等物品来合成。配方json为空会导致原配方生效而不是无法合成。

### ### ### ## ### ## ### §5.5 容器合成
使用箱子既可实现自定义GUI，又可用于含nbt物品合成。我们需要使用辅助的隐形实体来帮助定位。

手持石化橡木台阶时，探测目标方块位置，放置箱子和带修改过的物品模型的盔甲架，并在箱子内填满材质与背景同色的占位物品。
使用进度判断是否放置了石化橡木台阶machine.json
```
{
		"criteria": {
				"machine": {
						"trigger": "minecraft:placed_block",
						"conditions": {
								"item": {
										"item":"minecraft:petrified_oak_slab"
								}
						}
				}
		},
		"rewards": {
				"function": "cpp:block/machine/adv"
		}
}
```cpp/functions/block/machine/get_pos.mcfunction
```
execute if entity @s[distance=..5] if block ~ ~ ~ petrified_oak_slab align xyz positioned ~0.5 ~ ~0.5 run summon area_effect_cloud ~ ~ ~ {Tags:["cpp_machine_pos"]}
execute if entity @s[distance=..5] unless block ~ ~ ~ petrified_oak_slab positioned ^ ^ ^0.005 run function cpp:block/machine/get_pos```cpp/functions/block/machine/adv.mcfunction
```
advancement revoke @s only cpp:block/machine
execute store result score @s cppValue run data get entity @s SelectedItem.tag.CustomModelData
execute unless entity @s[nbt={SelectedItem:{id:"minecraft:petrified_oak_slab"}}] store result score @s cppValue run data get entity @s Inventory[{Slot:-106b}].tag.CustomModelData
execute at @s positioned ~ ~1.62 ~ run function cpp:block/machine/get_pos
execute at @e[tag=cpp_machine_pos] as @s[scores={cppValue=0}] run function cpp:block/machine/crafting_machine```cpp/functions/block/machine/crafting_machine.mcfunction
```
function cpp:get_facing
summon armor_stand ~ ~ ~ {Invulnerable:1b,Invisible:1b,Small:1b,Marker:1b,NoGravity:1b,DisabledSlots:7967,Tags:["cpp_machine","cpp_crafting_machine","cpp_barrel","cpp_need_fire"],Rotation:[0.0f,0.0f]}
loot replace entity @e[tag=cpp_crafting_machine,distance=..0.1,limit=1] armor.head loot cpp:crafting_machine
setblock ~ ~ ~ barrel{CustomName:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"}
kill @e[tag=cpp_machine_pos]```cpp/functions/get_facing.mcfunction
```
execute store result score @s cppValue run data get entity @s Rotation[0]
scoreboard players add @s cppValue 225
execute if score @s cppValue matches ..-1 run scoreboard players add @s cppValue 360
execute if score @s cppValue matches 360.. run scoreboard players remove @s cppValue 360
scoreboard players set #90 cppValue 90
scoreboard players operation @s cppValue /= #90 cppValue```主函数中清除玩家背包、地面、漏斗矿车、漏斗含isMachineBg:1b的所有物品(占位用的辅助物品，不应当被玩家获取)。若盔甲出方块被破坏，则将箱子掉落物替换为原物品(胡萝卜钓竿)。若一切正常，执行下一步nbt的探测。
```

execute as @e[type=armor_stand,tag=cpp_need_fire] run data merge entity @s {Fire:32767s}
execute as @e[type=armor_stand,tag=cpp_barrel] at @s unless block ~ ~ ~ barrel run function cpp:block/machine/break_barrel
execute as @e[tag=cpp_crafting_machine] at @s if entity @a[distance=..5] run function cpp:craft/craft
kill @e[type=item,nbt={Item:{tag:{isMachineBg:1b}}}]
clear @a firework_star{isMachineBg:1b}
execute as @e[type=hopper_minecart,nbt={Items:[{tag:{isMachineBg:1b}}]}] run function cpp:block/machine/clear_hopper_minecart
execute at @e[tag=cpp_machine] if block ~ ~-1 ~ hopper{Items:[{tag:{isMachineBg:1b}}]} run function cpp:block/machine/clear_hopper```部分内容省略，请参考更多的合成原版模组。

我们先做好GUI
```
execute unless data block ~ ~ ~ Items[{Slot:0b}] run replaceitem block ~ ~ ~ container.0 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971010}
execute unless data block ~ ~ ~ Items[{Slot:4b}] run replaceitem block ~ ~ ~ container.4 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:5b}] run replaceitem block ~ ~ ~ container.5 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:6b}] run replaceitem block ~ ~ ~ container.6 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:7b}] run replaceitem block ~ ~ ~ container.7 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:8b}] run replaceitem block ~ ~ ~ container.8 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}

execute unless data block ~ ~ ~ Items[{Slot:9b}] run replaceitem block ~ ~ ~ container.9 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:13b}] run replaceitem block ~ ~ ~ container.13 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:14b}] run replaceitem block ~ ~ ~ container.14 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:15b}] run replaceitem block ~ ~ ~ container.15 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute if data block ~ ~ ~ Items[{Slot:16b,tag:{isMachineBg:1b}}] run replaceitem block ~ ~ ~ container.16 air
execute unless data block ~ ~ ~ Items[{Slot:17b}] run replaceitem block ~ ~ ~ container.17 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:18b}] run replaceitem block ~ ~ ~ container.18 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:22b}] run replaceitem block ~ ~ ~ container.22 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:23b}] run replaceitem block ~ ~ ~ container.23 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:24b}] run replaceitem block ~ ~ ~ container.24 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:25b}] run replaceitem block ~ ~ ~ container.25 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}
execute unless data block ~ ~ ~ Items[{Slot:26b}] run replaceitem block ~ ~ ~ container.26 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"block.minecraft.petrified_oak_slab\"}"},CustomModelData:12971000}

execute if block ~ ~ ~ barrel{Items:[{Slot:0b,tag:{isMachineBg:1b}},{Slot:4b,tag:{isMachineBg:1b}},{Slot:5b,tag:{isMachineBg:1b}},{Slot:6b,tag:{isMachineBg:1b}},{Slot:7b,tag:{isMachineBg:1b}},{Slot:8b,tag:{isMachineBg:1b}},{Slot:9b,tag:{isMachineBg:1b}},{Slot:13b,tag:{isMachineBg:1b}},{Slot:14b,tag:{isMachineBg:1b}},{Slot:15b,tag:{isMachineBg:1b}},{Slot:17b,tag:{isMachineBg:1b}},{Slot:18b,tag:{isMachineBg:1b}},{Slot:22b,tag:{isMachineBg:1b}},{Slot:23b,tag:{isMachineBg:1b}},{Slot:24b,tag:{isMachineBg:1b}},{Slot:25b,tag:{isMachineBg:1b}},{Slot:26b,tag:{isMachineBg:1b}}]} unless data block ~ ~ ~ Items[{Slot:16b}] run function cpp:craft/type```然后我们先判断容器的物品槽位数量来分类
```
execute store result score @s cppValue run data get block ~ ~ ~ Items
function #cpp:craft
# 全部格子
execute as @s[scores={cppValue=26}] run function cpp:craft/shape_all
# 十字形
execute as @s[scores={cppValue=22}] if block ~ ~ ~ barrel{Items:[{Slot:2b},{Slot:10b},{Slot:11b},{Slot:12b},{Slot:20b}]} run function cpp:craft/shape_cross
# 无序合成
execute as @s[scores={cppValue=22}] run function cpp:craft/shapeless5
execute if data block ~ ~ ~ Items[{Slot:16b}] run function cpp:craft/clear_all```根据类别来合成，
```
execute if block ~ ~ ~ barrel{Items:[{id:"minecraft:sugar"},{id:"minecraft:rotten_flesh"},{id:"minecraft:glistering_melon_slice"},{id:"minecraft:gunpowder"},{id:"minecraft:potion",tag:{Potion:"minecraft:water"}}]} run loot replace block ~ ~ ~ container.16 loot cpp:acid```然后进入清理阶段```
execute if data block ~ ~ ~ Items[{Slot:16b,tag:{id:"cpp:cheese"}}] run data modify block ~ ~ ~ Items[{id:"minecraft:milk_bucket"}].Count set value 2
execute if data block ~ ~ ~ Items[{Slot:16b,tag:{id:"cpp:cheese"}}] run data modify block ~ ~ ~ Items[{id:"minecraft:milk_bucket"}].id set value "minecraft:bucket"
execute if data block ~ ~ ~ Items[{Slot:16b,tag:{id:"cpp:high_temperature_plugin"}}] run data modify block ~ ~ ~ Items[{id:"minecraft:lava_bucket"}].Count set value 2
execute if data block ~ ~ ~ Items[{Slot:16b,tag:{id:"cpp:high_temperature_plugin"}}] run data modify block ~ ~ ~ Items[{id:"minecraft:lava_bucket"}].id set value "minecraft:bucket"

execute store result score #temp cppValue run data get block ~ ~ ~ Items[{Slot:21b}].Count
execute store result block ~ ~ ~ Items[{Slot:21b}].Count byte 1 run scoreboard players remove #temp cppValue 1
execute store result score #temp cppValue run data get block ~ ~ ~ Items[{Slot:20b}].Count
execute store result block ~ ~ ~ Items[{Slot:20b}].Count byte 1 run scoreboard players remove #temp cppValue 1
execute store result score #temp cppValue run data get block ~ ~ ~ Items[{Slot:19b}].Count
execute store result block ~ ~ ~ Items[{Slot:19b}].Count byte 1 run scoreboard players remove #temp cppValue 1
execute store result score #temp cppValue run data get block ~ ~ ~ Items[{Slot:12b}].Count
execute store result block ~ ~ ~ Items[{Slot:12b}].Count byte 1 run scoreboard players remove #temp cppValue 1
execute store result score #temp cppValue run data get block ~ ~ ~ Items[{Slot:11b}].Count
execute store result block ~ ~ ~ Items[{Slot:11b}].Count byte 1 run scoreboard players remove #temp cppValue 1
execute store result score #temp cppValue run data get block ~ ~ ~ Items[{Slot:10b}].Count
execute store result block ~ ~ ~ Items[{Slot:10b}].Count byte 1 run scoreboard players remove #temp cppValue 1
execute store result score #temp cppValue run data get block ~ ~ ~ Items[{Slot:3b}].Count
execute store result block ~ ~ ~ Items[{Slot:3b}].Count byte 1 run scoreboard players remove #temp cppValue 1
execute store result score #temp cppValue run data get block ~ ~ ~ Items[{Slot:2b}].Count
execute store result block ~ ~ ~ Items[{Slot:2b}].Count byte 1 run scoreboard players remove #temp cppValue 1
execute store result score #temp cppValue run data get block ~ ~ ~ Items[{Slot:1b}].Count
execute store result block ~ ~ ~ Items[{Slot:1b}].Count byte 1 run scoreboard players remove #temp cppValue 1```如果不借助额外的实体，我们可以通过与容器交互的计分板判据和(http://www.mcbbs.net/thread-771638-1-1.html]方块追踪]来实现。
**例** 当朝上的发射器内正中间包含一个泥土时，右击其上方的工作台将泥土替换为钻石。
创建计分板
```
scoreboard objectives add cppUseDisp minecraft.custom:minecraft.interact_with_crafting_table```主函数
```
execute at @e[tag=cpp_tpback_aec] run tp @a[tag=cpp_tpback] ~ ~ ~
tag @a[tag=cpp_tpback] remove cpp_tpback
execute as @a[scores={cppUseDisp=1..}] at @s positioned ~ ~1.62 ~ run function cpp:ray```ray.mcfunction
```
execute if entity @s[distance=..5] unless block ~ ~ ~ crafting_table positioned ^ ^ ^0.005 run function cpp:ray
execute if entity @s[distance=..5] if block ~ ~ ~ crafting_table run scoreboard players set @s cppUseDisp 0
execute if entity @s[distance=..5] if block ~ ~ ~ crafting_table if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,id:"minecraft:dirt",Count:1b}]} run function cpp:craft```craft.mcfunction
```
replaceitem block ~ ~-1 ~ container.4 diamond
execute at @s run summon area_effect_cloud ~ ~ ~ {Tags:["cpp_tpback_aec"],Duration:2}
tp @s ~ ~256 ~
tag @s add cpp_tpback```配合战利品表还可方便地实现随机合成。

也可使用带背包的实体合成，例如玩家、矿车箱子、矿车漏斗、驴骡羊驼等。方法类似，这里不再赘述。

如果添加的合成比较少，采用扔在地上的物品合成也是一种简便的方法。例如
```
execute as @e[type=item,nbt={Item:{tag:{id:"cpp:magnet"}}}] at @s if entity @e[type=item,distance=..1,nbt={Item:{id:"minecraft:diamond",Count:4b}}] run function cpp:powered_magnet```cpp/functions/powered_magnet.mcfunction
```
kill @e[type=item,limit=1,distance=..1,nbt={Item:{id:"minecraft:diamond",Count:4b}}]
kill @s
summon item ~ ~ ~ {Item:{id:"minecraft:compass",Count:1b,tag:{id:"cpp:powered_magnet"}}}
```可将地面的含id:"cpp:magnet"的物品和4个钻石合成为含id:"cpp:powered_magnet"的指南针。

如果我们希望合成需要一定的时长，我们可以添加一个记分板，然后每刻对相应的实体分数+1，最后操作达到指定分数的实体，并重置分数。计时在制作机器时几乎是必需的。总之合成方式可以有千万种做法，选择一种适合自己模组的即可。
[page]    
### ### ## ### ## ### §6 ## 熔炼和酿造
### ### ### ## ### ## ### §6.1 ### 原版熔炼
**例** 烧炼皮革装备、腐肉、鞍为兔子皮。
cpp/recipes/rabbit_hide_from_smelting.json
```
{
		"type": "smelting",
		"ingredient": [
				{
						"item": "minecraft:rotten_flesh"
				},
				{
						"item": "minecraft:leather_helmet"
				},
				{
						"item": "minecraft:leather_chestplate"
				},
				{
						"item": "minecraft:leather_leggings"
				},
				{
						"item": "minecraft:leather_boots"
				},
				{
						"item": "minecraft:saddle"
				}
		],
		"result": "minecraft:rabbit_hide",
		"experience": 0.1,
		"cookingtime": 200
}
```其余不再赘述，experience表示每个物品烧炼完成后可获得的经验，cookingtime表示熔炼需要200刻=10秒。
此外，这里的ingredient以及有序合成中"*"等处均可使用[{},{}]来表达多个可选的物品，或者{}单个物品。

type可以为smelting(熔炉)，blasting(高炉)，smoking(烟熏炉)，campfire_cooking(营火)。

### ### ### ### ## ### ## ### §6.2 自定义熔炼
通过放置方块的判据，我们可以自定义熔炼。
**例**；将蛋烧炼为id:"cpp:egg_stew"的蘑菇煲。

创建烧炼配方以激活熔炼蛋：
cpp/recipes/egg.json
```
{
		"type": "smelting",
		"ingredient": {
				"item": "minecraft:egg"
		},
		"result": "minecraft:mushroom_stew",
		"experience": 0.1,
		"cookingtime": 200
}
```
创建放置熔炉的进度：
cpp:advancements/foods/put_furnace.json
```
{
		"parent": "cpp:foods/root",
		"criteria": {
				"put_furnace": {
						"trigger": "minecraft:placed_block",
						"conditions": {
								"block": "minecraft:furnace"
						}
				}
		},
		"rewards": {
				"function": "cpp:foods/system/put_furnace"
		}
}
```cpp:foods/system/put_furnace.mcfunction
```
execute at @s positioned ~ ~1.62 ~ run function cpp:foods/system/ray_furnace
advancement revoke @s only cpp:foods/put_furnace```cpp:foods/system/ray_furnace.mcfunction
```
execute if entity @s[distance=..5] if block ~ ~ ~ minecraft:furnace align xyz run summon minecraft:armor_stand ~0.5 ~ ~0.5 {Invulnerable:1b,Invisible:1b,NoGravity:1b,Tags:["cpp_furnace"],Marker:1b}
execute if entity @s[distance=..5] unless block ~ ~ ~ minecraft:furnace positioned ^ ^ ^0.005 run function cpp:foods/system/ray_furnace```这里注意生存玩家的手长4.5米，创造玩家的手长5米，这里设定最长5米即足够。至此，放置熔炉已完成。

然后在烧炼时间达到199s时，替换熔炉内的物品。
主函数```
execute as @e[type=minecraft:armor_stand,tag=cpp_furnace] at @s unless block ~ ~ ~ minecraft:furnace run kill @s
execute as @e[type=minecraft:armor_stand,tag=cpp_furnace] at @s if block ~ ~ ~ minecraft:furnace{CookTime:199s} run function cpp:foods/cook/check```cpp:foods/cook/check.mcfunction
```
execute if block ~ ~ ~ minecraft:furnace{Items:[{Slot:0b,id:"minecraft:egg"}]} run function cpp:foods/cook/egg_stew
...```cpp:foods/cook/egg_stew
```
replaceitem block ~ ~ ~ container.2 mushroom_stew{display:{"Name":"{\"translate\":\"item.cpp.egg_stew\"}"},id:"cpp:egg_stew"}
execute store result score @s cppCount run data get block ~ ~ ~ Items[0].Count
execute store result block ~ ~ ~ Items[0].Count byte 1 run scoreboard players remove @s cppCount 1
data merge block ~ ~ ~ {CookTime:0s}
```注意，这种做法的局限性一是若要求待烧炼物含指定nbt，则必须添加该物品的的烧炼配方，这就导致即使没有相应的nbt也会烧炼，个人建议添加为原物品也添加合理的烧炼配方，或者烧炼配方的产物和待烧炼物相同，同时不奖励经验值；二是即使产物应当可堆叠也无法正常堆叠，这时需配合漏斗等设备传输方可持续烧炼。

### ### ### ### ## ### ## ### §6.3 食物
食物可通过进度来探测，通过饱和效果来模拟回复饥饿值。
**例** 使用土豆牛肉回复16饥饿值并给予30秒力量II效果。
cpp:advancements/foods/braised_beef_with_potatoes.json
```
{
		"parent": "cpp:foods/root",
		"criteria": {
		   "braised_beef_with_potatoes": {
				   "trigger": "minecraft:consume_item",
				   "conditions": {
						   "item": {
								   "item": "minecraft:rabbit_stew",
								   "nbt": "{id:\"cpp:braised_beef_with_potatoes\"}"
								}
						}
				}
		},
		"rewards":{
				"function": "cpp:foods/foods/braised_beef_with_potatoes"
		}
}
```cpp:foods/foods/braised_beef_with_potatoes.mcfunction
```
effect give @s strength 30 1
effect give @s saturation 1 5
advancement revoke @s only cpp:food/braised_beef_with_potatoes```注意该物品必须为原版已有的食物。

### ### ### ### ## ### ## ### §6.4 自定义酿造
类似于自定义熔炼的方法，我们可以自定义少量的酿造。这要求酿造材料必须为原版酿造材料物品。

**例** 使用神秘烈焰粉(cpp:mystery_blaze_powder)将粗制的药水酿造成有多重药水效果的鲁莽药水(potion_of_reckless)，同时支持延长、加强、喷溅、滞留版本。
主要思路是通过potionType:["",""]来判断药水的状态(原版/延长/加强、瓶装/喷溅/滞留)来区分状态，通过药水的原版{Potion:"minecraft:swiftness"}来实现酿造台的酿造。

放置和探测酿造台的部分省略，假设已有相应的标签为cpp_brewing_stand的盔甲架。
主函数
```
execute as @e[type=minecraft:armor_stand,tag=cpp_brewing_stand] at @s unless block ~ ~ ~ minecraft:brewing_stand run kill @s
execute as @e[type=minecraft:armor_stand,tag=cpp_brewing_stand] at @s if block ~ ~ ~ minecraft:brewing_stand{BrewTime:1s} run function cpp:foods/brew/check```cpp:brew/check.mcfunction 区分酿造材料和药水类型
```
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:blaze_powder",tag:{id:"cpp:mystery_blaze_powder"}}]} run function cpp:foods/brew/potion_of_reckless

execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:redstone"},{Slot:0b,tag:{potionType:["normal"]}}]} run tag @s add cpp_potion_of_long
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:redstone"},{Slot:1b,tag:{potionType:["normal"]}}]} run tag @s add cpp_potion_of_long
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:redstone"},{Slot:2b,tag:{potionType:["normal"]}}]} run tag @s add cpp_potion_of_long
execute as @s[tag=cpp_potion_of_long] run function cpp:foods/brew/potion_of_long

execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:glowstone_dust"},{Slot:0b,tag:{potionType:["normal"]}}]} run tag @s add cpp_potion_of_strong
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:glowstone_dust"},{Slot:1b,tag:{potionType:["normal"]}}]} run tag @s add cpp_potion_of_strong
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:glowstone_dust"},{Slot:2b,tag:{potionType:["normal"]}}]} run tag @s add cpp_potion_of_strong
execute as @s[tag=cpp_potion_of_strong] run function cpp:foods/brew/potion_of_strong

execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:gunpowder"},{Slot:0b,id:"minecraft:potion",tag:{potionType:["potion"]}}]} run tag @s add cpp_potion_of_splash
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:gunpowder"},{Slot:1b,id:"minecraft:potion",tag:{potionType:["potion"]}}]} run tag @s add cpp_potion_of_splash
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:gunpowder"},{Slot:2b,id:"minecraft:potion",tag:{potionType:["potion"]}}]} run tag @s add cpp_potion_of_splash
execute as @s[tag=cpp_potion_of_splash] run function cpp:foods/brew/potion_of_splash

execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:dragon_breath"},{Slot:0b,id:"minecraft:splash_potion",tag:{potionType:["splash"]}}]} run tag @s add cpp_potion_of_lingering
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:dragon_breath"},{Slot:1b,id:"minecraft:splash_potion",tag:{potionType:["splash"]}}]} run tag @s add cpp_potion_of_lingering
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:3b,id:"minecraft:dragon_breath"},{Slot:2b,id:"minecraft:splash_potion",tag:{potionType:["splash"]}}]} run tag @s add cpp_potion_of_lingering
execute as @s[tag=cpp_potion_of_lingering] run function cpp:foods/brew/potion_of_lingering```cpp:foods/brew/potion_of_reckless 酿造鲁莽药水，原药水可以为粗制的药水、喷溅型粗制的药水和滞留型粗制的药水。
```
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b,id:"minecraft:potion",tag:{Potion:"minecraft:awkward"}}]} run replaceitem block ~ ~ ~ container.0 potion{Potion:"minecraft:swiftness",CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:11b,Duration:3600},{Id:12b,Duration:3600},{Id:16b,Duration:3600}],id:"cpp:potion_of_reckless",potionType:["normal","potion"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b,id:"minecraft:potion",tag:{Potion:"minecraft:awkward"}}]} run replaceitem block ~ ~ ~ container.1 potion{Potion:"minecraft:swiftness",CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:11b,Duration:3600},{Id:12b,Duration:3600},{Id:16b,Duration:3600}],id:"cpp:potion_of_reckless",potionType:["normal","potion"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b,id:"minecraft:potion",tag:{Potion:"minecraft:awkward"}}]} run replaceitem block ~ ~ ~ container.2 potion{Potion:"minecraft:swiftness",CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:11b,Duration:3600},{Id:12b,Duration:3600},{Id:16b,Duration:3600}],id:"cpp:potion_of_reckless",potionType:["normal","potion"]}

execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b,id:"minecraft:splash_potion",tag:{Potion:"minecraft:awkward"}}]} run replaceitem block ~ ~ ~ container.0 splash_potion{Potion:"minecraft:swiftness",CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:11b,Duration:3600},{Id:12b,Duration:3600},{Id:16b,Duration:3600}],id:"cpp:potion_of_reckless",potionType:["normal","splash"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b,id:"minecraft:splash_potion",tag:{Potion:"minecraft:awkward"}}]} run replaceitem block ~ ~ ~ container.1 splash_potion{Potion:"minecraft:swiftness",CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:11b,Duration:3600},{Id:12b,Duration:3600},{Id:16b,Duration:3600}],id:"cpp:potion_of_reckless",potionType:["normal","splash"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b,id:"minecraft:splash_potion",tag:{Potion:"minecraft:awkward"}}]} run replaceitem block ~ ~ ~ container.2 splash_potion{Potion:"minecraft:swiftness",CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:11b,Duration:3600},{Id:12b,Duration:3600},{Id:16b,Duration:3600}],id:"cpp:potion_of_reckless",potionType:["normal","splash"]}

execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b,id:"minecraft:lingering_potion",tag:{Potion:"minecraft:awkward"}}]} run replaceitem block ~ ~ ~ container.0 lingering_potion{Potion:"minecraft:swiftness",CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:11b,Duration:3600},{Id:12b,Duration:3600},{Id:16b,Duration:3600}],id:"cpp:potion_of_reckless",potionType:["normal","lingering"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b,id:"minecraft:lingering_potion",tag:{Potion:"minecraft:awkward"}}]} run replaceitem block ~ ~ ~ container.1 lingering_potion{Potion:"minecraft:swiftness",CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:11b,Duration:3600},{Id:12b,Duration:3600},{Id:16b,Duration:3600}],id:"cpp:potion_of_reckless",potionType:["normal","lingering"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b,id:"minecraft:lingering_potion",tag:{Potion:"minecraft:awkward"}}]} run replaceitem block ~ ~ ~ container.2 lingering_potion{Potion:"minecraft:swiftness",CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:11b,Duration:3600},{Id:12b,Duration:3600},{Id:16b,Duration:3600}],id:"cpp:potion_of_reckless",potionType:["normal","lingering"]}

scoreboard players set @s cppSlotsDown 0
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b}]} run scoreboard players add @s cppSlotsDown 1
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b}]} run scoreboard players add @s cppSlotsDown 1
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b}]} run scoreboard players add @s cppSlotsDown 1

execute as @s[scores={cppSlotsDown=1}] store result score @s cppCount run data get block ~ ~ ~ Items[1].Count
execute as @s[scores={cppSlotsDown=1}] store result block ~ ~ ~ Items[1].Count byte 1 run scoreboard players remove @s cppCount 1
execute as @s[scores={cppSlotsDown=2}] store result score @s cppCount run data get block ~ ~ ~ Items[2].Count
execute as @s[scores={cppSlotsDown=2}] store result block ~ ~ ~ Items[2].Count byte 1 run scoreboard players remove @s cppCount 1
execute as @s[scores={cppSlotsDown=3}] store result score @s cppCount run data get block ~ ~ ~ Items[3].Count
execute as @s[scores={cppSlotsDown=3}] store result block ~ ~ ~ Items[3].Count byte 1 run scoreboard players remove @s cppCount 1```cpp:foods/brew/potion_of_long 长效药水，同样需要处理各种药水类型。
```
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b,id:"minecraft:potion",tag:{id:"cpp:potion_of_reckless"}}]} run replaceitem block ~ ~ ~ container.0 potion{CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:1b,Duration:9600},{Id:11b,Duration:9600},{Id:12b,Duration:9600},{Id:16b,Duration:9600}],id:"cpp:potion_of_long_reckless",potionType:["long","potion"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b,id:"minecraft:potion",tag:{id:"cpp:potion_of_reckless"}}]} run replaceitem block ~ ~ ~ container.1 potion{CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:1b,Duration:9600},{Id:11b,Duration:9600},{Id:12b,Duration:9600},{Id:16b,Duration:9600}],id:"cpp:potion_of_long_reckless",potionType:["long","potion"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b,id:"minecraft:potion",tag:{id:"cpp:potion_of_reckless"}}]} run replaceitem block ~ ~ ~ container.2 potion{CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:1b,Duration:9600},{Id:11b,Duration:9600},{Id:12b,Duration:9600},{Id:16b,Duration:9600}],id:"cpp:potion_of_long_reckless",potionType:["long","potion"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b,id:"minecraft:potion",tag:{id:"cpp:potion_of_ninja"}}]} run replaceitem block ~ ~ ~ container.0 potion{CustomPotionColor:6786184,display:{Name:"{\"translate\":\"item.cpp.potion_of_ninja\"}"},CustomPotionEffects:[{Id:8b,Duration:9600},{Id:10b,Duration:9600},{Id:13b,Duration:9600},{Id:14b,Duration:9600}],id:"cpp:potion_of_long_ninja",potionType:["long","potion"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b,id:"minecraft:potion",tag:{id:"cpp:potion_of_ninja"}}]} run replaceitem block ~ ~ ~ container.1 potion{CustomPotionColor:6786184,display:{Name:"{\"translate\":\"item.cpp.potion_of_ninja\"}"},CustomPotionEffects:[{Id:8b,Duration:9600},{Id:10b,Duration:9600},{Id:13b,Duration:9600},{Id:14b,Duration:9600}],id:"cpp:potion_of_long_ninja",potionType:["long","potion"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b,id:"minecraft:potion",tag:{id:"cpp:potion_of_ninja"}}]} run replaceitem block ~ ~ ~ container.2 potion{CustomPotionColor:6786184,display:{Name:"{\"translate\":\"item.cpp.potion_of_ninja\"}"},CustomPotionEffects:[{Id:8b,Duration:9600},{Id:10b,Duration:9600},{Id:13b,Duration:9600},{Id:14b,Duration:9600}],id:"cpp:potion_of_long_ninja",potionType:["long","potion"]}

execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b,id:"minecraft:splash_potion",tag:{id:"cpp:potion_of_reckless"}}]} run replaceitem block ~ ~ ~ container.0 splash_potion{CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_splash_reckless\"}"},CustomPotionEffects:[{Id:1b,Duration:9600},{Id:11b,Duration:9600},{Id:12b,Duration:9600},{Id:16b,Duration:9600}],id:"cpp:potion_of_long_reckless",potionType:["long","splash"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b,id:"minecraft:splash_potion",tag:{id:"cpp:potion_of_reckless"}}]} run replaceitem block ~ ~ ~ container.1 splash_potion{CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_splash_reckless\"}"},CustomPotionEffects:[{Id:1b,Duration:9600},{Id:11b,Duration:9600},{Id:12b,Duration:9600},{Id:16b,Duration:9600}],id:"cpp:potion_of_long_reckless",potionType:["long","splash"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b,id:"minecraft:splash_potion",tag:{id:"cpp:potion_of_reckless"}}]} run replaceitem block ~ ~ ~ container.2 splash_potion{CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_splash_reckless\"}"},CustomPotionEffects:[{Id:1b,Duration:9600},{Id:11b,Duration:9600},{Id:12b,Duration:9600},{Id:16b,Duration:9600}],id:"cpp:potion_of_long_reckless",potionType:["long","splash"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b,id:"minecraft:splash_potion",tag:{id:"cpp:potion_of_ninja"}}]} run replaceitem block ~ ~ ~ container.0 splash_potion{CustomPotionColor:6786184,display:{Name:"{\"translate\":\"item.cpp.potion_of_splash_ninja\"}"},CustomPotionEffects:[{Id:8b,Duration:9600},{Id:10b,Duration:9600},{Id:13b,Duration:9600},{Id:14b,Duration:9600}],id:"cpp:potion_of_long_ninja",potionType:["long","splash"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b,id:"minecraft:splash_potion",tag:{id:"cpp:potion_of_ninja"}}]} run replaceitem block ~ ~ ~ container.1 splash_potion{CustomPotionColor:6786184,display:{Name:"{\"translate\":\"item.cpp.potion_of_splash_ninja\"}"},CustomPotionEffects:[{Id:8b,Duration:9600},{Id:10b,Duration:9600},{Id:13b,Duration:9600},{Id:14b,Duration:9600}],id:"cpp:potion_of_long_ninja",potionType:["long","splash"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b,id:"minecraft:splash_potion",tag:{id:"cpp:potion_of_ninja"}}]} run replaceitem block ~ ~ ~ container.2 splash_potion{CustomPotionColor:6786184,display:{Name:"{\"translate\":\"item.cpp.potion_of_splash_ninja\"}"},CustomPotionEffects:[{Id:8b,Duration:9600},{Id:10b,Duration:9600},{Id:13b,Duration:9600},{Id:14b,Duration:9600}],id:"cpp:potion_of_long_ninja",potionType:["long","splash"]}

execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b,id:"minecraft:lingering_potion",tag:{id:"cpp:potion_of_reckless"}}]} run replaceitem block ~ ~ ~ container.0 lingering_potion{CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:1b,Duration:9600},{Id:11b,Duration:9600},{Id:12b,Duration:9600},{Id:16b,Duration:9600}],id:"cpp:potion_of_long_reckless",potionType:["long","lingering"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b,id:"minecraft:lingering_potion",tag:{id:"cpp:potion_of_reckless"}}]} run replaceitem block ~ ~ ~ container.1 lingering_potion{CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:1b,Duration:9600},{Id:11b,Duration:9600},{Id:12b,Duration:9600},{Id:16b,Duration:9600}],id:"cpp:potion_of_long_reckless",potionType:["long","lingering"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b,id:"minecraft:lingering_potion",tag:{id:"cpp:potion_of_reckless"}}]} run replaceitem block ~ ~ ~ container.2 lingering_potion{CustomPotionColor:8809335,display:{Name:"{\"translate\":\"item.cpp.potion_of_reckless\"}"},CustomPotionEffects:[{Id:1b,Duration:9600},{Id:11b,Duration:9600},{Id:12b,Duration:9600},{Id:16b,Duration:9600}],id:"cpp:potion_of_long_reckless",potionType:["long","lingering"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b,id:"minecraft:lingering_potion",tag:{id:"cpp:potion_of_ninja"}}]} run replaceitem block ~ ~ ~ container.0 lingering_potion{CustomPotionColor:6786184,display:{Name:"{\"translate\":\"item.cpp.potion_of_ninja\"}"},CustomPotionEffects:[{Id:8b,Duration:9600},{Id:10b,Duration:9600},{Id:13b,Duration:9600},{Id:14b,Duration:9600}],id:"cpp:potion_of_long_ninja",potionType:["long","lingering"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b,id:"minecraft:lingering_potion",tag:{id:"cpp:potion_of_ninja"}}]} run replaceitem block ~ ~ ~ container.1 lingering_potion{CustomPotionColor:6786184,display:{Name:"{\"translate\":\"item.cpp.potion_of_ninja\"}"},CustomPotionEffects:[{Id:8b,Duration:9600},{Id:10b,Duration:9600},{Id:13b,Duration:9600},{Id:14b,Duration:9600}],id:"cpp:potion_of_long_ninja",potionType:["long","lingering"]}
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b,id:"minecraft:lingering_potion",tag:{id:"cpp:potion_of_ninja"}}]} run replaceitem block ~ ~ ~ container.2 lingering_potion{CustomPotionColor:6786184,display:{Name:"{\"translate\":\"item.cpp.potion_of_ninja\"}"},CustomPotionEffects:[{Id:8b,Duration:9600},{Id:10b,Duration:9600},{Id:13b,Duration:9600},{Id:14b,Duration:9600}],id:"cpp:potion_of_long_ninja",potionType:["long","lingering"]}

scoreboard players set @s cppSlotsDown 0
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:0b}]} run scoreboard players add @s cppSlotsDown 1
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:1b}]} run scoreboard players add @s cppSlotsDown 1
execute if block ~ ~ ~ minecraft:brewing_stand{Items:[{Slot:2b}]} run scoreboard players add @s cppSlotsDown 1

execute as @s[scores={cppSlotsDown=1}] store result score @s cppCount run data get block ~ ~ ~ Items[1].Count
execute as @s[scores={cppSlotsDown=1}] store result block ~ ~ ~ Items[1].Count byte 1 run scoreboard players remove @s cppCount 1
execute as @s[scores={cppSlotsDown=2}] store result score @s cppCount run data get block ~ ~ ~ Items[2].Count
execute as @s[scores={cppSlotsDown=2}] store result block ~ ~ ~ Items[2].Count byte 1 run scoreboard players remove @s cppCount 1
execute as @s[scores={cppSlotsDown=3}] store result score @s cppCount run data get block ~ ~ ~ Items[3].Count
execute as @s[scores={cppSlotsDown=3}] store result block ~ ~ ~ Items[3].Count byte 1 run scoreboard players remove @s cppCount 1
tag @s remove cpp_potion_of_long```加强、喷溅、滞留版本的方法类似，这里省略了。

[page]    
### ### ### ## ### ## ### §7 ## 交易
在RPG模组中，使用村民交易是一种常见的特殊物品获得方式。需要注意的是，如果不希望交易产生经验值，需将rewardExp设置为0b，例如
```
summon minecraft:villager ~ ~ ~ {NoAI:true,Invulnerable:true,Silent:true,Offers:{Recipes:[
{maxUses:99999999,rewardExp:0b,buy:{id:"minecraft:coal",Count:1b},buyB:{id:"minecraft:stone",Count:8b},
sell:{id:"minecraft:coal",Count:1b,tag:{Enchantments:[{id:999}],display:{Name:"{\"translate\":\"item.cpp.nice_coal\"}"}}}}]}}
```将村民的{VillagerData:{profession:"minecraft:none"}可以确保村民不含交易。通过设置不同的VillagerData以及修改村民的头盔材质模型，可以将村民的外观和原版村民加以区分。例如(http://www.mcbbs.net/thread-772311-1-1.html]【活动】【原版模组】新春惊喜]。

**例** 将1/5的农民修改为林业员，收购36-40原木，出售树苗(二层交易)。
简单来说，在CareerLevel:1时生成相应的交易列表，并保存价格，然后再CareerLevel:2时，重新添加上这些交易和对应价格，以及新增的交易部分。
主函数
```
execute as @e[type=villager,tag=!tpp_level1,nbt={VillagerData:{level:1}}] run function tpp:level1/check
execute as @e[type=villager,tag=!tpp_level2,nbt={VillagerData:{level:2}}] run function tpp:level2/check```tpp:level1/check
```
scoreboard players set #random_min tppRandom 1
scoreboard players set #random_max tppRandom 24
function tpp:random

data remove entity @s[scores={tppRandom=1..9}] VillagerData.profession

# 林业员
execute as @s[scores={tppRandom=1}] run function tpp:level1/forester
# 书画师
execute as @s[scores={tppRandom=2}] run function tpp:level1/painter
# 圣诞老人
execute as @s[scores={tppRandom=3}] run function tpp:level1/santa_claus
# 药剂师
execute as @s[scores={tppRandom=4}] run function tpp:level1/pharmacist
# 末地使
execute as @s[scores={tppRandom=5}] run function tpp:level1/end_envoy
# 烟花师
execute as @s[scores={tppRandom=6}] run function tpp:level1/fireworker
# 园丁
execute as @s[scores={tppRandom=7}] run function tpp:level1/gardener
# 机械工
execute as @s[scores={tppRandom=8}] run function tpp:level1/mechanician
# 潜水员
execute as @s[scores={tppRandom=9}] run function tpp:level1/frogman

tag @s add tpp_level1
scoreboard players reset @s tppRandom
```tpp:level1/forester
```
tag @s add tpp_forester
data merge entity @s {CustomName:"{\"translate\":\"entity.minecraft.villager.forester\"}",ArmorItems:[{},{},{},{id:"minecraft:player_head",Count:1b,tag:{SkullOwner:{Id:"a5abd11d-9493-498b-b89b-e0b4327678f0",Properties:{textures:[{Value:"eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvYzViNWE1MzlkOTE5ZmE4YzQ4OTY2NDI0MjJlYzkxNWUzNzg1NDU3MTIxNGIzMjU1Mjk2YzdjNzQyNWZmYiJ9fX0="}]}}}}],ArmorDropChances:[-1.0f,-1.0f,-1.0f,-1.0f],Offers:{Recipes:[{buy:{id:"minecraft:oak_log",Count:36b},sell:{id:"minecraft:emerald",Count:1b},maxUses:7},{buy:{id:"minecraft:spruce_log",Count:36b},sell:{id:"minecraft:emerald",Count:1b},maxUses:7},{buy:{id:"minecraft:birch_log",Count:36b},sell:{id:"minecraft:emerald",Count:1b},maxUses:7},{buy:{id:"minecraft:jungle_log",Count:36b},sell:{id:"minecraft:emerald",Count:1b},maxUses:7},{buy:{id:"minecraft:acacia_log",Count:36b},sell:{id:"minecraft:emerald",Count:1b},maxUses:7},{buy:{id:"minecraft:dark_oak_log",Count:36b},sell:{id:"minecraft:emerald",Count:1b},maxUses:7}]}}

scoreboard players set #random_min tppRandom 28
scoreboard players set #random_max tppRandom 32
function tpp:random
execute store result entity @s Offers.Recipes[0].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players set #random_min tppRandom 28
scoreboard players set #random_max tppRandom 32
function tpp:random
execute store result entity @s Offers.Recipes[1].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players set #random_min tppRandom 28
scoreboard players set #random_max tppRandom 32
function tpp:random
execute store result entity @s Offers.Recipes[2].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players set #random_min tppRandom 28
scoreboard players set #random_max tppRandom 32
function tpp:random
execute store result entity @s Offers.Recipes[3].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players set #random_min tppRandom 28
scoreboard players set #random_max tppRandom 32
function tpp:random
execute store result entity @s Offers.Recipes[4].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players set #random_min tppRandom 28
scoreboard players set #random_max tppRandom 32
function tpp:random
execute store result entity @s Offers.Recipes[5].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players reset @s tppRandom
```tpp:level2/check
```
execute as @s[tag=tpp_forester] run function tpp:level2/forester
execute as @s[tag=tpp_painter] run function tpp:level2/painter
execute as @s[tag=tpp_pharmacist] run function tpp:level2/pharmacist
execute as @s[tag=tpp_end_envoy] run function tpp:level2/end_envoy
execute as @s[tag=tpp_fireworker] run function tpp:level2/fireworker
execute as @s[tag=tpp_gardener] run function tpp:level2/gardener
execute as @s[tag=tpp_mechanician] run function tpp:level2/mechanician
execute as @s[tag=tpp_frogman] run function tpp:level2/frogman
execute as @s[tag=tpp_frogman] run function tpp:level2/frogman

execute if score #craftingpp cppValue matches 1 as @s[nbt={VillagerData:{profession:"minecraft:butcher"}}] run data modify entity @s Offers.Recipes[3].sell merge value {tag:{display:{Lore:["{\"text\":\"§r????\"}"]}}}
execute if score #craftingpp cppValue matches 1 as @s[nbt={VillagerData:{profession:"minecraft:butcher"}}] run data modify entity @s Offers.Recipes[4].sell merge value {tag:{display:{Lore:["{\"text\":\"§r???\"}"]}}}

tag @s add tpp_level2
```tpp:level2/forester
```
data modify entity @s Offers.Recipes append value {buy:{id:"minecraft:emerald",Count:2b},sell:{id:"minecraft:oak_sapling",Count:1b},maxUses:7}
data modify entity @s Offers.Recipes append value {buy:{id:"minecraft:emerald",Count:2b},sell:{id:"minecraft:spruce_sapling",Count:1b},maxUses:7}
data modify entity @s Offers.Recipes append value {buy:{id:"minecraft:emerald",Count:2b},sell:{id:"minecraft:birch_sapling",Count:1b},maxUses:7}
data modify entity @s Offers.Recipes append value {buy:{id:"minecraft:emerald",Count:2b},sell:{id:"minecraft:jungle_sapling",Count:1b},maxUses:7}
data modify entity @s Offers.Recipes append value {buy:{id:"minecraft:emerald",Count:2b},sell:{id:"minecraft:acacia_sapling",Count:1b},maxUses:7}
data modify entity @s Offers.Recipes append value {buy:{id:"minecraft:emerald",Count:2b},sell:{id:"minecraft:dark_oak_sapling",Count:1b},maxUses:7}

scoreboard players set #random_min tppRandom 2
scoreboard players set #random_max tppRandom 4
function tpp:random
execute store result entity @s Offers.Recipes[6].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players set #random_min tppRandom 2
scoreboard players set #random_max tppRandom 4
function tpp:random
execute store result entity @s Offers.Recipes[7].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players set #random_min tppRandom 2
scoreboard players set #random_max tppRandom 4
function tpp:random
execute store result entity @s Offers.Recipes[8].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players set #random_min tppRandom 2
scoreboard players set #random_max tppRandom 4
function tpp:random
execute store result entity @s Offers.Recipes[9].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players set #random_min tppRandom 2
scoreboard players set #random_max tppRandom 4
function tpp:random
execute store result entity @s Offers.Recipes[10].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players set #random_min tppRandom 2
scoreboard players set #random_max tppRandom 4
function tpp:random
execute store result entity @s Offers.Recipes[11].buy.Count byte 1 run scoreboard players get @s tppRandom

scoreboard players reset @s tppRandom
```这里的random函数采用的是(http://www.mcbbs.net/thread-706030-1-4.html]2b的random(min,max)随机模块]。

[page]    
### ### ### ## ### ## ### §8 ## 探测与触发
### ### ### ### ## ### ## ### §8.1 右击可投掷物
如果物品为喷溅、投掷药水、弓、雪球、鸡蛋、末影珍珠、末影之眼(有条件)，则右键后探测相应投射物并触发函数即可。如果是胡萝卜钓竿，则可由相应记分板判据探测。

理论上来说，投掷带自定义nbt标签的物品，对应的投掷物实体Item标签会包含这些nbt标签，这包括雪球、附魔之瓶等。但是由于在gametick中执行次序的问题，如果扔出的是最后一个物品，这个nbt无法被存储至这个投掷物实体。请当心这一点。

**例** 右键蓝色天之力(cpp:blue_force_of_sky)改变天气并消耗经验。
载入
```
scoreboard objectives add cppStatue dummy
scoreboard objectives add cppXpTotal dummy
scoreboard objectives add cppUseCSt1 minecraft.used:minecraft.carrot_on_a_stick```主函数
```
execute as @a[scores={cppUseCSt1=1..}] at @s run function cpp:elements/use```cpp:elements/use.mcfunction
```
execute as @s[nbt={SelectedItem:{tag:{id:"cpp:blue_force_of_sky"}}}] run function cpp:elements/use/blue
scoreboard players reset @s cppUseCSt1
```cpp:elements/use/blue.mcfunction
```
execute store result score @s cppXpTotal run data get entity @s XpTotal
tellraw @s[scores={cppXpTotal=..9}] {"translate":"item.cpp.elements.fail","with":[{"text":"10"}]}
execute as @s[scores={cppXpTotal=10..}] run function cpp:elements/use/blue_done```cpp:elements/use/blue_done.mcfunction
```
advancement grant @s only cpp:elements
advancement grant @s only cpp:weather
scoreboard players add #weather cppStatue 1
execute if score #weather cppStatue matches 4 run scoreboard players set #weather cppStatue 1
execute if score #weather cppStatue matches 1 run weather clear
execute if score #weather cppStatue matches 2 run weather rain
execute if score #weather cppStatue matches 3 run weather thunder
execute if score #weather cppStatue matches 1 run tellraw @a [{"translate":"item.cpp.blue_force_of_sky.info"},{"selector":"@s"},{"translate":"item.cpp.blue_force_of_sky.clear"}]
execute if score #weather cppStatue matches 2 run tellraw @a [{"translate":"item.cpp.blue_force_of_sky.info"},{"selector":"@s"},{"translate":"item.cpp.blue_force_of_sky.rain"}]
execute if score #weather cppStatue matches 3 run tellraw @a [{"translate":"item.cpp.blue_force_of_sky.info"},{"selector":"@s"},{"translate":"item.cpp.blue_force_of_sky.thunder"}]
xp add @s -10```**
例** 投掷ender_pearl{id:"cpp:transport_ball"}将玩家传送至所指方位（不超过100米），同时不消耗手中的末影珍珠。无视标签#cpp:fluid的所有方块（空气和水等）。
我们需要引入记分板延迟1tick记录玩家持有该物品。
初始化
```
#手持传送球
scoreboard objectives add cppHasTpball dummy
#使用传送球
scoreboard objectives add cppUsePearl minecraft.used:minecraft.ender_pearl```主函数
```
scoreboard players set @a[nbt={SelectedItem:{tag:{id:"cpp:transport_ball"}}}] cppHasTpball 2
scoreboard players remove @a[nbt=!{SelectedItem:{tag:{id:"cpp:transport_ball"}}}] cppHasTpball 1
execute as @a[scores={cppHasTpball=1..,cppUsePearl=1..}] at @s positioned ~ ~1.52 ~ run function cpp:transport```cpp/functions/transport.mcfunction
```
kill @e[type=ender_pearl,distance=..5,sort=nearest,limit=1]
scoreboard players set @s cppUsePearl 0
give @s minecraft:ender_pearl{display:{Name:"{\"translate\":\"item.cpp.transport_ball\"}"},id:"cpp:transport_ball",Enchantments:[{id:999s}]}
execute positioned ~ ~0.1 ~ run function cpp:transport_ray```cpp/functions/transport_ray.mcfunction
```
execute if entity @s[distance=..100] unless block ~ ~ ~ #cpp:fluid run tp @s ^ ^ ^-0.1
execute if entity @s[distance=..100] if block ~ ~ ~ #cpp:fluid positioned ^ ^ ^0.005 run function cpp:sys/transport_ray```
### ### ### ### ## ### ## ### §8.2 装备效果
如果物品本身为永久生效，探测(带槽位的)背包即可。如果与玩家的血量、饥饿值有关，则通过探测相应判据的计分板即可。
**例** 当玩家含有烈焰粉而不含节制器(cpp:temperancer)且胸甲栏物品含有triggerEffect:[{id:"regeneration"}]时，玩家生命值低于记分板cppMaxHealth值时，给予再生效果，每点生命值消耗1点经验值。
主函数
```
execute as @a[nbt={Inventory:[{id:"minecraft:blaze_powder"},{tag:{triggerEffect:[{}]}}]},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:rituals/effect/check```cpp:rituals/effect/check.mcfunction
```
execute store result score @s cppXpTotal run data get entity @s XpTotal
execute as @s[nbt={Inventory:[{Slot:101b,tag:{triggerEffect:[{id:"regeneration"}]}}],ActiveEffects:[{Id:10b,Duration:10}]}] run function cpp:rituals/effect/regeneration
execute as @s[nbt={Inventory:[{Slot:101b,tag:{triggerEffect:[{id:"regeneration"}]}}]},nbt=!{ActiveEffects:[{Id:10b}]}] run function cpp:rituals/effect/regeneration```cpp:rituals/effect/regeneration
```
scoreboard players set #random_min cppRandom 1
scoreboard players set #random_max cppRandom 10
function cpp:rituals/random
scoreboard players add @s cppMaxHealth 0
scoreboard players set @s[scores={cppMaxHealth=..0}] cppMaxHealth 20
scoreboard players enable @s cppMaxHealth
execute if score @s cppHealth < @s cppMaxHealth run effect give @s minecraft:regeneration 3 0 true
execute if score @s cppHealth < @s cppMaxHealth run xp add @s -1
execute if score @s cppHealth < @s cppMaxHealth run clear @s[scores={cppRandom=1}] blaze_powder 1```
### ### ### ### ## ### ## ### §8.3 方块交互
如果是与某些方块交互，可通过探测相应的交互判据的计分板即可。如果仅需要右击而不打开，可使用传送来实现强制关闭GUI。
**例** 将附魔台、书架、发射器摆放成特定形状，在发射器中放入特定物品，在上方放置一个物品展示框并放入待添加效果的物品。手持魔杖右击发射器，然后等待一段时间将物品附加属性效果。星之魔杖给予更高的属性。

右键时，通过记分板探测到，然后探测玩家手持魔杖类型给予展示框不同标签。判断发射器物品和展示框物品是否符合要求，符合则进入计时，时间到了之后随机给予属性类别、数量、大小，清空发射器，删除标签。
初始化
```
scoreboard objectives add cppInsDisp minecraft.custom:minecraft.inspect_dispenser```主函数
```
###魔杖仪式###
execute at @e[tag=cpp_rituals_back_archor] run tp @a[tag=cpp_rituals_willback] ~ ~ ~
tag @a remove cpp_rituals_willback
execute as @a[scores={cppInsDisp=1..}] run function cpp:rituals/init/check_wand
execute as @e[type=minecraft:item_frame,tag=cpp_rituals_item] at @s run function cpp:rituals/check/type```cpp:rituals/init/check_wand.mcfunction
```
execute as @s[nbt={SelectedItem:{tag:{isWand:1b}}}] at @s positioned ~ ~1.62 ~ run function cpp:rituals/init/ray
scoreboard players reset @s cppInsDisp```cpp:rituals/init/ray.mcfunction
```
execute if entity @s[distance=..9] unless block ~ ~ ~ minecraft:dispenser positioned ^ ^ ^0.005 run function cpp:rituals/init/ray
execute if entity @s[distance=..9] if block ~ ~ ~ minecraft:dispenser if block ~3 ~ ~ minecraft:bookshelf if block ~-3 ~ ~ minecraft:bookshelf if block ~ ~ ~3 minecraft:bookshelf if block ~ ~ ~-3 minecraft:bookshelf if block ~2 ~ ~2 minecraft:enchanting_table if block ~2 ~ ~-2 minecraft:enchanting_table if block ~-2 ~ ~2 minecraft:enchanting_table if block ~-2 ~ ~-2 minecraft:enchanting_table run function cpp:rituals/init/mark```cpp:rituals/init/mark.mcfunction
```
execute align xyz positioned ~0.5 ~1.03125 ~0.5 run tag @e[type=item_frame,distance=..0.1,limit=1] add cpp_rituals_item
execute as @s[nbt={SelectedItem:{tag:{id:"cpp:sakura_wand"}}}] align xyz positioned ~0.5 ~1.03125 ~0.5 run tag @e[type=item_frame,distance=..0.1,limit=1] add cpp_rituals_item_power
execute at @s run summon minecraft:area_effect_cloud ~ ~ ~ {Tags:["cpp_rituals_back_archor"],Duration:2}
tp @s ~ ~256 ~
tag @s add cpp_rituals_willback```cpp:rituals/check/type.mcfunction
```
execute if block ~ ~-1 ~ dispenser{Items:[{Slot:0b,id:"minecraft:gold_ingot",Count:1b},{Slot:2b,id:"minecraft:gold_ingot",Count:1b},{Slot:6b,id:"minecraft:gold_ingot",Count:1b},{Slot:8b,id:"minecraft:gold_ingot",Count:1b},{Slot:1b,id:"minecraft:experience_bottle",Count:64b},{Slot:3b,id:"minecraft:experience_bottle",Count:64b},{Slot:5b,id:"minecraft:experience_bottle",Count:64b},{Slot:7b,id:"minecraft:experience_bottle",Count:64b},{Slot:4b,Count:1b}]} run function cpp:rituals/check/attr

execute at @s[tag=!cpp_rituals_ticks] unless entity @s[scores={cppTicks=1..}] run tellraw @p {"translate":"item.cpp.magicka_wand.fail"}
execute at @s[tag=!cpp_rituals_ticks,scores={cppTicks=1..199}] run tellraw @p {"translate":"item.cpp.magicka_wand.break"}
execute at @s[scores={cppTicks=200..}] run tellraw @p {"translate":"item.cpp.magicka_wand.finish"}

scoreboard players add @s[tag=cpp_rituals_ticks] cppTicks 1
execute at @s[tag=cpp_rituals_ticks] run particle minecraft:enchant ~ ~0.7 ~ 0 0 0 1 10
execute at @s[scores={cppTicks=1}] run tellraw @p {"translate":"item.cpp.magicka_wand.start"}

tag @s[tag=!cpp_rituals_ticks] remove cpp_rituals_item
tag @s[tag=!cpp_rituals_ticks] remove cpp_rituals_item_power

scoreboard players reset @s[tag=!cpp_rituals_ticks] cppTicks
scoreboard players reset @s[scores={cppTicks=201..}] cppTicks
tag @s remove cpp_rituals_ticks```cpp:rituals/check/attr.mcfunction
```
execute if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,tag:{isRareDrops:1b}}]} run tag @s[nbt={Item:{id:"minecraft:diamond_helmet"}}] add cpp_rituals_ticks
execute if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,tag:{isRareDrops:1b}}]} run tag @s[nbt={Item:{id:"minecraft:diamond_chestplate"}}] add cpp_rituals_ticks
execute if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,tag:{isRareDrops:1b}}]} run tag @s[nbt={Item:{id:"minecraft:diamond_leggings"}}] add cpp_rituals_ticks
execute if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,tag:{isRareDrops:1b}}]} run tag @s[nbt={Item:{id:"minecraft:diamond_boots"}}] add cpp_rituals_ticks
execute if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,tag:{isRareDrops:1b}}]} run tag @s[nbt={Item:{id:"minecraft:diamond_sword"}}] add cpp_rituals_ticks

execute if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,id:"minecraft:nether_star"}]} run tag @s[nbt={Item:{id:"minecraft:diamond_helmet"}}] add cpp_rituals_ticks
execute if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,id:"minecraft:nether_star"}]} run tag @s[nbt={Item:{id:"minecraft:diamond_chestplate"}}] add cpp_rituals_ticks
execute if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,id:"minecraft:nether_star"}]} run tag @s[nbt={Item:{id:"minecraft:diamond_leggings"}}] add cpp_rituals_ticks
execute if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,id:"minecraft:nether_star"}]} run tag @s[nbt={Item:{id:"minecraft:diamond_boots"}}] add cpp_rituals_ticks
execute if block ~ ~-1 ~ dispenser{Items:[{Slot:4b,id:"minecraft:nether_star"}]} run tag @s[nbt={Item:{id:"minecraft:diamond_sword"}}] add cpp_rituals_ticks

execute as @s[scores={cppTicks=200..},nbt={Item:{id:"minecraft:diamond_sword"}}] run function cpp:rituals/check/attr_sword
execute as @s[scores={cppTicks=200..},nbt={Item:{id:"minecraft:diamond_helmet"}}] run function cpp:rituals/check/attr_head
execute as @s[scores={cppTicks=200..},nbt={Item:{id:"minecraft:diamond_chestplate"}}] run function cpp:rituals/check/attr_chest
execute as @s[scores={cppTicks=200..},nbt={Item:{id:"minecraft:diamond_leggings"}}] run function cpp:rituals/check/attr_legs
execute as @s[scores={cppTicks=200..},nbt={Item:{id:"minecraft:diamond_boots"}}] run function cpp:rituals/check/attr_feet```cpp:rituals/check/attr_chest.mcfunction
```
scoreboard players set #random_min cppRandom 1
scoreboard players set #random_max cppRandom 200
function cpp:rituals/random
execute as @s[scores={cppRandom=1..28}] run scoreboard players set @s cppAttrType 1
execute as @s[scores={cppRandom=29..56}] run scoreboard players set @s cppAttrType 2
execute as @s[scores={cppRandom=57..84}] run scoreboard players set @s cppAttrType 3
execute as @s[scores={cppRandom=85..112}] run scoreboard players set @s cppAttrType 4
execute as @s[scores={cppRandom=113..140}] run scoreboard players set @s cppAttrType 5
execute as @s[scores={cppRandom=141..168}] run scoreboard players set @s cppAttrType 6
execute as @s[scores={cppRandom=169..175}] run scoreboard players set @s cppAttrType 7
execute as @s[scores={cppRandom=176..182}] run scoreboard players set @s cppAttrType 8
execute as @s[scores={cppRandom=183..189}] run scoreboard players set @s cppAttrType 9
execute as @s[scores={cppRandom=190..196}] run scoreboard players set @s cppAttrType 10
execute as @s[scores={cppRandom=197..200}] run scoreboard players set @s cppAttrType 11

execute as @s[scores={cppAttrType=1}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.maxHealth",Name:"chestplate_MH",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.knockbackResistance",Name:"chestplate_kbR",UUIDLeast:4,UUIDMost:220,Slot:"chest"}]}}}
execute as @s[scores={cppAttrType=2}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.maxHealth",Name:"chestplate_MH",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.movementSpeed",Name:"chestplate_MS",UUIDLeast:4,UUIDMost:220,Slot:"chest"}]}}}
execute as @s[scores={cppAttrType=3}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.maxHealth",Name:"chestplate_MH",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.luck",Name:"chestplate_L",UUIDLeast:4,UUIDMost:220,Slot:"chest"}]}}}
execute as @s[scores={cppAttrType=4}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.knockbackResistance",Name:"chestplate_kbR",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.movementSpeed",Name:"chestplate_MS",UUIDLeast:4,UUIDMost:220,Slot:"chest"}]}}}
execute as @s[scores={cppAttrType=5}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.knockbackResistance",Name:"chestplate_kbR",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.luck",Name:"chestplate_L",UUIDLeast:4,UUIDMost:220,Slot:"chest"}]}}}
execute as @s[scores={cppAttrType=6}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.movementSpeed",Name:"chestplate_MS",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.luck",Name:"chestplate_L",UUIDLeast:4,UUIDMost:220,Slot:"chest"}]}}}

execute as @s[scores={cppAttrType=7}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.maxHealth",Name:"chestplate_MH",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.knockbackResistance",Name:"chestplate_kbR",UUIDLeast:4,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.movementSpeed",Name:"chestplate_MS",UUIDLeast:5,UUIDMost:220,Slot:"chest"}]}}}
execute as @s[scores={cppAttrType=8}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.maxHealth",Name:"chestplate_MH",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.knockbackResistance",Name:"chestplate_kbR",UUIDLeast:4,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.luck",Name:"chestplate_L",UUIDLeast:5,UUIDMost:220,Slot:"chest"}]}}}
execute as @s[scores={cppAttrType=9}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.maxHealth",Name:"chestplate_MH",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.luck",Name:"chestplate_L",UUIDLeast:4,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.movementSpeed",Name:"chestplate_MS",UUIDLeast:5,UUIDMost:220,Slot:"chest"}]}}}
execute as @s[scores={cppAttrType=10}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.luck",Name:"chestplate_L",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.knockbackResistance",Name:"chestplate_kbR",UUIDLeast:4,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.movementSpeed",Name:"chestplate_MS",UUIDLeast:5,UUIDMost:220,Slot:"chest"}]}}}

execute as @s[scores={cppAttrType=11}] run data merge entity @s {Item:{tag:{AttributeModifiers:[{Operation:0,Amount:3,AttributeName:"generic.armor",Name:"chestplate_Ar",UUIDLeast:1,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:2,AttributeName:"generic.armorToughness",Name:"chestplate_ArT",UUIDLeast:2,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.maxHealth",Name:"chestplate_MH",UUIDLeast:3,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.luck",Name:"chestplate_L",UUIDLeast:4,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.knockbackResistance",Name:"chestplate_kbR",UUIDLeast:5,UUIDMost:220,Slot:"chest"},{Operation:0,Amount:0,AttributeName:"generic.movementSpeed",Name:"chestplate_MS",UUIDLeast:6,UUIDMost:220,Slot:"chest"}]}}}

scoreboard players set #random_min cppRandom 8
scoreboard players set #random_max cppRandom 10
function cpp:rituals/random
scoreboard players add @s[tag=cpp_rituals_item_power] cppRandom 1
execute as @s store result entity @s Item.tag.AttributeModifiers[0].Amount double 1 run scoreboard players get @s cppRandom

scoreboard players set #random_min cppRandom 1
scoreboard players set #random_max cppRandom 12
function cpp:rituals/random
scoreboard players add @s[tag=cpp_rituals_item_power] cppRandom 2
execute as @s[scores={cppAttrType=1..3}] store result entity @s Item.tag.AttributeModifiers[2].Amount double 0.5 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=4..5}] store result entity @s Item.tag.AttributeModifiers[2].Amount double 0.04 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=6}] store result entity @s Item.tag.AttributeModifiers[2].Amount double 0.001 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=7..9}] store result entity @s Item.tag.AttributeModifiers[2].Amount double 0.5 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=10}] store result entity @s Item.tag.AttributeModifiers[2].Amount double 0.25 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=11}] store result entity @s Item.tag.AttributeModifiers[2].Amount double 0.5 run scoreboard players get @s cppRandom

scoreboard players set #random_min cppRandom 1
scoreboard players set #random_max cppRandom 12
function cpp:rituals/random
scoreboard players add @s[tag=cpp_rituals_item_power] cppRandom 2
execute as @s[scores={cppAttrType=1}] store result entity @s Item.tag.AttributeModifiers[3].Amount double 0.04 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=2}] store result entity @s Item.tag.AttributeModifiers[3].Amount double 0.001 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=3}] store result entity @s Item.tag.AttributeModifiers[3].Amount double 0.25 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=4}] store result entity @s Item.tag.AttributeModifiers[3].Amount double 0.001 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=5..6}] store result entity @s Item.tag.AttributeModifiers[3].Amount double 0.25 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=7..8}] store result entity @s Item.tag.AttributeModifiers[3].Amount double 0.04 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=9}] store result entity @s Item.tag.AttributeModifiers[3].Amount double 0.25 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=10}] store result entity @s Item.tag.AttributeModifiers[3].Amount double 0.04 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=11}] store result entity @s Item.tag.AttributeModifiers[3].Amount double 0.25 run scoreboard players get @s cppRandom

scoreboard players set #random_min cppRandom 1
scoreboard players set #random_max cppRandom 12
function cpp:rituals/random
scoreboard players add @s[tag=cpp_rituals_item_power] cppRandom 2
execute as @s[scores={cppAttrType=7}] store result entity @s Item.tag.AttributeModifiers[4].Amount double 0.001 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=8}] store result entity @s Item.tag.AttributeModifiers[4].Amount double 0.25 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=9..10}] store result entity @s Item.tag.AttributeModifiers[4].Amount double 0.001 run scoreboard players get @s cppRandom
execute as @s[scores={cppAttrType=11}] store result entity @s Item.tag.AttributeModifiers[4].Amount double 0.04 run scoreboard players get @s cppRandom

scoreboard players set #random_min cppRandom 1
scoreboard players set #random_max cppRandom 12
function cpp:rituals/random
scoreboard players add @s[tag=cpp_rituals_item_power] cppRandom 2
execute as @s[scores={cppAttrType=11}] store result entity @s Item.tag.AttributeModifiers[5].Amount double 0.001 run scoreboard players get @s cppRandom

data remove block ~ ~-1 ~ Items
tag @s remove cpp_rituals_item
tag @s remove cpp_rituals_item_power
tag @s remove cpp_rituals_ticks```如果容器无需打开交互，则可直接为方块物品添加BlockEntityTag:{Lock:"zsx<3wtt"}这种nbt来锁住，可避免采用上述tp玩家至远处来强行关闭GUI。

[page]    
	

## ### ### ### ## ### ## ### §9 机器实例
我们来看一个较为复杂的机器例子。
[img]https://i.loli.net/2018/07/15/5b4ad908501c8.png[/img]

首先将机器背景板、进度条、左侧按钮、右侧经验槽的材质全部画好，这里经验槽采用了动态材质。通过修改模型和display的放缩，一个物品的大小最多可以放大12倍。通过修改z轴高度可调整材质的覆盖次序(感谢@⊙v⊙)。

然后与高仿工作台类似，编写处理方块放置与破坏、背景的清理等内容。之后，检测机器的左侧按键槽位是否为空，若空则切换之。

cpp:all_in_one_machine/option/pressure
```
scoreboard players add @s cppPressure 1
scoreboard players set @s[scores={cppPressure=3..}] cppPressure 0
scoreboard players set @s[tag=!cpp_high_pressure,scores={cppPressure=2}] cppPressure 0
scoreboard players set @s[tag=!cpp_low_pressure,scores={cppPressure=0}] cppPressure 1

execute as @s[scores={cppPressure=0}] run replaceitem block ~ ~ ~ container.2 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"item.cpp.all_in_one_machine\"}"},CustomModelData:12971051}
execute as @s[scores={cppPressure=1}] run replaceitem block ~ ~ ~ container.2 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"item.cpp.all_in_one_machine\"}"},CustomModelData:12971052}
execute as @s[scores={cppPressure=2}] run replaceitem block ~ ~ ~ container.2 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"item.cpp.all_in_one_machine\"}"},CustomModelData:12971053}

execute as @s[scores={cppPressure=0}] run replaceitem block ~ ~ ~ container.1 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"item.cpp.low_pressure\"}",Lore:["{\"translate\":\"lore.cpp.switch\"}"]},CustomModelData:12971000}
execute as @s[scores={cppPressure=1}] run replaceitem block ~ ~ ~ container.1 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"item.cpp.normal_pressure\"}",Lore:["{\"translate\":\"lore.cpp.switch\"}"]},CustomModelData:12971000}
execute as @s[scores={cppPressure=2}] run replaceitem block ~ ~ ~ container.1 firework_star{isMachineBg:1b,display:{Name:"{\"translate\":\"item.cpp.high_pressure\"}",Lore:["{\"translate\":\"lore.cpp.switch\"}"]},CustomModelData:12971000}
```然后探测经验槽是否需要添加经验，若需要则将附魔之瓶转化为经验槽中的经验并切换材质。然后根据当前模式来分类
cpp:all_in_one_machine/type/all
```
execute as @s[scores={cppTemperature=0,cppPressure=0}] run function cpp:all_in_one_machine/type/ll
execute as @s[scores={cppTemperature=0,cppPressure=1}] run function cpp:all_in_one_machine/type/ln
execute as @s[scores={cppTemperature=0,cppPressure=2}] run function cpp:all_in_one_machine/type/lh
execute as @s[scores={cppTemperature=1,cppPressure=0}] run function cpp:all_in_one_machine/type/nl
execute as @s[scores={cppTemperature=1,cppPressure=1}] run function cpp:all_in_one_machine/type/nn
execute as @s[scores={cppTemperature=1,cppPressure=2}] run function cpp:all_in_one_machine/type/nh
execute as @s[scores={cppTemperature=2,cppPressure=0}] run function cpp:all_in_one_machine/type/hl
execute as @s[scores={cppTemperature=2,cppPressure=1}] run function cpp:all_in_one_machine/type/hn
execute as @s[scores={cppTemperature=2,cppPressure=2}] run function cpp:all_in_one_machine/type/hh```然后探测物品是否满足要求，若满足则进行计时。计时完成且经验达标后执行下一步。
cpp:all_in_one_machine/type/ln
```
execute if block ~ ~ ~ barrel{Items:[{Slot:3b,id:"minecraft:lava_bucket"},{Slot:4b,tag:{id:"cpp:cobblestone_plugin"}}]} run scoreboard players set @s cppMacType 1
execute if block ~ ~ ~ barrel{Items:[{Slot:4b,id:"minecraft:lava_bucket"},{Slot:3b,tag:{id:"cpp:cobblestone_plugin"}}]} run scoreboard players set @s cppMacType 1

execute if block ~ ~ ~ barrel{Items:[{Slot:3b,id:"minecraft:lava_bucket"},{Slot:4b,tag:{id:"cpp:stone_plugin"}}]} run scoreboard players set @s cppMacType 2
execute if block ~ ~ ~ barrel{Items:[{Slot:4b,id:"minecraft:lava_bucket"},{Slot:3b,tag:{id:"cpp:stone_plugin"}}]} run scoreboard players set @s cppMacType 2

execute if block ~ ~ ~ barrel{Items:[{Slot:3b,id:"minecraft:lava_bucket"},{Slot:4b,tag:{id:"cpp:obsidian_plugin"}}]} run scoreboard players set @s cppMacType 3
execute if block ~ ~ ~ barrel{Items:[{Slot:4b,id:"minecraft:lava_bucket"},{Slot:3b,tag:{id:"cpp:obsidian_plugin"}}]} run scoreboard players set @s cppMacType 4

scoreboard players add @s[scores={cppMacType=1..2,cppStoredxp=1..}] cppTick 60
scoreboard players add @s[scores={cppMacType=3..4,cppStoredxp=4..}] cppTick 6
execute if entity @s[scores={cppMacType=1..2,cppStoredxp=1..}] if score @s cppTick >= #all_in_one_machine_cd cppValue run function cpp:all_in_one_machine/done
execute if entity @s[scores={cppMacType=3..4,cppStoredxp=4..}] if score @s cppTick >= #all_in_one_machine_cd cppValue run function cpp:all_in_one_machine/done```分类输出朝向 cpp:all_in_one_machine/done
```
execute as @s[scores={cppOutpUTFace=1}] positioned ~1 ~ ~ run function cpp:all_in_one_machine/to_chest
execute as @s[scores={cppOutpUTFace=2}] positioned ~ ~ ~1 run function cpp:all_in_one_machine/to_chest
execute as @s[scores={cppOutpUTFace=3}] positioned ~-1 ~ ~ run function cpp:all_in_one_machine/to_chest
execute as @s[scores={cppOutpUTFace=4}] positioned ~ ~ ~-1 run function cpp:all_in_one_machine/to_chest
execute as @s[scores={cppOutpUTFace=5}] positioned ~ ~-1 ~ run function cpp:all_in_one_machine/to_chest
execute as @s[scores={cppOutpUTFace=6}] positioned ~ ~1 ~ run function cpp:all_in_one_machine/to_chest

execute as @s[scores={cppSlotsDown=26..}] run function cpp:all_in_one_machine/to_self

scoreboard players reset @s cppSlotsDown
scoreboard players reset @s cppTick```若相应位置可输出，则调整其包含的物品槽位，否则输出在机器内 cpp:all_in_one_machine/to_chest
```
execute store result score @s cppSlotsDown run data get block ~ ~ ~ Items
execute unless block ~ ~ ~ #cpp:container run scoreboard players set @s cppSlotsDown 27

execute as @s[scores={cppSlotsDown=0..25,cppTemperature=0,cppPressure=0}] run function cpp:all_in_one_machine/dist/ll
execute as @s[scores={cppSlotsDown=0..25,cppTemperature=0,cppPressure=1}] run function cpp:all_in_one_machine/dist/ln
execute as @s[scores={cppSlotsDown=0..25,cppTemperature=0,cppPressure=2}] run function cpp:all_in_one_machine/dist/lh
execute as @s[scores={cppSlotsDown=0..25,cppTemperature=1,cppPressure=0}] run function cpp:all_in_one_machine/dist/nl
execute as @s[scores={cppSlotsDown=0..25,cppTemperature=1,cppPressure=1}] run function cpp:all_in_one_machine/dist/nn
execute as @s[scores={cppSlotsDown=0..25,cppTemperature=1,cppPressure=2}] run function cpp:all_in_one_machine/dist/nh
execute as @s[scores={cppSlotsDown=0..25,cppTemperature=2,cppPressure=0}] run function cpp:all_in_one_machine/dist/hl
execute as @s[scores={cppSlotsDown=0..25,cppTemperature=2,cppPressure=1}] run function cpp:all_in_one_machine/dist/hn
execute as @s[scores={cppSlotsDown=0..25,cppTemperature=2,cppPressure=2}] run function cpp:all_in_one_machine/dist/hh```最后输出物品到箱子内，并清除输入材料 cpp:all_in_one_machine/dist/ln
```
scoreboard players remove @s[scores={cppMacType=1..2}] cppStoredxp 1
scoreboard players remove @s[scores={cppMacType=3..4}] cppStoredxp 4

execute as @s[scores={cppMacType=1}] run loot insert ~ ~ ~ loot blocks/cobblestone
execute as @s[scores={cppMacType=2}] run loot insert ~ ~ ~ loot cpp:items/stone
execute as @s[scores={cppMacType=3..4}] run loot insert ~ ~ ~ loot blocks/obsidian
execute as @s[scores={cppMacType=3..4}] run loot insert ~ ~ ~ loot cpp:items/bucket

execute at @s store result score #temp cppValue run data get block ~ ~ ~ Items[4].Count
execute at @s as @s[scores={cppMacType=4}] store result block ~ ~ ~ Items[4].Count byte 1 run scoreboard players remove #temp cppValue 1
execute at @s store result score #temp cppValue run data get block ~ ~ ~ Items[3].Count
execute at @s as @s[scores={cppMacType=3}] store result block ~ ~ ~ Items[3].Count byte 1 run scoreboard players remove #temp cppValue 1```

如果你擅长绘制UI的话，可以制作出很精美的UI。例如(https://www.youtube.com/watch?v=bv_wYNs5L6M]该视频]中：
[img]http://attachment.mcbbs.net/forum/201807/10/112312zdtxrrt8tyfhunr8.png[/img]
[img]http://attachment.mcbbs.net/forum/201807/10/112327brktztj6jrj11zrv.png[/img]
均是采用物品材质绘制的。

[page]
## ## ### ### ### ## ### ## ### §10 随机结构
**例** 世界生成时，随机生成羊毛树。

判断玩家东南32*32是否有标记，如无，添加相应标记在32整数倍坐标处，然后生成战利品表、分散，通过战利品表掉落物来生成结构。
也可以使用方块来标记，例如普通生存下y=0使用屏障替换基岩或超平坦生存y=255处使用air替换void_air来实现，这在某些对实体加载有修改的服务端会很有效。
主函数```
execute as @a at @s unless block ~ 0 ~ bedrock run function cpp:generate/check```
}
```cpp:generate/check.mcfunction```
execute positioned ~-64 -2 ~-64 unless entity @e[tag=cpp_chunk,dx=32,dy=256,dz=32] run function cpp:generate/mark
execute positioned ~-32 -2 ~-64 unless entity @e[tag=cpp_chunk,dx=32,dy=256,dz=32] run function cpp:generate/mark
execute positioned ~ -2 ~-64 unless entity @e[tag=cpp_chunk,dx=32,dy=256,dz=32] run function cpp:generate/mark
execute positioned ~-64 -2 ~-32 unless entity @e[tag=cpp_chunk,dx=32,dy=256,dz=32] run function cpp:generate/mark
execute positioned ~-32 -2 ~-32 unless entity @e[tag=cpp_chunk,dx=32,dy=256,dz=32] run function cpp:generate/mark
execute positioned ~ -2 ~-32 unless entity @e[tag=cpp_chunk,dx=32,dy=256,dz=32] run function cpp:generate/mark
execute positioned ~-64 -2 ~ unless entity @e[tag=cpp_chunk,dx=32,dy=256,dz=32] run function cpp:generate/mark
execute positioned ~-32 -2 ~ unless entity @e[tag=cpp_chunk,dx=32,dy=256,dz=32] run function cpp:generate/mark
execute positioned ~ -2 ~ unless entity @e[tag=cpp_chunk,dx=32,dy=256,dz=32] run function cpp:generate/mark```
cpp:generate/mark.mcfunction
```
summon armor_stand ~ -1 ~ {Tags:["cpp_chunk","cpp_undet"],Invulnerable:1b,Invisible:1b,Marker:1b,NoGravity:1b,Small:1b,DisabledSlots:7967}
scoreboard players set #32 cppValue 32
execute store result score #temp cppValue run data get entity @e[tag=cpp_undet,limit=1] Pos[0]
scoreboard players operation #temp cppValue /= #32 cppValue
scoreboard players add #temp cppValue 1
execute store result entity @e[tag=cpp_undet,sort=nearest,limit=1] Pos[0] double 1 run scoreboard players operation #temp cppValue *= #32 cppValue

execute store result score #temp cppValue run data get entity @e[tag=cpp_undet,limit=1] Pos[2]
scoreboard players operation #temp cppValue /= #32 cppValue
scoreboard players add #temp cppValue 1
execute store result entity @e[tag=cpp_undet,sort=nearest,limit=1] Pos[2] double 1 run scoreboard players operation #temp cppValue *= #32 cppValue

loot spawn ~ ~ ~ loot cpp:generate/markers
execute at @e[tag=cpp_undet,sort=nearest,limit=1] run spreadplayers ~16 ~16 0 15 false @e[type=item,nbt={Item:{tag:{isStrMark:1b}}}]
tag @e[tag=cpp_undet] remove cpp_undet
execute as @e[type=item,nbt={Item:{tag:{isStrMark:1b}}}] at @s run function cpp:generate/build
```cpp:generate/build.mcfunction
```
# 爬行者地牢
execute if score #generate_creeper_dungeon cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:creeper_dungeon_marker"}}}] if block ~ 15 ~ cave_air run function cpp:generate/structures/creeper_dungeon
# 附魔室
execute if score #generate_enchanting_room cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:enchanting_room_marker"}}}] run function cpp:generate/structures/enchanting_room
# 图腾柱
execute if score #generate_totem_pillar cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:totem_pillar_marker"}}}] run function cpp:generate/structures/totem_pillar

# 水果树
execute if score #generate_fruit_tree cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:fruit_tree_marker"}}}] if block ~ ~-1 ~ grass_block align xyz run function cpp:plants/trees/fruit
# 矿石树
execute if score #generate_ore_tree cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:ore_tree_marker"}}}] if block ~ ~-1 ~ grass_block align xyz run function cpp:plants/trees/ore
# 羊毛树
execute if score #generate_wool_tree cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:wool_tree_marker"}}}] if block ~ ~-1 ~ grass_block align xyz run function cpp:plants/trees/wool

# 死珊瑚扇
execute if score #generate_dead_coral_fan cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:dead_coral_fan_marker"}}}] run function cpp:generate/structures/dead_coral_fan

# 灌木丛
execute if score #generate_small_bush cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:small_bush_marker"}}}] if block ~ ~-1 ~ grass_block run function cpp:generate/structures/small_bush

# 死云杉树
execute if score #generate_dead_spruce cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:dead_spruce_marker"}}}] unless block ~ ~-1 ~ #cpp:fluid run function cpp:generate/structures/dead_spruce

# 农作物
execute if score #generate_crops cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:crops_marker"}}}] if block ~ ~-1 ~ grass_block run function cpp:generate/structures/crops

# 花草
execute if score #generate_modcrops cppValue matches 1.. as @s[nbt={Item:{tag:{id:"cpp:modcrops_marker"}}}] if block ~ ~-1 ~ grass_block run function cpp:generate/structures/modcrops

kill @s
```生成羊毛树部分略。

[page]
## ## ### ### ### ## ### ## ### §11 种植
**例** 种植铁种子，收获种子和铁锭，可由骨粉催熟。

种下后，探测位置放置盔甲架。破坏时，修改附近掉落物。
cpp:advancements/plants/iron_seeds
```
{
		"parent": "cpp:plants/root",
		"criteria": {
				"iron_seeds": {
						"trigger": "minecraft:placed_block",
						"conditions": {
								"item": {
										"nbt":"{id:\"cpp:iron_seeds\"}"
								}
						}
				}
		},
		"rewards": {
				"function": "cpp:plants/plants/iron_seeds"
		}
}
```cpp:plants/plants/iron_seeds.mcfunction
```
execute at @s positioned ~ ~1.62 ~ run function cpp:plants/plants/iron_seeds_ray
advancement revoke @s only cpp:plants/iron_seeds```cpp:plants/plants/iron_seeds_ray.mcfunction
```
execute if block ~ ~ ~ beetroots align xyz positioned ~0.5 ~0.5 ~0.5 run summon armor_stand ~ ~ ~ {Invulnerable:1b,Invisible:1b,NoGravity:1b,Tags:["cpp_beetroots_plants","cpp_iron_seeds"],Marker:1b}
execute if entity @s[distance=..5] unless block ~ ~ ~ beetroots positioned ^ ^ ^0.005 run function cpp:plants/plants/iron_seeds_ray```主函数
```
execute as @e[type=armor_stand,tag=cpp_beetroots_plants] at @s unless block ~ ~ ~ beetroots run function cpp:plants/break/beetroots```cpp:plants/break/beetroots.mcfunction
```
execute as @s[tag=cpp_iron_seeds] as @e[type=item,nbt={Item:{id:"minecraft:beetroot_seeds"},Age:0s},distance=..1] run data merge entity @s {Item:{tag:{HideFlags:63,Enchantments:[{}],display:{Name:"{\"translate\":\"item.cpp.iron_seeds\"}"},id:"cpp:iron_seeds"}}}
execute as @s[tag=cpp_iron_seeds] as @e[type=item,nbt={Item:{id:"minecraft:beetroot"},Age:0s},distance=..1] run data merge entity @s {Item:{id:"minecraft:iron_ingot"}}
```

实际上，我们也可以通过盔甲架手持物品来实现自定义材质的作物。

[page]
## ## ### ### ### ## ### ## ### §12 连锁挖矿

加载
```

# 使用斧(连锁效果)
scoreboard objectives add cppUseAxe1 minecraft.used:minecraft.diamond_axe
scoreboard objectives add cppUseAxe2 minecraft.used:minecraft.iron_axe
scoreboard objectives add cppUseAxe3 minecraft.used:minecraft.golden_axe
scoreboard objectives add cppUseAxe4 minecraft.used:minecraft.stone_axe
# 使用镐(连锁效果)
scoreboard objectives add cppUsePick1 minecraft.used:minecraft.diamond_pickaxe
scoreboard objectives add cppUsePick2 minecraft.used:minecraft.iron_pickaxe
scoreboard objectives add cppUsePick3 minecraft.used:minecraft.golden_pickaxe
scoreboard objectives add cppUsePick4 minecraft.used:minecraft.stone_pickaxe
# 使用锹(连锁效果)
scoreboard objectives add cppUseShovel1 minecraft.used:minecraft.diamond_shovel
scoreboard objectives add cppUseShovel2 minecraft.used:minecraft.iron_shovel
scoreboard objectives add cppUseShovel3 minecraft.used:minecraft.golden_shovel
scoreboard objectives add cppUseShovel4 minecraft.used:minecraft.stone_shovel```主函数
```
execute as @a[scores={cppChainTick=1..}] at @s positioned ~ ~1.62 ~ run function cpp:chain/type```cpp:chain/type.mcfunction
```
execute positioned ^ ^ ^0.2 run particle entity_effect ~ ~-1 ~ 0.734375 0.37890625 0.3046875 1 0
title @s[scores={cppChainTick=1}] actionbar [{"text":" "}]

scoreboard players remove @s cppChainTick 1

execute as @s[scores={cppUseAxe1=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/axe/init
execute as @s[scores={cppUseAxe2=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/axe/init
execute as @s[scores={cppUseAxe3=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/axe/init
execute as @s[scores={cppUseAxe4=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/axe/init

execute as @s[scores={cppUsePick1=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/pickaxe1/init
execute as @s[scores={cppUsePick2=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/pickaxe2/init
execute as @s[scores={cppUsePick3=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/pickaxe3/init
execute as @s[scores={cppUsePick4=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/pickaxe4/init

execute at @s[scores={cppUseShovel1=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/shovel/init
execute at @s[scores={cppUseShovel2=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/shovel/init
execute at @s[scores={cppUseShovel3=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/shovel/init
execute at @s[scores={cppUseShovel4=1..},nbt=!{Inventory:[{tag:{id:"cpp:temperancer"}}]}] run function cpp:chain/shovel/init

scoreboard players reset @s cppUseAxe1
scoreboard players reset @s cppUseAxe2
scoreboard players reset @s cppUseAxe3
scoreboard players reset @s cppUseAxe4

scoreboard players reset @s cppUsePick1
scoreboard players reset @s cppUsePick2
scoreboard players reset @s cppUsePick3
scoreboard players reset @s cppUsePick4

scoreboard players reset @s cppUseShovel1
scoreboard players reset @s cppUseShovel2
scoreboard players reset @s cppUseShovel3
scoreboard players reset @s cppUseShovel4```cpp:chain/pickaxe1/init```
scoreboard players set #max_durality cppValue 1561
execute store result score #temp cppValue run data get entity @s SelectedItem.tag.Damage
execute if score #temp cppValue < #max_durality cppValue at @e[type=item,nbt={Age:0s},distance=..6,sort=nearest,limit=1] run function cpp:chain/pickaxe1/mark
execute if score #temp cppValue < #max_durality cppValue at @e[type=item,nbt={Age:1s},distance=..6,sort=nearest,limit=1] run function cpp:chain/pickaxe1/mark
scoreboard players reset @s cppUsePick1```cpp:chain/pickaxe1/mark```
execute positioned ~1 ~ ~ if block ~ ~ ~ #cpp:pickaxe1_chain run function cpp:chain/pickaxe1/damage
execute positioned ~-1 ~ ~ if block ~ ~ ~ #cpp:pickaxe1_chain run function cpp:chain/pickaxe1/damage
execute positioned ~ ~1 ~ if block ~ ~ ~ #cpp:pickaxe1_chain run function cpp:chain/pickaxe1/damage
execute positioned ~ ~-1 ~ if block ~ ~ ~ #cpp:pickaxe1_chain run function cpp:chain/pickaxe1/damage
execute positioned ~ ~ ~1 if block ~ ~ ~ #cpp:pickaxe1_chain run function cpp:chain/pickaxe1/damage
execute positioned ~ ~ ~-1 if block ~ ~ ~ #cpp:pickaxe1_chain run function cpp:chain/pickaxe1/damage
```cpp:chain/pickaxe1/damage```
execute as @s[nbt=!{SelectedItem:{tag:{Enchantments:[{id:"minecraft:silk_touch"}]}}}] run function cpp:chain/xp
loot spawn ~ ~ ~ mine ~ ~ ~ mainhand
setblock ~ ~ ~ air
function cpp:chain/damage_check
execute if score #temp cppValue < #max_durality cppValue run function cpp:chain/pickaxe1/mark
```cpp:chain/damage_check```
# 获得1/(耐久度+1)几率的条件
loot spawn ~ ~ ~ loot cpp:random/60
execute store result score #damage_var cppValue run data get entity @e[type=item,nbt={Item:{tag:{isRdMark:1b}}},distance=..1,limit=1] Item.Count
scoreboard players operation #damage_var cppValue *= @s cppChainDam

execute if score #damage_var cppValue matches ..60 run scoreboard players add #temp cppValue 1
execute store result entity @s[gamemode=!creative] SelectedItem.tag.Damage int 1 run scoreboard players get #temp cppValue

kill @e[type=item,nbt={Item:{tag:{isRdMark:1b}}},distance=..1,limit=1]```
其中cpp/loot_tables/random/60.json为```
{
	"pools": [
		{
			"rolls": 1,
			"entries": [
				{
					"type": "item",
					"name": "minecraft:firework_star",
					"functions": [
						{
							"function": "set_count",
							"count": {
								"min": 1,
								"max": 60
							}
						},
						{
							"function": "set_nbt",
							"tag": "{isRdMark:1b,isMachineBg:1b,CustomModelData:12971000}"
						}
					]
				}
			]
		}
	]
}
```


[page]
## §13 磁力效果
核心部分：将物品的Motion修改为玩家的坐标减去物品的坐标即可。
```
execute store result score #playerPos cppPos run data get entity @p[nbt={Inventory:[{tag:{id:"cpp:magnet",Type:1b}}]}] Pos[0] 100
execute store result score #itemPos cppPos run data get entity @s Pos[0] 100
execute store result entity @s Motion[0] double 0.001 run scoreboard players operation #playerPos cppPos -= #itemPos cppPos

execute store result score #playerPos cppPos run data get entity @p[nbt={Inventory:[{tag:{id:"cpp:magnet",Type:1b}}]}] Pos[1] 100
execute store result score #itemPos cppPos run data get entity @s Pos[1] 100
execute store result entity @s Motion[1] double 0.001 run scoreboard players operation #playerPos cppPos -= #itemPos cppPos

execute store result score #playerPos cppPos run data get entity @p[nbt={Inventory:[{tag:{id:"cpp:magnet",Type:1b}}]}] Pos[2] 100
execute store result score #itemPos cppPos run data get entity @s Pos[2] 100
execute store result entity @s Motion[2] double 0.001 run scoreboard players operation #playerPos cppPos -= #itemPos cppPos
```
生物被玩家吸引的效果也可以类似实现。

----
以上内容仅仅是我个人制作过程中的一些感受和经验，具体的应用纷繁复杂，既没有固定的套路，也不可能在短短一篇帖子内尽述。技术不是一成不变的，但这不是重点，因为兴趣和创意才是制作模组的源动力。最后有任何错误和疑问请联系我，谢谢阅读！



