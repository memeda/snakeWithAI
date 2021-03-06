# SNAKE Game 贪吃蛇游戏

The game rewrited based on https://gist.github.com/sanchitgangwar/2158089 . 

We split the 
drawing logic and game inner state, so that it can be easily migrated to any other UI system. 
What's more, it the first step to make a snake-ai -> in trainning, we just need the game state, while
the UI became a burden.

what's more, we abstract the controller strategy from Game executor, so that we can impl the manual, rule-based,
and RL based strategy.

基于 https://gist.github.com/sanchitgangwar/2158089 写成，主要改动是把游戏状态和绘制逻辑拆开了，这样可以

（1）解耦状态和绘制，以后可以迁移到多种平台上（……）
（2）无需绘制即可“运行”游戏，利于未来AI训练

此外，我们抽象出了 `strategy.Strategy` 类，从而可以方便地添加手工、基于规则、基于强化学习的策略来控制贪吃蛇游戏。

# 贪吃蛇游戏的奥秘

没看人家的代码前，我曾经想贪吃蛇得多复杂啊。看完代码才恍然大悟：

1. 身体存储起来就是一个坐标的序列，另外再存储一个方向
2. 每个时钟，贪吃蛇移动；移动逻辑非常简单：根据当前的头部位置坐标，以及方向，生成新的头部坐标，插入到身体序列里，并移除尾部的坐标，这样
贪吃蛇就往前移动了！
3. 吃果子检测及更新：前面生成头部坐标后，直接对比果子坐标，如果一样就吃到果子了！玩游戏时我们知道吃到果子时身体是变长了1——但其实内部状态更新，
就是头部照样插入到身体序列，但是尾部的坐标不用删除了！
4. 撞墙检测，同样基于头部坐标和墙坐标的对比

很有意思~

## Game Screenshot

![screenshot](../resource/snake_game_running.png)

## Run

```
python3 run.py
```
