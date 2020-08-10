```java
// 双向循环链表

/**
 * 双向循环链表
 * 功能：追加，根据序号获取元素，插入，删除
 *
 */
public class MyLinkedList<E> {

	private Node head;
	private int size;
	private class Node{
		E data;
		Node next;
		Node prev;
		Node(E e) {
			data = e;
		}
	}
	
	public String toString() {
		if (head == null) {
			return "[]";
		}
		// 遍历每个元素
		StringBuilder buf = new StringBuilder("[");
		buf.append(head.data);
		Node node = head.next;
		while (node != head) {
			buf.append(",").append(node.data);
			node = node.next;
		}
		return buf.append("]").toString();
	}
	
	// 长度
	public int size() {
		return size;
	}
	
	/**
	 * 插入
	 * @param index 下标
	 * @param e 元素
	 * @return
	 */
	public boolean add(int index, E e) {
		if (index < 0 || index > size) {
			throw new IndexOutOfBoundsException("越界");
		}
		if (index == size) {
			return add(e);
		}
		Node node = new Node(e);
		Node next = find(index);
		Node prev = next.prev;
		prev.next = node;
		node.next = next;
		next.prev = node;
		node.prev = prev;
		if (index == 0) {
			head = node;
		}
		size++;
		return true;
	}
	
	/**
	 * 删除
	 * @param index 下标
	 * @return
	 */
	public E delete(int index) {
		if(index<0 || index>=size) {
			throw new IndexOutOfBoundsException("超范围");
		}
		if (size == 1) {
			E e = head.data;
			head = null;
			size--;
			return e;
		}
		Node node = find(index);
		Node next = node.next;
		Node prev = node.prev;
		next.prev = prev;
		prev.next = next;
		node.prev = null;
		node.next = null;
		if (index == 0) {
			head = next;
		}
		size--;
		return node.data;
	}
	
	
	private Node find(int index) {
		Node node;
		if (index < size >> 1) { // 往左半部查找
			node = head;
			for (int i=0; i<index; i++) {
				node = node.next;
			}
		} else { // 往后半部分查找
			node = head.prev;
			for (int i=size-1;i>index;i--) {
				node = node.prev;
			}
		}
		return node;
	}
	
	public E get(int index) {
		if (index<0 || index >=size) {
			throw new IndexOutOfBoundsException("超范围");
		}
		Node node = find(index);
		return node.data;
	}
	
	// 向链表尾部追加元素
	public boolean add(E e) {
		if (head == null) {
			head = new Node(e);
			// 建立双向循环链表
			head.next = head;
			head.prev = head;
		} else {
			// 第二个节点及以后的节点
			Node node = new Node(e);
			Node last = head.prev;
			// 建立双向循环关系
			last.next = node;
			node.next = head;
			head.prev = node;
			node.prev = last;
		}
		size++;
		return true;
	}
}
```

```java
// 双向链表

/**
 * 双向链表
 *
 */
public class MyLinkedList1<E> {

	private Node head; // 头结点
	private Node tail; // 最后一个节点
	private int size;
	private class Node {
		E data;
		Node next;
		Node prev;
		Node(E e) {
			data = e;
		}
	}
	
	public String toString() {
		if (head == null) {
			return "[]";
		}
		// 遍历每个元素进行拼接
		StringBuilder buf = new StringBuilder("[");
		buf.append(head.data);
		Node node = head.next;
		while (node != null) {
			buf.append(", ").append(node.data);
			node = node.next;
		}
		return buf.append("]").toString();
	}
	
	public int size() {
		return size;
	}
	
	/**
	 * 通过位置插入元素
	 * @param index
	 * @param e
	 * @return
	 */
	public boolean add(int index, E e) {
		if (index<0 || index>size) {
			throw new IndexOutOfBoundsException();
		}
		if (index == size) {
			return add(e);
		}
		Node node = new Node(e);
		Node next = find(index);
		Node prev = next.prev;
		if (index == 0) { // 头部添加
			node.next = next;
			next.prev = node;
			head = node;
		} else {
			prev.next = node;
			node.next = next;
			next.prev = node;
			node.prev = prev;
		}
		size++;
		return true;
		
	}
	
	/**
	 * 删除元素
	 * @param index
	 * @return
	 */
	public E delete(int index) {
		if (index<0 || index>=size) {
			throw new IndexOutOfBoundsException();
		}
		if (size == 1) {
			Node node = head;
			head = null;
			tail = null;
			size--;
			return node.data;
		}
		Node node = find(index);
		Node prev = node.prev;
		Node next = node.next;
		if (next == null) { // 如果下一个为空说明是删除最后一个
			prev.next = null;
			tail = prev;
		} else if (prev == null) { // 如果上一个为空说明删除第一个元素
			next.prev = null;
			head = next;
		} else {
			prev.next = next;
			next.prev = prev;
		}
		size--;
		return node.data;
		
	}
	
	/**
	 * 寻找元素
	 * @param index
	 * @return
	 */
	private Node find(int index) {
		Node node;
		if (index < size >> 1) { // 向左查找
			node = head;
			for (int i=0;i<index;i++) {
				node = node.next;
			}
		} else { // 向右查找
			node = tail;
			for (int i=size-1;i>index;i--) {
				node = node.prev;
			}
		}
		return node;
	}
	
	public E get(int index) {
		if (index < 0 || index >= size) {
			throw new IndexOutOfBoundsException();
		}
		Node node = find(index);
		return node.data;
	}
	
	/**
	 * 添加元素
	 * @param e
	 * @return
	 */
	public boolean add(E e) {
		Node node = new Node(e);
		if (head == null) {
			head = node;
			tail = head;
			head.prev = null;
			head.next = null;
		} else {
			tail.next = node;
			node.prev = tail;
			tail = node;
		}
		size++;
		return true;
	}
	

}
```

```java
// 单向链表

/**
 * 单向链表
 */
public class MyLinkedList2<E> {

	private Node head;
	private Node tail;
	private int size;
	private class Node{
		E data;
		Node next;
		Node(E e) {
			data = e;
		}
	}
	
	public String toString() {
		if (head == null) {
			return "[]";
		}
		StringBuilder buf = new StringBuilder("[");
		buf.append(head.data);
		Node node = head.next;
		while (node != null) {
			buf.append(", ").append(node.data);
			node = node.next;
		}
		return buf.append("]").toString();
	}
	
	public int size() {
		return size;
	}
	
	public E get(int index) {
		if (index<0 || index>=size) {
			throw new IndexOutOfBoundsException();
		}
		Node node = find(index);
		return node.data;
	}
	
	public boolean add(int index, E e) {
		if (index<0 || index>size) {
			throw new IndexOutOfBoundsException();
		}
		if (index == size) {
			return add(e);
		}
		Node node = new Node(e);
		Node next = find(index);
		if (index > 0) {
			Node prev = find(index-1);
			prev.next = node;
			node.next = next;
		} else {
			node.next = next;
			head = node;
		}
		size++;
		return true;
	}
	
	private Node find(int index) {
		Node node = head;
		for (int i=0;i<index;i++) {
			node = node.next;
		}
		return node;
	}
	
	public boolean add(E e) {
		Node node = new Node(e);
		if (head == null) {
			head = node;
			tail = head;
			head.next = null;
		} else {			
			tail.next = node;
			tail = node;
		}
		size++;
		return true;
	}
}
```

