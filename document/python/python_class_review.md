# **python 中 Class 使用**

## 1、类的定义和创建

​		python 中使用关键字class对类进行定义，一般class name首字母要大写，新式类定义的时候需要继承一个object类，也可以不继承，但是为了防止出现意外的情况，一般都默认填写继承

## 2、类中的实例属性和类属性

​		实例属性通常使用__init__()在创建对象的时候进行实例化。__init__()不是对实例进行创建，创建实例的是__new__()

​		类属性通常是实例的共有属性，一般通过类的调用对类的属性进行修改，实例也可以修改类的属性，但是只是修改的副本。

## 3、方法

​		实例方法就是绑定在实例上的方法（通过关键字self进行绑定），实例可以调用类方法

​		类方法就是绑定在类上的方法，类不可以调用实例方法

​		静态方法 可以通过实例和类进行调用，类和实例都能调用静态方法

```python
class TemplateClass(object):
    class_vars = [1, 2, 3]

    def __init__(self, obj_var):
        self.obj_var = obj_var

    def object_method(self):
        print(self.obj_var)
        print(self.class_vars)
        return "object" + self.obj_var

    @classmethod
    def class_method(cls):
        cls.class_vars = [0]
        print("this is class method")
        print("class_var" + str(cls.class_vars))

    @staticmethod
    def static_method():
        '''static_method 可以当做一般的方法'''
        print("this is staticmethod")

    def obj_modify_class_var(self):
        '''object 可以修改类变量，但是修改的是自身的类变量'''
        self.class_vars = ['temp']
 if __name__=="__main__":
    temp = TemplateClass('my_object_vars')
    TemplateClass.class_method()#类调用类方法
    temp.object_method()#实例调用实例方法
    temp.obj_modify_class_var()#实例可以修改类变量，但是修改的是副本
    temp.static_method()#实例可以调用静态方法
    TemplateClass.static_method()#类也可以调用静态方法
    temp.class_method()#实例可以调用类方法。
    
```

## 4、继承

​	单继承：子类继承父类所有功能，父类的初始化使用super().__init__()进行初始化

​	多继承：如果多继承出现相同方法，首先调用首先继承的父类方法，父类的初始化一般使用baseClass(selft).__init__()

​	多重继承是个坑，尽量避免MRO，代码要合理化，好好设计一下

```python
class Father(object):
    father_class_var = "father"

    def __init__(self, father_var):
        self.father_var = father_var

    def modify_object_var(self):
        self.father_var = "modify father"
        print("modify object var father")

    @staticmethod
    def father_static_method():
        print("this is father static meth od")

    @classmethod
    def father_class_method(cls):
        print("this is father class method")

    def father_object_method(self):
        print("this is father object method")


class Mother(object):
    mother_class_var = "mother"

    def __init__(self, mother_var):
        self.mother_var = mother_var

    def modify_object_var(self):
        self.mother_var = "modify mother"
        print("modify object var mother")


class Son(Father, Mother):
    son_class_var = "son"

    def __init__(self, father_var, mother_var, son_var):
        # super().__init__(father_var=father_var, mother_var=mother_var)
        Father.__init__(self, father_var=father_var)
        Mother.__init__(self, mother_var=mother_var)
        self.son_var = son_var

    def modify_object_var(self):
        self.son_var = "modify by father object"
        self.father_var = "modify by son object"
        print("modify object var son")

    @staticmethod
    def father_static_method():
        print("this is happened in son class and call by son object")


if __name__ == '__main__':
    father = Father("father init")
    son = Son("son father init", "son mather init", "son son init")
    son.modify_object_var()
```

