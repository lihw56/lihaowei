#lihw56

**使用construct2制作射击小游戏**
--------------------------

1. 建立一个空白项目，双击空白处插入背景，使背景铺满整个画面，并将其所在图层锁定。

![layer](https://www.scirra.com/images/articles/layersbar.png)

2. 建立一个新的图层，将玩家，怪物，子弹和爆炸置于此图层，并修改名字以便后续操作。

![player](https://www.scirra.com/images/articles/player.png)
![monster](https://www.scirra.com/images/articles/monster.png)
![bullet](https://www.scirra.com/images/articles/Bullet.png)
![explosion](https://www.scirra.com/images/articles/explode.png)

3. 开始给对象添加行为。
- 点击玩家，在左侧的属性栏里的Behaviors添加玩家的行为，如：8 Directions，Scroll To,Bound To Layout,使得玩家可以朝任意方向移动。

![Behaviors](https://www.scirra.com/images/articles/openbehaviors.png)
- 点击子弹，同样在Behaviors里添加行为，需要添加的有Bullet和Destroy Outside Layout,使子弹能够发射出去，并在合适的时候消失。
- 同样的，为了使怪物能在游戏中移动，我们也需要给怪物添加一个bullet行为，并调试好速度。
- 游戏中只有一个怪物当然是不够的，所以我们可以先将怪物复制多次，至于其可持续性，将会在接下来讲到。
- 最后，我们给爆炸对象添加一个Fade Behavior，使爆炸能够逐渐消失，以免阻塞了游戏。
*添加行为就暂时告一段落了*

4. 添加事件。
- 首先，单击顶部的选项卡切换到事件编辑器。
![事件编辑器](https://www.scirra.com/images/articles/eventsheettab.png)
- 接着，我们需要先确定每一个时刻需要发生的事件。
 
  先确定好条件：点击add event，选择system，再选择every tick。

  接着添加事件：点击add action,选择玩家，再选择set angle toward position,分别填入Mouse.X和Mouse.Y，使玩家跟着鼠标转动方向。
  ![结果如图](https://www.scirra.com/images/articles/alwayslookatmouse.png)
- 下一步,我们要让鼠标能够控制子弹的发射。
  确定条件：仍点击add event，选择Mouse，再选择On click,点击确定，建立起单击鼠标左键的条件。

  添加事件：选择对象玩家，再找到Spawn another object，确定另一个对象为子弹，layer 1。

  这就形成了点击鼠标左键发生子弹的效果。

  但是，此时的子弹是从玩家处射出的，而不是从手枪处射出，所以此时我们应回到图层界面，右键单击玩家，选择Edit animations，生成派生对象，并定点在手枪前方。

  ![](https://www.scirra.com/images/articles/placingimagepoint.png)
- 再次回到事件编辑器，这一次，我们要设置子弹的行为。

  仍旧是确定条件：选择子弹->On collision with another object->Monster.

  这一次需要添加的行为比较多：

  怪物->destroy

  子弹->Spawn another object->Explosion,layer 1

  子弹->destroy

  这样子就会实现子弹打到怪物，怪物死亡，子弹爆炸的效果。
- 现在，又出现了新的问题，爆炸效果底色是黑的，不合适，我们该怎么办呢？
  回到图层界面，点击爆炸，在左边的属性栏里找到Effects,
  将Blend mode 从normal改为additive。
- 