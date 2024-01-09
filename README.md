#include<iostream>
using namespace std;
//Data Structure:
struct node {
	int data;
	node* next;
};
class linked_list {
	node* head;

	//===============
	node* create_node() {
		node* p = new node;
		return p;
	}
	void free_node(node* p) {
		delete(p);
	}
	//===============
public:
	linked_list() {
		head = NULL;
	}

	void add_last(int value) {
		node* add = new node;
		add->next = NULL;
		add->data = value;
		if (head == NULL) {
			head = add;
		}
		else {
			node* last = head;
			while (last->next != NULL)
			{
				last = last->next;
			}
			last->next = add;
		}
	}
	void add_first(int value) {
		node* first = new node;
		first->data = value;
		first->next = head;
		head = first;
	}
	void display() {
		if (head == NULL) {
			cout << "List is empty";
			return;
		}
		node* display = head;
		while (display != NULL)
		{
			cout << display->data << ' ';
			display = display->next;
		}
		cout << endl;
	}
	int pop_front() {
		if (head == NULL) {
			cout << "\nUnderflow\n";
			exit(-1);
		}
		node* pop = head;
		head = pop->next;
		int temp = pop->data;
		delete(pop);
		return temp;
	}
	int pop_back() {
		node* pop = head;
		int temp;
		if (head == NULL) {
			cout << "\nUnderflow\n";
			exit(-1);
		}
		if (pop->next == NULL) {
			head = NULL;
			temp = pop->data;
			delete (pop);
			return temp;
		}
		else {
			while (pop->next->next != NULL)
			{
				pop = pop->next;
			}
			int temp = pop->next->data;
			delete(pop->next);
			pop->next = NULL;
			return temp;
		}

	}
	void reverse() {
		if (head == NULL) {
			cout << "enpty";
			return;
		}
		node* current = head;
		node* next = NULL;
		node* prev = NULL;
		while (current != NULL) {
			next = current->next;
			current->next = prev;
			prev = current;
			current = next;
		}
		head = prev;
	}

	void add_after(int value, int pos) {

		if (head == NULL) {
			cout << "list is empty\n";
		}
		else if (pos == 0) {
			add_first(value);
		}
		else {
			node* nu = new node;
			nu->data = value;
			node* inser = head;
			for (int i = 0; i < pos - 1; i++)
			{
				if (inser == NULL) {
					cout << "There are less than " << pos << " elemnt in linked list" << endl;
					return;
				}
				inser = inser->next;
			}
			nu->next = inser->next;
			inser->next = nu;
		}
	}
	void delete_node(int value) {
		if (head == NULL) {
			cout << "Node is Empty\n";
			return;
		}
		node* previous = head;
		node* current = head;
		if (current->data == value) {
			head = current->next;
			free_node(current);
		}
		else {
			while (current->data != value)
			{
				if (current->next == NULL) {
					cout << "This Node value Dosen't Exist in the Linked_List!\n";
					return;
				}
				previous = current;
				current = current->next;
			}
			previous->next = current->next;
			free_node(current);
		}
	}
	int count() {
		node* p = head;
		int c = 0;
		while (p != NULL)
		{
			c++;
			p = p->next;
		}
		free_node(p);
		return c;
	}
	int search(int value) {
		if (head == NULL) {
			cout << "List is Empty!\n";
			exit(-1);
		}
		node* Find = head;
		int index = 0;
		while (Find != NULL)
		{
			if (Find->data == value) {
				return index;
			}
			index++;
			Find = Find->next;
		}
		cout << "Elemnt dosenot exist";
		exit(-1);
	}
};


class stack {
	int top;
	int* items;
	int size;
public:
	stack() {
		cout << "Enter stack size:";
		cin >> size;
		top = -1;
		items = new int[size];
	}
	bool is_empty() {
		if (top == -1)return 1;
		return 0;
	}
	bool is_full() {
		if (top == size - 1)return 1;
		return 0;
	}
	void push(int item) {
		if (is_full()) {
			cout << "\nOverflow\n";
			return;
		}
		top++;
		items[top] = item;
	}
	int pop() {
		if (is_empty()) {
			cout << "Underflow\n";
			exit(-1);
		}
		int temp = items[top];
		top--;
		return temp;
	}
	void display() {
		for (int i = 0; i <= top; i++)
		{
			cout << items[i] << ' ';
		}
		cout << endl;
	}
};


class queue {
	int front, rear;
	int MAX_SIZE;
	int* elements;
public:
	queue() {
		front = rear = -1;
		cout << "Enter Queue Size:";
		cin >> MAX_SIZE;
		elements = new int[MAX_SIZE];
	}
	bool is_empty() {
		if (front == -1)return 1;
		return 0;
	}
	bool is_full() {
		if (rear == MAX_SIZE - 1)return 1;
		return 0;
	}
	void push(int elemnt) {
		if (is_full()) {
			cout << "\nOver flow\n";
			return;
		}
		if (is_empty()) {
			front = 0;
		}
		rear++;
		elements[rear] = elemnt;
	}
	int pop() {
		if (is_empty()) {
			cout << "\nUnderflow\n";
			exit(-1);
		}
		int temp = elements[rear];
		if (rear == front) {
			rear = front = -1;
		}
		else {
			front++;
		}
		return temp;
	}
	void display() {
		for (int i = front; i <= rear; i++)
		{
			cout << elements[i] << ' ';
		}
		cout << '\n';
	}
};


class circular_queue {
	int front, rear;
	int* items;
	int size;

public:

	circular_queue() {
		cout << "Enter CQueue size:";
		cin >> size;
		front = rear = -1;
		items = new int[size];
	}
	bool is_empty() {
		if (front == -1 && front == -1)return 1;
		return 0;
	}
	bool is_full() {
		if (rear + 1 == front || (front == 0 && rear == size - 1))return 1;
		return 0;
	}
	void push(int item) {
		if (is_full()) {
			cout << "Overflow\n";
			return;
		}
		if (is_empty()) {
			front = 0;
		}
		rear = (rear + 1) % size;
		items[rear] = item;
	}
	int pop() {
		if (is_empty()) {
			cout << "Under flow\n";
			exit(-1);
		}
		int temp = items[front];
		if (front == rear) {
			front = rear = -1;
		}
		else front = (front + 1) % size;
		return temp;
	}
	void display() {
		if (rear >= front) {
			for (int i = front; i <= rear; i++)
			{
				cout << items[i] << ' ';
			}
		}
		else {
			for (int i = front; i < size; i++)
			{
				cout << items[i] << ' ';
			}
			for (int i = 0; i <= rear; i++)
			{
				cout << items[i] << ' ';
			}
		}
		cout << endl;
	}
};


class deque {
	int front, rear;
	int size;
	int* items;
public:
	deque() {
		front = rear = -1;
		cout << "Enter Deque Size:";
		cin >> size;
		items = new int[size];
	}
	bool is_full() {
		if ((front == 0 && rear == size - 1) || rear + 1 == front)return 1;
		return 0;
	}
	bool is_empty() {
		if (front == -1 && rear == -1)return 1;
		return 0;
	}
	void insert_rear(int val) {
		if (is_full()) {
			cout << "Deque Overflow\n";
			return;
		}
		else if (is_empty()) {
			front = rear = 0;
		}
		else rear = (rear + 1) % size;

		items[rear] = val;
	}
	void insert_front(int val) {
		if (is_full()) {
			cout << "Deque Overflow\n";
			return;
		}
		else if (is_empty()) {
			front = rear = 0;
		}
		else if (front == 0) {
			front = size - 1;
		}
		else front = front - 1;

		items[front] = val;
	}
	int remove_rear() {
		if (is_empty()) {
			cout << "Deque Underflow\n";
			exit(-1);
		}
		int temp = items[rear];
		if (front == rear) {
			rear = front = -1;
		}
		else if (rear == 0)rear = size - 1;
		else rear--;
		return temp;
	}
	int removo_front() {
		if (is_empty()) {
			cout << "Deque Underflow\n";
			exit(-1);
		}
		int temp = items[front];
		if (front == rear) {
			rear = front = -1;
		}
		else front = (front + 1) % size;
		return temp;
	}
	void print() {
		if (is_empty()) {
			cout << "Deque is Empty\n";
			return;
		}
		cout << "Deque Elements:\n";
		if (front <= rear) {
			for (int i = front; i <= rear; i++)
			{
				cout << items[i] << ' ';
			}
			cout << endl;
		}
		else {
			//elemnt from front to end 
			for (int i = front; i < size; i++)
			{
				cout << items[i] << ' ';
			}
			//elemnts from 0 to rear
			for (int i = 0; i <= rear; i++)
			{
				cout << items[i] << ' ';
			}
			cout << endl;
		}
	}

};



//Data Structure using Linked List:
//LL for linked list...

class LL_stack {
	linked_list STACK;
public:
	void push(int value) {
		STACK.add_last(value);
	}
	int pop() {
		int temp = STACK.pop_back();
		return temp;
	}
	void display() {
		STACK.display();
	}
};


class LL_queue {
	linked_list QUEUE;
public:
	void push(int value) {
		QUEUE.add_last(value);
	}
	int pop() {
		int temp = QUEUE.pop_front();
		return temp;
	}
	void display() {
		QUEUE.display();
	}
};


class LL_deque {
	linked_list DEQUE;
public:
	void push_back(int value) {
		DEQUE.add_last(value);
	}
	void push_front(int value) {
		DEQUE.add_first(value);
	}
	int pop_front() {
		return DEQUE.pop_front();
	}
	int pop_back() {
		return DEQUE.pop_back();
	}
	void display() {
		DEQUE.display();
	}

};


//Recursionnnnnnn:

void recersion_defenition(int n) {
	if (n == 0) {
		cout << "This is base case\n";
		return;
	}
	cout << "Returtning to Function Again(recusive)\n";
	return recersion_defenition(n - 1);
	//"n-1" the update
	// you have to update the n to go forwoard to base case
	//if you dont update it then it will be infinite loop or recusive function
}

int factorial(int n) {
	if (n == 0 || n == 1)return 1;
	return n * factorial(n - 1);
}
int Power(int n, int p) {
	if (p == 0)return 1;
	return n * Power(n, p - 1);
}
void print_triangle(int x) {
	if (x <= 0)return;

	for (int i = 0; i < x; i++)
		cout << "*";

	cout << endl;
	print_triangle(x - 1);
}
int sum_arr(int arr[], int size, int i = 0) {
	if (i >= size)return 0;
	int S = 0;
	S += arr[i] + sum_arr(arr, size, i + 1);
	return S;

}
void hanoi(int n, char from, char to, char temp) {
	//n is number of disks
	if (n == 0) {
		return;
	}
	hanoi(n - 1, from, temp, to);
	cout << "Move " << n << " from " << from << " to " << to << endl;
	hanoi(n - 1, temp, to, from);
}


int main() {

	return 0;
}
