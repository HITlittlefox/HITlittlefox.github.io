---
title: DataStructure-review-01
category: Java
date: 2021-12-17 15:48:17
tags:
---
知识点、设计类、例题


```java
//顺序表类设计见教材P17
package chap2.List_SeqList;

//顺序线性表设计
public class SeqList implements List {
	final int defaultSize = 10;

	int maxSize;
	int size;
	Object[] listArray;

	public SeqList() {
		initiate(defaultSize);
	}

	public SeqList(int size) {
		initiate(size);
	}

	private void initiate(int sz) {
		maxSize = sz;
		size = 0;
		listArray = new Object[sz];
	}


	//定点插入
	public void insert(int i, Object obj) throws Exception {
		if (size == maxSize) {
			throw new Exception("顺序表已满无法插入！");
		}
		if (i > size) {
			throw new Exception("参数错误！");
		}

		for (int j = size; j > i; j--) {
			listArray[j] = listArray[j - 1];
		}

		listArray[i] = obj;
		size++;
	}

    //定点删除
	public Object delete(int i) throws Exception {
		if (size == 0) {
			throw new Exception("顺序表已空无法删除！");
		}
		if (i > size - 1) {
			throw new Exception("参数错误！");
		}
		Object it = listArray[i];
		for (int j = i; j < size - 1; j++) {
			listArray[j] = listArray[j + 1];
		}

		size--;
		return it;
	}

    //定点获取数据
	public Object getData(int i) throws Exception {
		if (i < 0 || i >= size) {
			throw new Exception("参数错误！");
		}
		return listArray[i];
	}

	public int size() {
		return size;
	}

	public boolean isEmpty() {
		return size == 0;
	}

    //多数据删除
	public int MoreDataDelete(SeqList L, Object x) throws Exception {

		int i, j;
		int tag = 0;

		for (i = 0; i < L.size; i++) {
			if (x.equals(L.getData(i))) {
				L.delete(i);
				i--;
				tag = 1;
			}
		}

		return tag;
	}
}

```

```java
package chap2.SingleList;

//结点类设计见教材
public class Node {
    Object data; // 数据元素
    Node next; // 表示下一个结点的对象引用

    Node(Node nextval) { // 用于头结点的构造函数1
        next = nextval;
    }

    Node(Object obj, Node nextval) { // 用于其他结点的构造函数2
        data = obj;
        next = nextval;
    }

    public Node getNext() { // 取next
        return next;
    }

    public void setNext(Node nextval) { // 置next
        next = nextval;
    }

    public Object getElement() { // 取data
        return data;
    }

    public void setElement(Object obj) { // 置data
        data = obj;
    }

    public String toString() { // 转换data为String类型
        return data.toString();
    }
}

```

```java
package chap2.SingleList;

//单链表类的定义见教材P27
//单链表
public class LinList implements List {
    Node head;
    Node current;
    int size;

    LinList() {
        head = current = new Node(null);
    }

    public void index(int i) throws Exception {
        if (i < -1 || i > size - 1) {
            throw new Exception("参数错误！");
        }
        if (i == -1)
            return;
        current = head.next;
        int j = 0;
        while ((current != null) && j < i) {
            current = current.next;
            j++;
        }
    }

    public void insert(int i, Object obj) throws Exception {
        if (i < 0 || i > size) {
            throw new Exception("参数错误！");
        }
        index(i - 1);
        //“待插入结点”的上一结点的下一结点是“待插入结点”，“待插入结点”的下一结点是其上一结点刚才的下一结点
        current.setNext(new Node(obj, current.next));
        size++;
    }

    public Object delete(int i) throws Exception {
        if (size == 0) {
            throw new Exception("链表已空无元素可删！");
        }
        if (i < 0 || i > size - 1) {
            throw new Exception("参数错误！");
        }

        index(i - 1);
        Object obj = current.next.getElement();
        current.setNext(current.next.next);
        size--;
        return obj;
    }

    public int size() {
        return size;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public Object getData(int i) throws Exception {
        if (i < -1 || i > size - 1) {
            throw new Exception("参数错误！");
        }
        index(i);
        return current.getElement();
    }
}


```

```java
//循环单链表类实现见补充教材P25
```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

```java

```

