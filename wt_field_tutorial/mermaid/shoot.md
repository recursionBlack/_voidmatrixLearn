```mermaid
graph TD
    root[_physics_process(delta)<br/>读取输入并调度射击分支]

    %% 左侧：普通模式射击流程
    A1[_try_shoot(shoot_input)<br/>普通模式: 检查冷却并准备发射]
    A2[_fire_bullets(base_direction)<br/>决定本轮发射几颗子弹]
    A3[_spawn_bullet(shoot_direction)<br/>实例化子弹并设置出生位置]
    A4[bullet.gd<br/>子弹自行飞行、命中、超时回收]

    %% 中间：强化模式射击流程
    B1[_try_auto_spiral_shoot()<br/>强化模式: 自动生成旋转射击方向]

    %% 右侧：朝向/动画/特效流程
    C1[_update_facing()<br/>更新角色朝向]
    C2[_update_animation()<br/>切换 normal 或 armed 动画]
    C3[_update_armed_effect()<br/>控制强化特效显示]

    %% 连接关系
    root --> A1
    root --> B1
    root --> C1

    A1 --> A2
    B1 --> A2
    A2 --> A3
    A3 --> A4

    C1 --> C2
    C2 --> C3
```

