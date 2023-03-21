<h2> 1.선형구조</h3>

<h3>리스트</h3>

관련된 자료들이 일정하게 나열되어 있는 구조를 리스트라고 한다.

<h3>연결 리스트</h3>

선형 리스트 : 배열(Array)과 같이 연속되는 기억장소에 저장되는 리스트입니다.
* 연결 리스트는 자료들을 반드시 연속적으로 배열시키지 않는다
* 동적 메모리에 할당된 링크에 의해 연결된 유한 개수의 데이터 원소들

<h3> 특징 </h3>

* 기억공간이 연속적으로 놓여 있지 않아도 저장이 가능하다.
* 트리를 표현할 때 가장 적합한 자료이다.
* 중간 노드 연결이 끊어지면 그 다음 노드를 찾지 못한다.
* 연결을 위한 포인터를 찾는 시간이 필요하기 때문에 접근 속도가 느리다

<h3> 노드 (node) </h3>
 
 * 자료와 포인터를 갖고 있는 것을 노드(node)라고 한다

![linkedlist](https://user-images.githubusercontent.com/106642094/226498770-92d8e0cc-d5b6-4dd7-8319-ff85ee056b23.png)

<h3>간단하게 구현</h3>

```java
public class LinkedList {
	// 첫번째 노드를 가리키는 필드
	private Node head;
	private Node tail;
	private int size = 0;
	// 데이터가 저정될 필드
	private class Node {
		private Object data;
		private Object next;
		//다음 노드를 가리키는 필드
		public Node(Object Input) {
			this.data = Input;
			this.next = null;
		}
		// 노드의 내용을 쉽게 출력해서 확인 해볼수 있는 기능
		public String toString() {
			return String.valueOf(this.data);
		}
	}
	
	public void addFirst(Object input) {
		// 노드를 생성합니다.
		Node temp = new Node(input);
		// 새로운 노드의 다음 노드로 헤드를 지정합니다
		temp.next = head;
		// 헤드로 새로운 노드로 지정합니다
		head = temp;
		size++;
		if(head.next == null) {
			tail = head;
		}
	}
	
	
    public void addLast(Object input){
        // 노드를 생성합니다.
        Node newNode = new Node(input);
        // 리스트의 노드가 없다면 첫번째 노드를 추가하는 메소드를 사용합니다.
        if(size == 0){
            addFirst(input);
        } else {
            // 마지막 노드의 다음 노드로 생성한 노드를 지정합니다.
            tail.next = newNode;
            // 마지막 노드를 갱신합니다.
            tail = newNode;
            // 엘리먼트의 개수를 1 증가 시킵니다.
            size++;
        }
    }
	

}
```

<h3> 희소행렬 </h3>

* 희소 행렬은 요소 중 많은 항들이 0 (영)으로 되어 있는 형태로 기억 장소를 절약하기
위해 링크드 리스트를 이용하여 저장한다

<h3> 1-2 스택(Stack) - LIFO</h3>
<p>스택은 리스트의 한쪽 끝으로만 자료의 삽입 및 삭제가 이루어지는 구조로 </br>먼저  삽입된 자료가 맨 나중에 삭제가 되는 후입 선출로 Lasf In First Out</br>방식이다</p>

![image](https://user-images.githubusercontent.com/106642094/226506986-7e7c316a-1fa0-46df-be3c-b856901e84eb.png)

![image](https://user-images.githubusercontent.com/106642094/226507009-41341911-103c-4511-b868-1bede771e987.png)

<h3>스택으로 간단하게 자바로 구현</h3>

```java
package sungil;

public class IntStack {
	private int[] stk; //스택의 배열
	private int capacity;// 스택의 크기
	private int ptr;// 스택 포인터
	
	//실행시 예외 : 스택이 비어있음
	public class EmptyIntStackException extends RuntimeException {
		public EmptyIntStackException() {}
	}
	//실행시 예외 : 스택이 가득참
	public class OverflowIntStackException extends RuntimeException {
		public OverflowIntStackException() {}

	}
	//생성자
	public IntStack(int maxlen) {
		ptr = 0;
		capacity = maxlen;
		try {
			stk = new int[capacity]; //스택 본체용 배열을 생성
		}catch (OutOfMemoryError e) { //생성 할 수 없음
			capacity = 0;
		}
	}
	// 스택에 x 를 푸시
	public int push(int x) throws OverflowIntStackException{
		if(ptr >= capacity)							//스택이 가득참
			throw new OverflowIntStackException();
		return stk[ptr++] = x;
	}
	public int pop() throws EmptyIntStackException{
		if(ptr == 0)								//스택이 빔	
			
			throw new EmptyIntStackException();
		return stk[--ptr];
	}
}

```

















