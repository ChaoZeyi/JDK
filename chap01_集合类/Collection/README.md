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
        * 继承的是Iterable接口的iterator方法，返回该集合的一个迭代器，在遍历时，使用的是Iterator接口
        * 的next方法
        * 对于有序的集合，比如list，则遍历顺序和数据新增顺序一致；对于set等无序集合，遍历顺序和实现
        * Comparable接口的顺序一致，按大小顺序
        */
        Iterator<E> iterator();
  
        /**
         * Returns an array containing all of the elements in this collection.
         * If this collection makes any guarantees as to what order its elements
         * are returned by its iterator, this method must return the elements in
         * the same order.
         *
         * @return an array containing all of the elements in this collection
         * 以数组的形式返回集合中的所有元素，数组中元素的顺序与遍历的顺序一致。     
         */
         Object[] toArray();
  
         /**
          * Returns an array containing all of the elements in this collection.
          * If this collection makes any guarantees as to what order its elements
          * are returned by its iterator, this method must return the elements in
          * the same order.
          * @return an array containing all of the elements in this collection
          * 功能和上面的toArray()方法一致，以数组的形式返回集合中的所有元素，数组中元素的顺序与遍历的顺
          * 序一致。
          * 不同点可参见下面的注意点第一条
         */
         <T> T[] toArray(T[] a);
  
  		/**
     	 * Ensures that this collection contains the specified element (optional
         * operation).  Returns <tt>true</tt> if this collection changed as a
         * result of the call.  (Returns <tt>false</tt> if this collection does
         * not permit duplicates and already contains the specified element.)<p>       
         *
         * @param e element whose presence in this collection is to be ensured
         * @return <tt>true</tt> if this collection changed as a result of the
         *         call
         * 往集合中新增一个元素，如果新增成功，则返回true，如果失败（集合不允许添加重复元素）则返回false
     	 */
        boolean add(E e);
  
        /**
         * Removes a single instance of the specified element from this
         * collection
         * Returns <tt>true</tt> if this collection contained the specified element (or
         * equivalently, if this collection changed as a result of the call).
         *
         * @param o element to be removed from this collection, if present
         * @return <tt>true</tt> if an element was removed as a result of this call
         * 从集合中删除一个元素，如果删除成功则返回true，如果失败(集合中不存在该元素)则返回false
         */
    	boolean remove(Object o);

        /**
         * Returns <tt>true</tt> if this collection contains all of the elements
         * in the specified collection.
         *
         * @param  c collection to be checked for containment in this collection
         * @return <tt>true</tt> if this collection contains all of the elements
         *         in the specified collection
         * 判断该集合是否包含指定集合的所有元素，如果包含则返回true，强调的是元素间的包含关系，可以是一个
         * set包含一个list
         */
        boolean containsAll(Collection<?> c);

        /**
         * Adds all of the elements in the specified collection to this collection
         * (optional operation).  The behavior of this operation is undefined if
         * the specified collection is modified while the operation is in progress.
         * (This implies that the behavior of this call is undefined if the
         * specified collection is this collection, and this collection is
         * nonempty.)
         *
         * @param c collection containing elements to be added to this collection
         * @return <tt>true</tt> if this collection changed as a result of the call
         * 新增指定集合中的所有元素，如果所有元素均添加成功，则返回true
         */
        boolean addAll(Collection<? extends E> c);

        /**
         * Removes all of this collection's elements that are also contained in the
         * specified collection (optional operation).  After this call returns,
         * this collection will contain no elements in common with the specified
         * collection.
         *
         * @param c collection containing elements to be removed from this collection
         * @return <tt>true</tt> if this collection changed as a result of the call
         * 从集合中删除指定集合中的所有元素，相当于求两个集合的差集，
         * a = {1,2,3,4}, b = {3,5}，a.removeAll(b)之后，a = {1,2,4}
         * 如果原集合发生了改变，则返回true        
         */
        boolean removeAll(Collection<?> c);

        /**
         * Removes all of the elements of this collection that satisfy the given
         * predicate.  Errors or runtime exceptions thrown during iteration or by
         * the predicate are relayed to the caller.
         * @param filter a predicate which returns {@code true} for elements to be
         *        removed
         * @return {@code true} if any elements were removed
         * @since 1.8
         * 按照规则过滤集合中的元素，通常和lambda表达式连用
         * collection.removeIf(x -> x.getAge()>30) 去掉集合中所有年龄大于30的对象
         * 如果集合元素发生改变，则返回true
         */
        default boolean removeIf(Predicate<? super E> filter) {
            Objects.requireNonNull(filter);
            boolean removed = false;
            final Iterator<E> each = iterator();
            while (each.hasNext()) {
                if (filter.test(each.next())) {
                    each.remove();
                    removed = true;
                }
            }
            return removed;
        }

        /**
         * Retains only the elements in this collection that are contained in the
         * specified collection (optional operation).  In other words, removes from
         * this collection all of its elements that are not contained in the
         * specified collection.
         *
         * @param c collection containing elements to be retained in this collection
         * @return <tt>true</tt> if this collection changed as a result of the call
         * 取两个集合的交集，如果原集合发生了变化，则返回的是true，可以和removeAll()方法对比
         */
        boolean retainAll(Collection<?> c);

        /**
         * Removes all of the elements from this collection (optional operation).
         * The collection will be empty after this method returns.
         *
         * @throws UnsupportedOperationException if the <tt>clear</tt> operation
         *         is not supported by this collection
         * 清空集合中的所有元素，执行该方法后，集合为empty
         */
        void clear();
  
        /**
         * Compares the specified object with this collection for equality. <p>
         *
         * @param o object to be compared for equality with this collection
         * @return <tt>true</tt> if the specified object is equal to this collection
         * 继承自Object基类的方法，判断两个对象是否相等
         */
        boolean equals(Object o);

        /**
         * Returns the hash code value for this collection.  
         * @return the hash code value for this collection
         * 继承自Object基类的方法，得到集合的哈希值
         */
        int hashCode();

        /**
         * Creates a {@link Spliterator} over the elements in this collection.
         *
         * @return a {@code Spliterator} over the elements in this collection
         * @since 1.8
         * 继承自Iterable的方法，java8之后添加的对stream的支持
         */
        @Override
        default Spliterator<E> spliterator() {
            return Spliterators.spliterator(this, 0);
        }

        /**
         * Returns a sequential {@code Stream} with this collection as its source.
         *
         * @return a sequential {@code Stream} over the elements in this collection
         * @since 1.8
         * 使用spliterator()方法得到的Spliterator，返回所有集合元素的一个Stream对象
         */
        default Stream<E> stream() {
            return StreamSupport.stream(spliterator(), false);
        }

        /**
         * Returns a possibly parallel {@code Stream} with this collection as its
         * source.  It is allowable for this method to return a sequential stream.
         *
         * @return a possibly parallel {@code Stream} over the elements in this
         * collection
         * @since 1.8
         * 相比于上面的stream()方法，该方法返回的是一个并行流，使用fork/join并行方式来拆分任务和加速处
         * 理过程，相当于是将大任务拆分成多个互不依赖的子任务队列，每个任务队列都由一个线程来执行，这样就
         * 存在线程安全的问题，需要特别注意
         */
        default Stream<E> parallelStream() {
            return StreamSupport.stream(spliterator(), true);
        }
｝
```

### 注意点：

1. Object\[\] toArray\(\);与&lt;T&gt; T\[\] toArray\(T\[\] a\);    两者功能相同，区别在于：前者返回的是Object\[\]，当需要强制转换成Integer\[\]时，会报错：`Exception in thread "main" java.lang.ClassCastException: [Ljava.lang.Object; cannot be cast to [Ljava.lang.Integer;`在这种情况下，就可以使用后面的方法： `Integer[] y = x.toArray(new Integer[1]);`
2. java8下新增了几个和lambda表达式以及stream相关的default方法，需要特别注意。



