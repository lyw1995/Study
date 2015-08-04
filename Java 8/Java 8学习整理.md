#     @Track   24245@163.com   转载请注明来源!
## 1. Interface Default关键字
> 1.使用该修饰关键字,可以在interface中包含带有主体内容的函数
>> 
```java
 interface  Dog
    {
        void eat();
        //default 关键字
        default void startEat()
        {
            System.out.print("nima");
        }
    }
```

## 2. Functional Interfaces 的概念。
>> Functional Interfaces 是一个只有单个方法的接口，这代表了这个方法契约。


http://winterbe.com/posts/2014/03/16/java-8-tutorial/
http://openjdk.java.net/projects/lambda/
http://cr.openjdk.java.net/~briangoetz/lambda/sotc3.html
http://ifeve.com/java-8-lambdas-part-1/
http://ifeve.com/category/concurrency-translation/
https://github.com/ReactiveX/RxJava
http://blog.csdn.net/vector_yi/article/details/24719873
http://www.java3z.com/cwbwebhome/article/article20/200102.html?id=4969
http://www.oschina.net/question/82993_74395
http://www.iteye.com/topic/1127931
http://www.java3z.com/cwbwebhome/article/article20/200102.html?id=4969
http://www.cnblogs.com/figure9/archive/2014/10/24/4048421.html
http://blog.csdn.net/renfufei/article/details/24600507
http://www.importnew.com/11908.html
http://ifeve.com/stream/
http://www.javacodegeeks.com/2013/06/java-8-lambda-walkthrough.html
http://ifeve.com/java-7%E4%B8%AD%E7%9A%84try-with-resources/
http://ifeve.com/processing-data-with-java-se-8-streamspart-1/
http://ifeve.com/20-examples-of-date-and-time-api-from-java8/
http://www.importnew.com/6675.html

