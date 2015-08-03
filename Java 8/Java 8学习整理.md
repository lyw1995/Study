#     @Track   24245@163.com   转载请注明来源!
## 1. Interface Default关键字
> 1.使用该修饰关键字,可以在interface中包含带有主体内容的函数

	 interface  Dog
    {
        void eat();

		//default作为修饰符
        default void startEat()
        {
            System.out.print("start eat");
        }
    }