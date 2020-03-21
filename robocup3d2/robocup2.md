# 球队开发入门指南2

---

## 前置条件

1. 对C++有一定了解。
2. 平台和球队Demo已经可以运行。

---

## 基础概念讲解

该部分将对平台上的基础概念和模拟过程进行讲解。

RoboCup 3D足球模拟采用C/S架构模式。模拟平台作为服务器(Server)，球员作为客户端(Client)，客户端通过TCP连接到服务器上，双方在每个模拟周期中(目前被设置为0.02S)相互发送消息来进行通讯。双方使用S-Expression作为底层通讯数据的格式。客户端也被称作智能体(Agent)

服务器端负责进行物理效果的模拟，足球规则的应用。服务器会把场上的各种物理信息以及机器人自身的状态发送给客户端。客户端收到这些消息，对这些消息进行处理，进行决策，这些信息的处理与决策就是我们要编程的部分。通过我们编写程序，客户端对场上的各种变化做出反应，这些“反应“会以一定的形式发送给服务器。服务器根据每个机器人的反应来进行物理演算，计算出下一个模拟周期的物理状态，再次讲这些状态发送给球员，以此往复。

在一支队伍中每个球员都会有一个球员编号`unique number`(简写为`unum`)，范围为1-11。也就是说，一支队伍会有十一名球员。

球场的大小如图所示：

![avator](1.png)

这一部分内容更多请参考群内`官方相关文档`文件夹下文档。也可参考群公告中的simspark项目wiki页面。入门开发并不过多考虑这些底层内容。

## 找到Demo的实现

在`behaviors/strategy.cc`，你会看到:

```cpp
SkillType NaoBehavior::demoKickingCircle() {
    // Parameters for circle
    VecPosition center = VecPosition(-HALF_FIELD_X/2.0, 0, 0);
    double circleRadius = 5.0;
    double rotateRate = 2.5;

    // Find closest player to ball
    int playerClosestToBall = -1;
    double closestDistanceToBall = 10000;
    for(int i = WO_TEAMMATE1; i < WO_TEAMMATE1+NUM_AGENTS; ++i) {
        VecPosition temp;
        int playerNum = i - WO_TEAMMATE1 + 1;
        if (worldModel->getUNum() == playerNum) {
            // This is us
            temp = worldModel->getMyPosition();
        } else {
            WorldObject* teammate = worldModel->getWorldObject( i );
            if (teammate->validPosition) {
                temp = teammate->pos;
            } else {
                continue;
            }
        }
        temp.setZ(0);

        double distanceToBall = temp.getDistanceTo(ball);
        if (distanceToBall < closestDistanceToBall) {
            playerClosestToBall = playerNum;
            closestDistanceToBall = distanceToBall;
        }
    }

    if (playerClosestToBall == worldModel->getUNum()) {
        // Have closest player kick the ball toward the center
        return kickBall(KICK_FORWARD, center);
    } else {
        // Move to circle position around center and face the center
        VecPosition localCenter = worldModel->g2l(center);
        SIM::AngDeg localCenterAngle = atan2Deg(localCenter.getY(), localCenter.getX());

        // Our desired target position on the circle
        // Compute target based on uniform number, rotate rate, and time
        VecPosition target = center + VecPosition(circleRadius,0,0).rotateAboutZ(360.0/(NUM_AGENTS-1)*(worldModel->getUNum()-(worldModel->getUNum() > playerClosestToBall ? 1 : 0)) + worldModel->getTime()*rotateRate);

        // Adjust target to not be too close to teammates or the ball
        target = collisionAvoidance(true /*teammate*/, false/*opponent*/, true/*ball*/, 1/*proximity thresh*/, .5/*collision thresh*/, target, true/*keepDistance*/);

        if (me.getDistanceTo(target) < .25 && abs(localCenterAngle) <= 10) {
            // Close enough to desired position and orientation so just stand
            return SKILL_STAND;
        } else if (me.getDistanceTo(target) < .5) {
            // Close to desired position so start turning to face center
            return goToTargetRelative(worldModel->g2l(target), localCenterAngle);
        } else {
            // Move toward target location
            return goToTarget(target);
        }
    }

```

这里就是我们所运行出来的demo的实现部分。大家可以自己看一下大致的逻辑，本篇文章不会讲解该Demo。

## 编写简单的Demo

**注意**，以下做法并非`Best Practice`。较为正确的做法是建立新的继承自`NaoBehavior`的类，并重写相关虚函数，并在`main.cc`中添加命令行参数相关接口。本着简单原则，本篇采用较为简单的方式。

首先在`behaviors/naobehavior.h`的`NaoBehavior`里面加入成员函数的声明，找到这一行：

```cpp
SkillType demoKickingCircle();
```

在下面添加一行，就变成了

```cpp
SkillType demoKickingCircle();
SkillType demoKicking();
```

找到`behaviors/naobehavor.cc`，加入`demoKicking()`的定义。

```cpp
SkillType NaoBehavior::demoKicking()
{
    if(worldmodel->getPlayMode() != PM_PLAYON)
    {

    }
}






