# priority-queue-with-linklist
Node.h

#include<iostream>
class Node
{
private:
	int data;
	int key; //priority 
	Node* next;
public:
	Node();
	Node(int data, int key);
	void setData(int data);
	void setKey(int key);
	void setNext(Node* next);
	int getData();
	int getKey();
	Node* getNext();

};

Queue.h
#include<iostream>
#include "Node.h"
class Queue
{
private:
	Node* front;
	Node* rear;

public:
	Queue();
	void enQueue(int, int);
	void deQueue();
	bool isEmpty();
	void print();
	void sort();
	void swap(Node*, Node*);
};

imp

#include "Queue.h"
#include <iostream>
using namespace std;


Node::Node()
{
	data = 0;
	key = 0;
	next = NULL;
}
Node::Node(int data, int key)
{
	this->data = data;
	this->key = key;
	this->next = NULL;

}
void Node::setData(int data)
{
	this->data = data;
}
void Node::setKey(int key)
{
	this->key = key;
}
void Node::setNext(Node* next)
{
	this->next = next;
}
int Node::getData()
{
	return data;
}
int Node::getKey()
{
	return key;
}
Node* Node::getNext()
{
	return next;
}

bool Queue::isEmpty()
{
	if (front == NULL && rear == NULL)
	{
		return true;
	}
	else
	{
		return false;
	}
}

Queue::Queue()
{
	front = NULL;
	rear = NULL;
}

void Queue::deQueue()
{
	if (isEmpty())
	{
		return;
	}
	else
	{
		Node* temp = front;
		front = front->getNext();
		delete temp;
	}
}

void Queue::enQueue(int data, int key)
{
	if (isEmpty())
	{
		Node* new_Node = new Node(data, key);
		front = new_Node;
		rear = new_Node;
	}
	else
	{
		Node* new_Node = new Node(data, key);
		rear->setNext(new_Node);
		rear = new_Node;
		sort();
	}
}

void Queue::print()

{
	Node* temp = front;
	cout << "\tData\t\tPriority" << endl;
	while (temp != NULL)
	{
		cout << "\t" << temp->getData() << "\t\t" << temp->getKey() << endl;
		temp = temp->getNext();
	}

}
void Queue::swap(Node* current, Node* next)
{
	int tempData = current->getData();
	int tempKey = current->getKey();
	current->setData(next->getData());
	current->setKey(next->getKey());
	next->setData(tempData);
	next->setKey(tempKey);
}

void Queue::sort()
{
	for (Node* temp = front; temp->getNext() != NULL; temp = temp->getNext())
	{
		for (Node* temp2 = temp->getNext(); temp2 != NULL;temp2 = temp2->getNext())
		{
			if (temp2->getKey() < temp->getKey())
			{
				swap(temp, temp2);
			}
		}
	}
}

main
#include <iostream>
#include "Queue.h"
using namespace std;

int main() 
{
    Queue queue;

    cout << "elements into the priority queue:" << endl;
    queue.enQueue(10, 2);
    queue.enQueue(20, 1);
    queue.enQueue(30, 3);
    queue.enQueue(40, 0);

    cout << "\nPriority queue after enqueuing elements:" << endl;
    queue.print();

    cout << "\nDequeuing the highest priority element..." << endl;
    queue.deQueue();
    queue.print();

    cout << "\nDequeuing another element..." << endl;
    queue.deQueue();
    queue.print();

    cout << "\nFinal state of the priority queue:" << endl;
    queue.print();
    

    return 0;
}
