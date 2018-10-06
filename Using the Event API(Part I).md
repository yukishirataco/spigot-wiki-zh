# 使用事件 API(上)
原文来自[Using the Event API](https://www.spigotmc.org/wiki/using-the-event-api/)

使用 Spigot 的最佳功能是它能够拦截各类事件。这个教程能示范入门监听和拦截事件以及如何创建你自己的监听器。
## 1.创建你的第一个监听器

**1.1 创建一个新的 Spigot 项目**

或者使用已存在的项目

**1.2 创建一个新类**

给这个类起一个你想要的名字，注意这个类将会用于监听事件。

**1.3 准备你的监听器**

监听器必须是` org.bukkit.event.Listener `的接口。你的监听器类现在看起来应该是这样的:
```
import org.bukkit.event.Listener;

public class MyListener implements Listener
{

}
```

**1.4 注册你的监听器**

现在需要注册这个类的实例，以便Spigot能够将事件传递给你的插件。创建监听器的新实例并且注册它的公共区域是你插件的主类中的`onEnable()`方法。
例子:
```
@Override
public void onEnable()
{
    getServer().getPluginManager().registerEvents(new MyListener(), this);
}
```
你现在可以准备向监听器添加事件了。

**1.5 监听事件**

要使你的监听器类能够监听到任何类中给定的事件，必须创建一个添加了`org.bukkit.event.EventHandler`装饰器的方法，并且在该方法的参数中指定了事件的类型。这个方法可以起一个你想要的名字。例子:
```
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.PlayerJoinEvent;

public class MyListener implements Listener
{
     @EventHandler
     public void onPlayerJoin(PlayerJoinEvent event)
     {

     }
}
```

这个方法当玩家加入服务器的时候就会被激活。让我们在全服广播欢迎词:
```
import org.bukkit.Bukkit;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.PlayerJoinEvent;

public class MyListener implements Listener
{
     @EventHandler
     public void onPlayerJoin(PlayerJoinEvent event)
     {
         Bukkit.broadcastMessage("Welcome to the server!");
     }
}
```

**1.6 操作事件**

你可以修改大部分事件发生的时候该做的事并且从事件中获取信息。这些函数存储于你的方法中的事件对象。让我们修改当玩家加入服务器时广播的消息:
```
import org.bukkit.Bukkit;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.PlayerJoinEvent;

public class MyListener implements Listener
{
     @EventHandler
     public void onPlayerJoin(PlayerJoinEvent event)
     {
         event.setJoinMessage("Welcome, " + event.getPlayer().getName() + "!");
     }
}
```

**1.7 我们可以监听什么？**

`org.bukkit.event` 包里有你可以使用的完整的事件列表。参见 [Spigot JavaDoc](https://hub.spigotmc.org/javadocs/spigot/)