



# JS 设计模式


# JS中面向对象编程的演变进程

# 面向对象编程

## 函数式编程

    function sayA() {
        console.log('A');
    }

    function sayB() {
        console.log('B');
    }


## 用对象收编函数



- 将函数作为对象的属性，从而将多个函数收归到一处，减少了变量的声明， 同时也方便了对于代码的管理。



        var checkObject = {
            checkName: function() {},
            checkAge: function() {},
        }

        等价于

        var checkObject = function () {}
        checkObject.checkName = function() {}
        checkObject.checkAge = function () {}



- 构造一个函数， 返回该具有多个属性为函数的复杂的对象



        var CheckObject = function () {
            return {
                checkName: function() {
                    console.log('name');
                },
                checkAge: function() {
                    console.log('age');
                },
            }
        } 

        var a = CheckObject();
        a.checkName();  //  age 



    这种直接在一个函数中返回一个对象的方式，  并不是真正意义上的类的创建方式， 创建出来的对象 a 与 CheckObject 这个名义上的构造函数没有任何的关系。




    改造下，变成另一种方式如下： 

        var CheckObject = function () {
            this.checkName = function() {
                console.log('name');
            };
            this.checkAge = function() {
                console.log('age');
            };
        } 

        var a = new CheckObject();
        a.checkName();  //  age 


    这种创建对象的方式， 可以认为是真正意义上的对象的创建方式，通过new 关键字类创建对象， 并拥有属于自己的属性。


    然而，这中创建对象的方式还是有一些缺陷， 缺陷在于， 当我们使用该构造方法来创建对象的时候，每一个通过this添加的变量都会拷贝一份到当前的新生成的对象中。这么做对于内存大的消耗是很奢侈的，不推荐这样做。


    由于js的继承是基于原型链的，此时可考虑通过原型来解决创建对象时的属性复制造成的内存的巨大消耗问题。解决的方式如下： 

        var checkObject = function() {}

        checkObject.prototype.checkName = function() {
            console.log('name');
        };

        checkObject.prototype.checkAge = function() {
            console.log('age');
        };

        var a = new CheckObject();
        a.checkAge();  //  age
        a.checkName();  //  name


        






