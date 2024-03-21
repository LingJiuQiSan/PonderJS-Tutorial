# 开始

## 开始之前

在开始之前，请确保你已经安装位于 [介绍的必要的准备的东西](./README.md#必要的准备)

所有属于 PonderJS 的脚本都应该位于 `client_scripts` 文件夹内。如果你不知道该文件在哪，请查阅 [KubeJS wiki](https://kubejs.com/wiki/tutorials/getting-started)

## 创建场景

### 事件

使用 `Ponder.registry` 事件来创建场景。

```javascript
// 对于 KubeJS5 ，请使用  onEvent("ponder.registry", event => { ... })
Ponder.registry((event) => {
    /**
    * 为 "minecraft:apple" 用场景来创建一个新的思考条目。
    */
    event.create("minecraft:apple")
        .scene(
            "scene_id", // id, 请只使用小写英文字母、数字和下划线
            "场景名称", //会显示在游戏中思索的左上角
            (scene, util) => {
                // 你的场景代码
            }
        )
})
```

对于没有指定自定义结构的代码， PonderJS 将自动使用基本的 5x5 结构。

你可以使用自定义结构，方法是将自定义结构的 `*.nbt` 文件放在 `kubejs/assets/kubejs/ponder` 文件夹内并更改代码为：

```javascript
// 对于 KubeJS5 ，请使用  onEvent("ponder.registry", event => { ... })
Ponder.registry((event) => {
    /**
    * 为 "minecraft:apple" 用场景来创建一个新的思考条目。
    */
    event.create("minecraft:apple")
        .scene(
            "scene_id", // id, 请只使用小写英文字母、数字和下划线
            "场景名称", //会显示在游戏中思索的左上角
            "kubejs:structure_id", // 对应 kubejs/assets/kubejs/ponder/structure_id.nbt
            (scene, util) => {
                // 你的场景代码
            }
        )
})
```

### 注意

1、可以为一个物品创建多个场景，只需要另外进行一次 `event.create("id")` 即可，但是 `scene_id` 不应相同。

2、nbt文件可以使用机械动力的 [蓝图与笔](https://www.mcmod.cn/item/347848.html) 或原版的 [结构方块](https://www.mcmod.cn/item/35469.html) 生成。

## 显示初始结构

```javascript
scene.showStructure(n)
```

以上这段代码将显示读取的nbt中y值为 0 至 n 的部分。你也可以不传入参数，这将会获取地板的大小并乘二作为n传入以上函数（相关代码段： https://github.com/AlmostReliable/ponderjs/blob/36486f72234540b2ac54ca266e2698471bbad97b/src/main/java/com/almostreliable/ponderjs/api/ExtendedSceneBuilder.java#L77 ）。

当你使用机械动力自带的地板时，你可以使用 `scene.showBasePlate()` 来显示地板。该方法的效果等效于 `scene.showStructure(0)` 。

## 放置、替换和修改方块

### 开始之前

你可以打开机械动力的思索的编辑模式来查看/推断所放置、替换和修改方块的位置。打开方法请见 [官方文档](https://github.com/AlmostReliable/ponderjs/wiki/6.-Coordinates) 。

### 放置方块

```javascript
scene.world.setBlock([1, 1, 1], "minecraft:stone", false);
scene.world.setBlocks([1, 1, 1, 2, 2, 2], "minecraft:cobblestone", true);
```

此处第一个参数为方块位置/区域 具体写法请参阅 [类型语法](./Type_Syntax.md) ；第二个参数为所放置的方块id；第三个参数为是否生成方块粒子（false为不生成，true为生成）。

### 替换方块

```javascript
scene.world.replaceBlocks([3, 1, 0, 4, 1, 4], "minecraft:cobblestone", true);
```

替换方块与放置方块最大的区别为不会替换空气方块，而放置方块会在空气处也放置。

### 修改方块

`// TODO` 