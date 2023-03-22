<h2> 1.선형구조</h3>

<h3>리스트</h3>

관련된 자료들이 일정하게 나열되어 있는 구조를 리스트라고 한다.

![image](https://user-images.githubusercontent.com/106642094/226522751-ac9a7a50-5b52-408c-80f9-90db4d2cfd88.png)


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

![image](https://user-images.githubusercontent.com/106642094/226522834-989817c8-0c29-413a-973d-4bc520b2a568.png)

![image](https://user-images.githubusercontent.com/106642094/226522851-d1ba72fd-cc23-4a1b-8dcf-619cdece84d2.png)
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

<h3> 큐 (queue)</h3>

*  큐(queue)는 한쪽 방향으로 데이터가 삽입되고 반대 방향으로 데이터가 삭제되는 </br>
들어온 데이터가 먼저 나가는 선입 선출(First In Fist Out)구조이다.

- 컴퓨터 시스템의 작업 스케줄에서 특별한 우선 순위가 없는 경구 먼저 들어온 프로세스가</br>
먼저 처리 된다
- 계산대에서 계산대에 먼저 도착한 고객이 먼저 계산하고 나간다.</br>
- 버스 승강장에서 앞에 선 사람이 먼저 승리한다

![image](https://user-images.githubusercontent.com/106642094/226807921-7c648336-f0ba-4ed6-ab9e-106679773a2a.png)

<h3> 프런트 (Front) </h3>

* 가장 먼저 삽입된 자료의 기억 공간을 가리키는 포인터 이다.
* 삭제 작업을 할 때 사용

<h3> 리어 (Rear) </h3>
* 가장 마지막에 삽입된 자료가 위치한 기억 장소를 가리키는 포인터 이다.
* 삽입 작업을 할 때 사용

<h3> Queue의 응용 분야 </h3>

* 창구 업무나 택시 정거장처럼 서비스순서를 기다리는 등의 대기 행열의 처리에 사용한다.
* 운영 체제의 작업 스케줄링에 사용

![image](https://user-images.githubusercontent.com/106642094/226808539-6bef92bd-04f2-43aa-994e-dd769532107a.png)

<h3> 뎈Deque </h3>

* 삽입과 삭제가 양쪽 끝에서 모두 발생할 수 있는 자료 구조이다.

![image](https://user-images.githubusercontent.com/106642094/226808911-d6718487-95bc-43e1-9ff7-1251a069d6d3.png)

```java
public class intQueue {
	private int que[]; //큐용 배열
	private int capacity; // 큐의 크기
	private int front; // 맨 처음 요소의 커서
	private int rear; //맨끝 요소의 커서
	private int num; //현재 데이터 개수
	
	// 실행시 예외 : 큐이 비어있음
	public class EmptyIntQueueException extends RuntimeException {
		public EmptyIntQueueException() {}
	}
	// 실행시 예외 : 큐이 가득참
	public class OverflowIntQueueException extends RuntimeException {
		 public OverflowIntQueueException() {}
	}
	
	// 생성자
	public intQueue(int maxlen) {
		num = front = rear = 0;
		capacity = maxlen;
		try {
			que = new int[capacity];
			// 큐 본체용 배열 생성
		} catch (OutOfMemoryError e) {
			// 생성 할수 없음
			capacity = 0;
		}
	}
	
	public int enque(int x) throws OverflowIntQueueException {
		if(num >=capacity) {
			throw new OverflowIntQueueException();
		
		}
		que[rear ++] =x;
		num++;
		if(rear == capacity) {
			rear = 0;
		}
		return x;
	}
	
	
	public int deque() throws EmptyIntQueueException {
		if (num <= 0)
			throw new EmptyIntQueueException();
		int x = que[front]++;
		num--;
		if(front == capacity) {
			front =0;
		}
		return x;
	}
	

}
```

















