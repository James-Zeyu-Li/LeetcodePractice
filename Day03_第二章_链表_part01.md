### Problem 1: [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/)
- Delete node it's not complex, point previous node's next to current node's next node.
- 3 problems to be considered on:
	- the correct position to move pointers. 
	- consider the possibility of delete the head node. 
	- delete dummy and temp node to prevent memory leak.
- Create a Dummy ListNode which means don't need to handle the headNode deletion separately. 

```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {

        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* curr = dummy; // a pointer points to the head

        while( curr-> next != NULL){
            if ( curr->next->val == val){
                ListNode* temp = curr->next;
                curr->next = curr->next->next;
                delete temp;
            } else {
                curr = curr->next;
            }
        }

        head = dummy->next; //retrive the linkedlist
        delete dummy;
        return head;

    }
};
```

### Problem 2: [707. Design Linked List](https://leetcode.com/problems/design-linked-list/)
- Create a Linked List from 0
- The structure of c++ likedList creation is important. 
- Mind the boundary.
```
MyLinkedList() {
    _dummyHead = new ListNode(0); // 创建虚拟头节点
    _size = 0;                   // 初始化链表长度为0
}

private:
	ListNode* _dummyHead;
	int _size;
```
- `deleteAtIndex`: be careful on the usage of tmp node. 
	- If only delete, the pointer still exists and hanging
	- set to null pointer to completely reset.
```cpp
class MyLinkedList {

public:

    struct ListNode{
        int val;
        ListNode* next;
        ListNode(int val): val(val), next(nullptr){}
    };

    MyLinkedList() {
        _dummyHead = new ListNode(0); // dummy node at 0 place
        _size = 0;
    }
    
    int get(int index) {
        if (index > _size - 1 || index < 0){
            return -1;
        }

        ListNode* curr = _dummyHead -> next;
        for (int i = 0; i < index; i++) {
            curr = curr->next;
        }
        return curr->val;
    }
    
    void addAtHead(int val) {
        ListNode* newNode = new ListNode(val);
        newNode->next = _dummyHead -> next;
        _dummyHead -> next = newNode;
        _size++;
    }
    
    void addAtTail(int val) {
        ListNode* newNode = new ListNode(val);
        ListNode* curr =  _dummyHead;
        while (curr->next != nullptr){
            curr = curr->next;
        }

        curr->next = newNode;
        _size++;
    }
    
    void addAtIndex(int index, int val) {
        if(index > _size) return;
        if(index < 0) index = 0;
        ListNode* newNode = new ListNode(val);
        ListNode* curr =  _dummyHead;

        while(index--){
            curr = curr->next;
        }

        newNode -> next = curr->next;
        curr->next = newNode;
        _size++;
    }
    
    void deleteAtIndex(int index) {
        if(index >= _size || index < 0) return;
        ListNode* curr = _dummyHead;
        while(index--) {
            curr = curr ->next;
        }
        ListNode* tmp = curr->next;
        curr->next = curr->next->next;

        delete tmp;
        tmp = nullptr;
        _size--;
    }

    private:
        ListNode* _dummyHead;
        int _size;

};
```


### Problem 3: [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
- To avoid create a new linked list 2 pointers is the best way to proceed
- `prev` point to the place previous of head and the value is null
- `curr` point to the head node and change the pointer to the previous node. 
- **`temp`: this is important since after moving the pointers and the connection, the pointer won't be able to move to the next position.**
- **Note**:  
	- a dummy node at the beginning of ListNode won't help with this problem since after reverse there will be an extra dummy node. Since the last node points to null it's the correct construction, NULL it's the best choice.

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
       ListNode* temp;
       ListNode* curr = head;
       ListNode* prev = NULL;

       while(curr != NULL){
            temp = curr->next;
            curr->next = prev;
            prev = curr;
            curr = temp;
       }
       return prev;
    }
};
```