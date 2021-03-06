理解python中的元类
======
[note:参考这里](http://blog.jobbole.com/21351/)

**类也是对象**

一般而言类是描述如何生成对象的代码断。但是python中的类还远不止此,只有使用new关键字。python就生成了对象

    >>> class ObjectCreator(object):
    …       pass
    …

则此时在内存中创建了一个对象.这个对象的名称为ObjectCreator。也就是说它拥有对象的特征。

1. 可以将它赋值给变量
2. 可以拷贝它
3. 可以增加属性
4. 可以作为参数传递

**动态地创建类**

这里注意因为类是对象,所以可以在运行的时候动态的创建

    >>> def choose_class(name):
    …       if name == 'foo':
    …           class Foo(object):
    …               pass
    …           return Foo     # 返回的是类，不是类的实例
    …       else:
    …           class Bar(object):
    …               pass
    …           return Bar
    …

type 在动态生成对象的使用。可以接受一个类的描述返回一个类。使用格式为 

type(类名, 父类的元组（针对继承的情况，可以为空），包含属性的字典（名称和值）)

    >>> MyShinyClass = type('MyShinyClass', (), {})  # 返回一个类对象
    >>> print MyShinyClass
    <class '__main__.MyShinyClass'>
    >>> print MyShinyClass()  #  创建一个该类的实例
    <__main__.MyShinyClass object at 0x8997cec>
    
这里需要重点知道动态的为类增加方法

    >>> def echo_bar(self):
    …       print self.bar
    …
    >>> FooChild = type('FooChild', (Foo,), {'echo_bar': echo_bar})
    >>> hasattr(Foo, 'echo_bar')
    False
    >>> hasattr(FooChild, 'echo_bar')
    True
    >>> my_foo = FooChild()
    >>> my_foo.echo_bar()
    True

从上面可以看出可以动态的创建类.当然上面其实是new关键字幕后所作的事情

***什么是元类***

元类是用来创建类的东西。元类就是类的类

注意 所有东西（整型，字符串、函数、类）都是对象

    >>> age = 35
    >>> age.__class__
    <type 'int'>
    >>> name = 'bob'
    >>> name.__class__
    <type 'str'>
    >>> def foo(): pass
    >>>foo.__class__
    <type 'function'>
    >>> class Bar(object): pass
    >>> b = Bar()
    >>> b.__class__
    <class '__main__.Bar'>

当然这里有一个很有意思的问题__class__的__class__是什么呢？

    >>> a.__class__.__class__
    <type 'type'>
    >>> age.__class__.__class__
    <type 'type'>
    >>> foo.__class__.__class__
    <type 'type'>
    >>> b.__class__.__class__
    <type 'type'>

所以元类就是用来创建类这种东西的类了

    class Foo(Bar):
        pass

python分析的步骤为

1. Foo中有__metaclass__这个属性吗？如果是，Python会在内存中通过__metaclass__创建一个名字为Foo的类对象（我说的是类对象，请紧跟我的思路）。如果Python没有找到__metaclass__，它会继续在Bar（父类）中寻找__metaclass__属性，并尝试做和前面同样的操作。如果Python在任何父类中都找不到__metaclass__，它就会在模块层次中去寻找__metaclass__，并尝试做同样的操作。
2. 如果还是找不到__metaclass__,Python就会用内置的type来创建这个类对象。

***自定义元类***

     元类会自动将你通常传给‘type’的参数作为自己的参数传入
    def upper_attr(future_class_name, future_class_parents, future_class_attr):
        '''返回一个类对象，将属性都转为大写形式'''
        #  选择所有不以'__'开头的属性
        attrs = ((name, value) for name, value in future_class_attr.items() if not name.startswith('__'))
     # 将它们转为大写形式
        uppercase_attr = dict((name.upper(), value) for name, value in attrs)
     
        # 通过'type'来做类对象的创建
        return type(future_class_name, future_class_parents, uppercase_attr)
     
    __metaclass__ = upper_attr  #  这会作用到这个模块中的所有类
     
    class Foo(object):
        # 我们也可以只在这里定义__metaclass__，这样就只会作用于这个类中
        bar = 'bip'

上面很重要的一点是_作用范围_



***结语***

python中一切都是实例。要么是类的实例。要么是元类的实例.当然除了type。当然一般修改类还是使用以下两种方法

>* Monkey patching
>* class decorators



ps [参考这里](http://stackoverflow.com/questions/100003/what-is-a-metaclass-in-python)








