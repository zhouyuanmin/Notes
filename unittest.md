# unittest

- 面向对象
- 测试用例的组成：用例编号、模块、***测试标题***、前提条件、***操作步骤***、***期望结果***、世纪结果

### 概念

- 测试脚手架 test fixture
- 测试用例 TestCase 基类
- 测试套件 test suite
- 测试运行器 test runner

### 使用

```python
setUp和tearDown 设置初始化和状态还原
unittest.main() # 开始执行测试
self.assertEqual # assertTrue、assertFalse
# assertRaises(), assertRaisesRegex(), assertWarns(), assertWarnsRegex()
with self.assertRaises(TypeError):
    pass
# 命令 python -m unittest ...
```

 *常见判断方法：*

 <img src="https://gitee.com/zhouyuanmin/images/raw/master/imgs/20201027100723.png" alt="image-20201027100723831" style="zoom: 33%;" />

 <img src="https://gitee.com/zhouyuanmin/images/raw/master/imgs/20201027101027.png" alt="image-20201027101027126" style="zoom: 33%;" />

```
# 测试套件 test suite
def suite():
    suite = unittest.TestSuite()
    suite.addTest(WidgetTestCase('test_default_widget_size'))  # 这是一个测试方法名
    suite.addTest(WidgetTestCase('test_widget_resize')) # 这是一个测试方法名
    return suite

if __name__ == '__main__':
    runner = unittest.TextTestRunner()
    runner.run(suite())
```



### 跳过测试与预计的失败

```
# 跳过测试
@unittest.skip
@unittest.skipIf
@unittest.skipUnless
# 预计失败
@unittest.expectedFailure
```

