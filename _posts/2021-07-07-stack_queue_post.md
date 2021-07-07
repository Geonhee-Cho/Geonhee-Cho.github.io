---
title: "java arr를 이용한 stack과 queue 구현"
date: 2021-07-07 10:36:12 -0400
categories: study
---

----
스택

	public class Stack {
		int[] arr = null;
		int top = 0;

		Stack(int size){
			arr = new int[size];
		}

		public void push(int number){
			if(top+1 == arr.length){
				System.out.println("Stack OverFlow!");
				return;
			}else{
				arr[top] = number;
				top ++;
				System.out.println("push("+number+")!");
			}
		}

		public void pop(){
			if(top == 0){
				System.out.println("Stack UnderFlow!");
				return;
			}else{
				int popNumber = arr[top-1];
				top --;
				arr[top] = 0;
				System.out.println("pop("+popNumber+")!");
			}
		}

		public void showStack(){
			if(top == 0){
				System.out.println("Stack is Empty!");
				return;
			}else{
				for(int i=top-1; i >= 0; i--){
					System.out.println(i+"-> | "+arr[i]);
				}
			}
		}
	}

----
순환큐

	public class Queue {
		int[] arr = null;
		int front = 0;
		int rear = 0;
		int deleteNumber = 0;

		Queue(int size){
			arr = new int[size+1];
			for(int i = 0; i < arr.length; i++){
				arr[i] = --deleteNumber;
			}
		}

		public void enqueue(int number){
			if(number < 0){
				System.out.println("Please enter a positive number");
				return;
			}

			int tempRear = rear;

			if(rear == arr.length-1){
				tempRear = -1;
			}

			if(arr[tempRear+1] == arr[front]){
				System.out.println("Queue is Full!");
				return;
			}else{
				arr[rear] = number;
				rear = tempRear;

				rear ++;
				System.out.println("enqueue("+number+")!");
			}
		}

		public void dequeue(){
			if(front == rear){
				System.out.println("Queue is Empty!");
				return;
			}else{
				int dequeueNumber = arr[front];
				arr[front] = --deleteNumber;

				if(front == arr.length-1){
					front = -1;
				}

				front ++;
				System.out.println("dequeue("+dequeueNumber+")!");
			}
		}

		public void showQueue(){
			if(front == rear){
				System.out.println("Queue is Empty!");
				return;
			}else{
				int showCount = (front > rear) ? arr.length - (front - rear) : rear - front;

				System.out.print("Front");
				for(int i=0; i < showCount; i++){
					int idx = front+i;
					if(idx > arr.length-1){
						idx -= arr.length;
					}
					System.out.print(" "+arr[idx]);
				}
				System.out.print(" Rear");
			}
		}
	}

----

지난번에 정리한 자료구조를 바탕으로 스택과 순환큐를 java arr를 통해 구현해봤습니다.

스택은 고려할 사항이 많지 않고 알고리즘 문제로도 많이 봐서 10분? 정도 걸렸습니다만..

순환힙은 생각보다 처리할게 많더군요...

제가 구현한 힙은 음수를 넣을 수 없게 구현했습니다.

처음 힙의 사이즈를 받고 arr를 생성 해주면 모든 항목이 0으로 초기화 됩니다.

그렇게 되면 순환힙 '후단의 다음항목의 값이 전단의 값과 같을때 가득찬 상태' 를 만족하기 때문에 enqueue가 불가능 했습니다.

그래서 arr를 생성해준 후 각 항목을 1씩 증가하는 음수로 초기화 해주었습니다.

다음에 기회가 된다면 음수도 넣을 수 있는 방법을 생각해보겠습니다..

알고리즘 문제 풀때를 제외하곤 사실 써본적이 없어서 한번 구현해본건데.. 나름 재밌었습니다!

감사합니다!
