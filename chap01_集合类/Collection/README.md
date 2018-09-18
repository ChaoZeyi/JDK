java.util.Collection是一组元素的集合，提供了集合通用的方法，之后会讲到的list, set等接口继承的也都是Collection接口。

```java
package java.util;

public interface Collection<E> extends Iterable<E>{
      /**
       * Returns the number of elements in this collection.  If this collection
       * contains more than <tt>Integer.MAX_VALUE</tt> elements, returns
       * <tt>Integer.MAX_VALUE</tt>.
       *
       * @return the number of elements in this collection
       * 返回集合中元素的个数，也就是常说的集合大小     
       */
       int size();

       /**
        * Returns <tt>true</tt> if this collection contains no elements.
        *
        * @return <tt>true</tt> if this collection contains no elements
        * 判断集合是否为空，如果集合大小为0，则返回true     
        */
       boolean isEmpty();

       /**
        * Returns <tt>true</tt> if this collection contains the specified element.
        * @param o element whose presence in this collection is to be tested
        * @return <tt>true</tt> if this collection contains the specified element    
        * 判断该集合是否包含指定的元素，如何包含，则返回true
        */
       boolean contains(Object o);

       /**
        * Returns an iterator over the elements in this collection.  There are no
        * guarantees concerning the order in which the elements are returned
        * (unless this collection is an instance of some class that provides a
        * guarantee).
        *
        * @return an <tt>Iterator</tt> over the elements in this collection
        * 继承的是Iterable接口的iterator方法，返回该集合的一个迭代器，在遍历时，使用的是Iterator接口的next方法
        */
        Iterator<E> iterator();
        
｝
```



