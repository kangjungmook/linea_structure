<h1> 선형구조</h1>

* 리스트
* 스택
* 큐
* 뎈

<h1> 비선형 구조</h1>

* 트리









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


<h2> 스택 구현 </h2>

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

<h3> 트리(tree) </h3>

트리는 정점(node)과 선분(branch)를 이용하여 사이클을 이루지 않도록 구성한 그래프(Graph)의 특수한 형태이다.
* 가족이 계보(족보), 연산수칙, 회사 조직 구성도, 히프(Heep) 등을 표현하기에 적합하다

<h3> 이진트리 </h3>

![image](https://user-images.githubusercontent.com/106642094/227130445-784650f7-244f-4e82-908c-e85042c6b4d4.png)

- 디그리(Degree) : 차수로 각 노드에서 뻗어 나온 가지의 수
-> A=3, B=2, C=1, D=3
- 단말 노드(Terminal Node, = 잎(Leaf) 노드 ) : 자식이 없는 노드 즉, Degree(차수)가 0인 노드
-> K L, F, G, M, I, J
- 비단말 노드(Non-Terminal Node) : 자식이 하나라도 있는 노드, Degree(차수)가 0이 아닌 노드
-> A, B, C, D, E, H
- 조상 노드(Ancestors Node) : 임의의 노드에서 근 노드에 이르는 경로상에 있는 노드들
-> M의 조상 노드는 H, D, A
- 자식 노드(Son Node) : 어떤 노드에 연결된 다음 레벨의 노드들
-> D의 자식 노드는 H, I, J
- 부모 노드(Parent Node) : 어떤 노드에 연결된 이전 레벨의 노드들
-> E, F의 부모 노드는 B
- 형제 노드(Brother Node, Sibling) : 동일한 부모를 갖는 노드들
-> H의 형제 노드는 I, J

모든 노드들의 자식 노드가 두 개 이하인 트리를 의미한다. 다음은 이진트리의에다 이런 이진 트리에서는
서브 트리가 두 개 이하기 때문에 서브 트리는 왼쪽 서브 트리와 오른쪽 서브 트리로 구분한다.

![image](https://user-images.githubusercontent.com/106642094/227129406-a82e8313-85cd-4a49-8091-0244d3c7e15a.png)

## 이진 트리(Binary tree)

![image](https://user-images.githubusercontent.com/106642094/227129612-30ceef75-bc2a-4f19-8282-f6d773058579.png) 

## 전이진 트리(Complete Binary Tree)  

<h4>전이진 트리는 노드의 수가n개일 때, 정이진 트리의

각 노드에 붙힌 1~n의 일련번호와 1:1 대응되는 트리를 말한다.

중간에 빈 부분이 있으면 전이진 트리가 될 수 없다.

+ 사향 이진 트리(Skewed Binary Tree)

사향 이진 트리는 루트 노드로 부터 왼쪽 또는 오른쪽으로만 기울어진 트리, 즉

왼쪽 또는 오른쪽 자식이 없는 노드들로 만 구성된 트리다.

- 왼쪽 사향 이진 트리 : 오른쪽 자식이 없는 노드들로 만 구성된 트리

- 오른쪽 사향 이진 트리 : 왼쪽 자식이 없는 노드들로 만 구성된 트리</p>

<h3>이진 트리(binary tree)의 순회</h3>

이진 트리의 모든 노드를 특정한 순서대로 한 번씩 방문하는 것이다.
순회하는 방법에는 전위(preorder), 중위(inorder), 후위(postorder) 순회가 있다.</h4>

## - 전위 순회(Preorder)

<h4>노드(루트)를 먼저 방문하고 왼쪽 서브 트리, 오른쪽 서브 트리 순으로 방문

루트 방문 ➞ 왼쪽 서브 트리 방문 ➞ 오른쪽 서브 트리 방문 (Root -> Left -> Right)

- 중위 순회(Inorder)

왼쪽 서브 트리, 루트, 오른쪽 서브 트리 순으로 방문

왼쪽 서브 트리 방문 ➞ 루트 방문 ➞ 오른쪽 서브 트리 방문 (Left -> Root -> Right)

- 후위 순회(Posorder)

왼쪽 서브 트리, 오른쪽 서브 트리, 루트 순으로 방문

왼쪽 서브 트리 방문 ➞ 오른쪽 서브 트리 방문 ➞ 루트 방문 (Left -> Right -> Root)</p> 

- 전위 순회(Preorder)

노드(루트)를 먼저 방문하고 왼쪽 서브 트리, 오른쪽 서브 트리 순으로 방문

루트 방문 ➞ 왼쪽 서브 트리 방문 ➞ 오른쪽 서브 트리 방문(Root -> Left -> Right)

-> A, B, D, E, F, C

- 중위 순회(Inorder)

왼쪽 서브 트리, 루트, 오른쪽 서브 트리 순으로 방문

왼쪽 서브 트리 방문 ➞ 루트 방문 ➞ 오른쪽 서브 트리 방문 (Left -> Root -> Right)

-> D, B

- 중위 순회(Inorder)

왼쪽 서브 트리, 루트, 오른쪽 서브 트리 순으로 방문

왼쪽 서브 트리 방문 ➞ 루트 방문 ➞ 오른쪽 서브 트리 방문 (Left -> Root -> Right)

-> D, B, F, E

- 중위 순회(Inorder)

왼쪽 서브 트리, 루트, 오른쪽 서브 트리 순으로 방문

왼쪽 서브 트리 방문 ➞ 루트 방문 ➞ 오른쪽 서브 트리 방문 (Left -> Root -> Right)

-> D, B, F, E, A, C

- 후위 순회(Postorder)

왼쪽 서브 트리, 오른쪽 서브 트리, 루트 순으로 방문

왼쪽 서브 트리 방문 ➞ 오른쪽 서브 트리 방문 ➞ 루트 방문 (Left -> Right -> Root)

-> D

- 후위 순회(postorder)

왼쪽 서브 트리, 오른쪽 서브 트리, 루트 순으로 방문

왼쪽 서브 트리 방문 ➞ 오른쪽 서브 트리 방문 ➞ 루트 방문 (Left -> Right -> Root)

-> D, F, E

- 후위 순회(Potorder)

왼쪽 서브 트리, 오른쪽 서브 트리, 루트 순으로 방문

왼쪽 서브 트리 방문 ➞ 오른쪽 서브 트리 방문 ➞ 루트 방문 (Left -> Right -> Root)

-> D, F, E, B, C, A</h4>

## 이진 트리 탐색(Binary Search Tree)

<h4> 이진 탐색 트리(binary search tree)는 데이터의 삽입, 삭제, 탐색 등이 자주 발생하는

경우에 효율적인 구조로, 이진 트리이면서 같은 값을 갖는 노드가 없어야 한다.

왼쪽 서브 트리에 있는 모든 데이터는 현재 노드의 값보다 작고,

오른쪽 서브 트리에 있는 모든 노드의 데이터는 현재 노드의 값보다 크다.

데이터 탐색은 루트에서부터 시작된다.

- 루트 노드의 데이터와 찾으려는 데이터를 비교하여 같으면 탐색은 성공 종료

- 루트 노드가 작으면 루트 노드의 오른쪽

- 루트 노드가 크면 루트 노드의 왼쪽

이진 트리 탐색(Binary Search Tree)

이진 탐색 트리(binary search tree)는 데이터의 삽입, 삭제, 탐색 등이 자주 발생하는

경우에 효율적인 구조로, 이진 트리이면서 같은 값을 갖는 노드가 없어야 한다.

왼쪽 서브 트리에 있는 모든 데이터는 현재 노드의 값보다 작고,

오른쪽 서브 트리에 있는 모든 노드의 데이터는 현재 노드의 값보다 크다.

데이터 탐색은 루트에서부터 시작된다.

- 루트 노드의 데이터와 찾으려는 데이터를 비교하여 같으면 탐색은 성공 종료

- 루트 노드가 작으면 루트 노드의 오른쪽

- 루트 노드가 크면 루트 노드의 왼쪽</h4>

## 이진 트리 삽입

이진 탐색 트리에서의 삽입은 탐색 동작을 통해 이루어진다.
탐색에 성공하면 삽입은 실패하는데, 이는 이진 탐색 트리는 같은 데이터를 갖는
노드가 없어야 하기 때문이다.
반면에 탐색에 실패하면 삽입을 할 수 있으며, 탐색에 종료된 지점의 데이터를 값으
로 하는 노드가 삽입된다.
삽입할 위치는 루트 노드에서부터 시작되며 삽입할 노드의 데이터가 비교하는 노드
의 데이터보다 작으면 왼쪽 서브 트리로 진행하고 크면 오른쪽 서브 트리로 진행한다

![image](https://user-images.githubusercontent.com/106642094/227134721-ec1e90c3-a8ea-4834-b9ea-1bd05d66aee1.png)

## 이진 트리 삭제

이진 탐색 트리에서 노드를 삭제하는 동작은 삭제할 노드의 위치에 따라 세 가지로
구분된다.</br>
* 삭제할 노드가 단말 노드인 경우
부모 노드에서 삭제할 노드를 가리키는 링크를 제거하면 된다.</br>
-> 데이터가 6인 노드를 삭제하려면
부모 노드인 데이터가 7인 노드에서 삭제할 노드를 가리키는 링크를 제거

![image](https://user-images.githubusercontent.com/106642094/227135360-efcd8a09-bf3b-474d-a2ec-f1852aacca82.png)

* 삭제할 노드의 자식 노드가 하나인 경우
부모 노드에서 삭제할 노드를 가리키는 링크를 삭제할 노드의 자식 노드를 가리킨다.</br>

-> 12인 노드를 삭제하려면 데이터가 12인 노드를 삭제하고,
데이터가 12인 노드의 부모 노드, 즉 데이터가 10인 노드가 삭제된 노드의 자식 노드인
데이터 15인 노드를 가리키게 한다.

### 노드생성 코드
```java
```


















