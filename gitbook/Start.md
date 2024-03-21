# 开始

## 开始之前

在开始之前，请确保你已经安装位于 [介绍的必要的准备的东西](https://lingjiuqisan.gitbook.io/ponder-for-kubejs-tutorial#bi-yao-de-zhun-bei) 

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

注意：可以为一个物品创建多个场景，只需要另外进行一次 `event.create("id")` 即可，但是 `scene_id` 不应相同。