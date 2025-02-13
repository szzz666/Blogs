# Minecraft基岩版命令方块防飞行

## 记分板创建
首先，手动创建一个记分板：

```minecraft
/scoreboard objectives add 飞行 dummy 飞行
```

## 命令方块设置
以下所有命令方块均为无条件始终活动的循环命令方块。

### 防飞行核心
执行延迟：0

```minecraft
execute as @a[tag=!有鞘翅] at @s run execute if block ~ ~ ~ air run execute if block ~ ~-1 ~ air run execute if block ~ ~-3 ~ air run execute if block ~-1 ~-1 ~-1 air run execute if block ~1 ~-1 ~1 air run execute if block ~1 ~-1 ~ air run execute if block ~ ~-1 ~1 air run execute if block ~-1 ~-1 ~ air run execute if block ~ ~-1 ~-1 air run execute if block ~-1 ~-1 ~1 air run execute if block ~1 ~-1 ~-1 air run execute if block ~ ~1 ~ air run execute if block ~-1 ~1 ~-1 air run execute if block ~1 ~1 ~1 air run execute if block ~1 ~1 ~ air run execute if block ~ ~1 ~1 air run execute if block ~-1 ~1 ~ air run execute if block ~ ~1 ~-1 air run execute if block ~-1 ~1 ~1 air run execute if block ~1 ~1 ~-1 air run execute if block ~-1 ~ ~-1 air run execute if block ~1 ~ ~1 air run execute if block ~1 ~ ~ air run execute if block ~ ~ ~1 air run execute if block ~-1 ~ ~ air run execute if block ~ ~ ~-1 air run execute if block ~-1 ~ ~1 air run execute if block ~1 ~ ~-1 air run execute if block ~-1 ~2 ~-1 air run execute if block ~1 ~2 ~1 air run execute if block ~1 ~2 ~ air run execute if block ~ ~2 ~1 air run execute if block ~-1 ~2 ~ air run execute if block ~ ~2 ~-1 air run execute if block ~-1 ~2 ~1 air run execute if block ~1 ~2 ~-1 air run execute if block ~ ~2 ~ air run scoreboard players add @s 飞行 1
```

### 鞘翅检测
执行延迟：0

```minecraft
tag @a[hasitem={item=elytra,location=slot.armor.chest}] add 有鞘翅
```

### 鞘翅检测重置
执行延迟：4

```minecraft
tag @a remove 有鞘翅
```

### 在地面的时候归零
执行延迟：0

```minecraft
execute as @a at @s unless block ~ ~-1 ~ air run scoreboard players set @s 飞行 0
```

### 排除烟花推进
执行延迟：0

```minecraft
execute as @e[type=fireworks_rocket] at @s run scoreboard players set @p[r=10] 飞行 0
```

### 排除潜影贝导弹造成的漂浮
执行延迟：0

```minecraft
execute as @e[type=minecraft:shulker_bullet] at @s run scoreboard players set @p[r=2] 飞行 -200
```

### 达到阈值重置飞行
执行延迟：0

```minecraft
scoreboard players set @a[scores={飞行=250}] 飞行 0
```

### 自动清除缓降效果
执行延迟：0

```minecraft
effect @a[scores={飞行=50}] slow_falling 0 0 true
```

### 对疑似飞行者执行警告一
执行延迟：0

```minecraft
/title @a[scores={飞行=80}] actionbar §c检测到您可能违法飞行，请马上降落在方块表面~
```

### 警告二
执行延迟：0

```minecraft
/title @a[scores={飞行=120}] actionbar §4请立马回到方块表面，否则进行封禁~
```

### 进行封禁
执行延迟：0

```minecraft
tag @a[scores={飞行=240}] add 封禁
```