python 描述符
===

访问一个属性的优先级顺序

>* 类属性
>* 数据描述符
>* 实例属性
>* 非数据描述符
>* __getattr__方法

**关于数据描述符的定义**

实现了 \__get__  \__set__  \__del__  方法的类属性

**关于非数据描述符的定义**

所有的类数据函数都是非数据描述符

    __get__(self,obj,type=None)
    __set__(self,obj,val)
    __del__(self,obj)
其中 self 是调用它的实例,访问属性的方法。

对于给定的类X和实例x 

X.foo 等价于
    
    type(x).__dict__["foo"].__get__(None,type(x))

x.foo 等价于
    type(x).__dict__["foo"].__get__(x,type(x))
    
**先看类属性**

    >>> class A(object):
    ...     foo=1.2
    ... 
    >>> A.__dict__
    dict_proxy({'__dict__': <attribute '__dict__' of 'A' objects>, '__module__': '__main__', 'foo': 1.2, '__weakref__': <attribute '__weakref__' of 'A' objects>, '__doc__': None})


可以看到在类的dict属性里

**实例属性**

**数据描述符**

    class simpleDescriptor(object):
       def __get__(self,obj,type=None) :
           pass;
       def __set__(self,obj,val):
           pass;
       def __del__(self,obj):
           pass
    class A(object):
        foo=simpleDescriptor();

    >>> a=A();
    >>> print a.foo;
    None
    >>> a.foo=13;
    >>> print a.foo;
    None
    >>> 

原因在于 get 与set 方法都没有实体方法




**note:Python在实在找不到方法的时候，就会求助于\__getattr__方法**















    
    
    
    
    
    
    
    

