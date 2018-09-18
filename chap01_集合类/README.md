首先声明，这里提到的集合指的就是java.util包下的容器类，不只是java.util.Collection。至于Map属不属于集合类，这个问题也没必要钻牛角尖，自己知道Map是什么就好，只是翻译的差异。我认为Map也是一堆键值对的集合，属于集合类。

可以把集合类形象地理解成一系列对象的集合，在平时开发过程中使用非常广泛，也是笔试面试中的高频考点。可以分为两大接口：Collection和Map，再往下又分别对应于多个接口与实现。集合类接口的大致层次关系如下图所示：

> - Iterable                   迭代器功能，支持foreach语法
>
>    - Collection               集合超类，有add,remove等方法
>        - List                   允许重复数据的表，新添了get,set,indexof,subList等方法
>        - Queue                  先进先出或先进后出的队列，新添了offer,poll,peek等方法
>            - Deque                双端队列，新添了addFirst,addLast,removeFirst,removeLast等方法
>        - Set                    不允许重复数据的无序表，没有新添方法
>           - SortedSet            排好序的set结构,新添了comparator,first,last,subSet等方法
>              - NavigableSet       用于元素最近匹配查找的set结构，新添了lower,floor,ceiling,higher,pollFirest,pollLast等方法
> - Map                        关联容器，键不允许重复，包含Entry接口，对应每个键值对实体
>    - SortedMap               排好序的map结构，新添了comparator,firstkey,lastkey,subMap等方法
>        - NavigableMap           用于元素最近匹配查找的map结构，新添了lowerEntry,floorEntry,ceilingEntry,等方法

具体每个接口及实现会在下面详细介绍。

