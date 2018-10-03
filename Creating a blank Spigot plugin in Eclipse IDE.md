# 在 Eclipse IDE 中创建一个空白的Spigot插件
原文来自:[Creating a blank Spigot plugin In Eclipse IDE](https://www.spigotmc.org/wiki/creating-a-blank-spigot-plugin-in-eclipse/)<br>
　　这个教程的目的是教你如何创建你的第一个能被Spigot载入的空白插件。这个教程也会展示你一种可能的从设置工作环境到导出JAR文件的开发工作流程。
### 前置条件
假定你拥有我们将会用到的[Spigot API](https://hub.spigotmc.org/nexus/content/repositories/snapshots/org/spigotmc/spigot-api/)的jar文件

1. 打开 Eclipse:你也许会想要更改工作区的位置。<br>

2. 创建一个新的Java项目
- 给项目起一个你想要使用的名字。在这个教程里，我们使用SpigotBlankPlugin作为项目的名字，然后点击下一步。
- 在**Java设置**中，进入**库**选项卡，选择**添加外部JAR**。在选择JAR的对话框中，选择 Spigot-api-shaded jar 文件，它通常位于你的 BuildTools 文件夹中的 Spigot/Spigot-API/target 目录里，找到之后，点击**完成**。
3. 添加一个新的包<br>
右键点击 **src**，然后点击**新建→包**，只要能保持一致，你可以使用任何你想要使用的命名空间。在这篇教程里，我们使用反向域名命名法(比如:com.google.android)。

4. 创建一个新的类<br>
右键点击新创建的包，然后选择**新建→类**。给它随便起个名字，因为这是一个空白插件，我把它命名和项目一个名字。在编辑器中，新建的Java类会被打开。其中的代码看起来应该是这样的:
```
package com.laffey.tutorialPlugin;
public class SpigotBlankPlugin {
}
```

5.  修改类声明<br>
你的类必须继承自 JavaPlugin ，这样做能让你的类继承 JavaPlugin 类的所有字段与方法，这就是继承的概念。修改类的构造器， Eclipse 就会产生不知道 JavaPlugin 是什么的错误。如果你成功地导入了 Spigot API ，你应该可以在 import 部分中导入 JavaPlugin 类。你无需手动输入那一行，只需简单地点击错误，然后选择合适的快速修正就可以了。你的代码现在看起来应该是这样的:
```
package com.meeku.tutorialPlugin;
import org.bukkit.plugin.java.JavaPlugin;

public class SpigotBlankPlugin extends JavaPlugin {

}
 
```

6. 实现必要的方法<br>
JavaPlugin 类有一些抽象方法必须被你的插件实现。因此，添加 onDisable 和 onEnable 函数能让插件在控制台中被启用或者是停用时触发，你现在可以在这些函数中留空。你也要在方法的上方写上 `@Override`。<br>
注意:你无需在你的插件启用或者停用的时候加上 getLogger， Bukkit 已经为你做好这件事了。
```
package com.meeku.tutorialPlugin;
import org.bukkit.plugin.java.JavaPlugin;

public class SpigotBlankPlugin extends JavaPlugin {
    // Fired when plugin is first enabled
    @Override
    public void onEnable() {
    }
    // Fired when plugin is disabled
    @Override
    public void onDisable() {

    }
}
```

7. 创建plugin.yml文件<br>
右键点击项目，然后使用**新建→文件**建立一个叫做 plugin.yml 的文件，然后在其中粘贴下列内容:
```
name: SpigotBlankPlugin
main: com.meeku.tutorialPlugin.SpigotBlankPlugin
version: 1.0
api-version: 1.13
commands:
```

8. 导出
如果其中没有错误的话，我们就可以把这个项目导出为 jar 了。**右键**点击**项目名**，选择**导出**，在弹出的对话框中，选择 **Java→JAR 文件**，然后点击**下一步**，修改**导出目标**为你的插件目录。
9. 运行
运行 Spigot 服务端，你就能看到插件被启用了。
