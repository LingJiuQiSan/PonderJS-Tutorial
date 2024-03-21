# 类型语法

在 PonderJS 中，一些函数需要区域、方块位置或向量。区域是两个位置或向量之间的区域。

KubeJS 和 PonderJS 提供了一种简单的语法来将位置或向量传递给函数。

将具有三个值 的数组 `[x, y, z]` 传递给需要区域、方块位置或向量的函数会自动将数组包装为相应的类型。

如果您想简写选择区域，您可以传入以下类型：

* `[x1, y1, z1, x2, y2, z2]` 

* `[[x1, y1, z1], [x2, y2, z2]]` 

* `[vector1, vector2]` 

* `[blockPos1, blockPos2]` 

如果您不喜欢简写语法，你可以在你的思索场景中使用 `util` 提供的函数，关于util提供的函数，请参阅 `// TODO` 。不过在此处util教程施工完成前，你可以查阅 [官方文档](https://github.com/AlmostReliable/ponderjs/wiki/5.-Utils) 。