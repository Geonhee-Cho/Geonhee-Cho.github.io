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
