# 基于位置的移动
- 修改物体的transform.position
- Transform组件提供了Translate方法，可以让你相对当前位置移动物体。
- vector内置函数
  - MoveTowards
  - SmoothDamp
# 基于物理的移动
- 设置外力的大小 Rigidbody.AddForce()
- 直接修改速度 Rigidbody.Velocity