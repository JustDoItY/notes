# js原型概念理解

## 一. 创建实例对象的过程

1.  当使用一个函数创建实例对象的时候，函数的prototype属性会指向一个对象，这个对象拥有constructor，constructor就是函数本身，对象的__proto__指向Object.prototype，Object.prototype中包含有一些属性，__proto__为null，原型链到此为止。
2.  实例对象__proto__属性，和函数的prototype属性指向同一个对象，并且__proto__和prototype可以改变指向的对象。实例对象的__proto__和函数的prototype不是等价的。

## 二. 如何寻找变量和函数

1. 如果一个函数或对象获取变量和函数，先找自身拥有的成员变量和函数，如果找不到就会向上找原型对象，__proto__属性，如果找不到，就会在Object.prototype上找，如果再找不到，就会返回undefined。

## 三. 类的使用

1. 类的定义，本质是函数的实现。例如定义一个类A，A中有个constructor函数，constructor内可以定义实例对象成员变量，类中可以定义函数供实例对象调用，可以使用static，为类定义函数。
2. 把类A转为函数来看，constructor就是函数A，类内的非static函数，都会被添加到A.prototype上，static函数都会添加到函数A上，作为A的成员变量。
3. 类可以继承别的类，继承代表的是层级关系。例如类A继承类B，这时A.prototype就会指向B.prototype。当实例对象在类A中找不到函数的时候，就会在类B中寻找。
4. super只能在继承的类中使用。例如类A继承类B。（1）当类B有constructor时，在类A的constructor中需要调用super()，代表执行类B的构造函数，必须在类B的构造函数执行完之后，类A的构造函数才能被执行。（2）如果需要在类A函数中执行类B中的函数，可以在类A的函数内调用super.funcition()，执行类B中的函数。
5. 当使用类创建实例对象时，在构造函数内定义的变量，都会被添加到实例对象，作为实例对象的成员变量。其类内的非static函数都会在原型链上，实例对象可以直接调用。
