## Spring 的事务传播

1. Required: 如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新的事务。
2. Required_New: 总是创建一个新的事务，如果当前存在事务，则把当前事务挂起。
3. Nested: 如果当前存在事务，则嵌套执行事务；如果当前没有事务，则执行一个单独的事务。
4. Supports: 如果当前存在事务，则加入该事务；如果当前没有事务，则执行 WITHOUT_TRANSACTION。
5. Not_Supported: 如果当前存在事务，则把当前事务挂起；如果当前没有事务，则执行 WITHOUT_TRANSACTION。
6. Never: 总是不执行事务，如果当前存在事务，则抛出异常。
7. Mandatory: 如果当前存在事务，则加入该事务；如果当前没有事务，则抛出异常。

## Spring 中 Bean 的生命周期

### 流程图

[Bean 生命周期](../static/image/Bean的生命周期.png)

### 概述：

1. 实例化 Bean 对象：通过反射实例化 Bean 对象
2. 填充 Bean 的属性：populateBean():通过 setter 方法为 Bean 的属性赋值
3. 初始化 Bean 对象：
   - 前置处理方法：initializeBean():调用 BeanPostProcessor 的 postProcessBeforeInitialization()方法，
   - 后置处理方法：再调用 Bean 的初始化方法，再调用 BeanPostProcessor 的 postProcessAfterInitialization()方法（实现 InitializingBean 接口的 afterPropertiesSet()方法）
4. 获得 Bean 对象：通过 getBean()方法获得 Bean 对象
5. 销毁 Bean 对象：
   - 是否实现 DisposableBean 接口的 destroy()方法
   - 是否在配置文件中定义了销毁方法
