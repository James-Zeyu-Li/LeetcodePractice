### Problem 1: [24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)
- *First Idea:* 
	- dummy->1->2->3->4
	- **Set Pointers**
		- prev = dummy
		- curr = head
		- nextNode = curr->next
	- **Swap**
		- curr->next = nextNode->next
		- nextNode->next = curr
		- prev->next = nextNode
	- **after Swap**
		- dummy->2 nextNode->1 curr->3->4
	- **Next Step**
		- prev = curr
		- curr= curr->next
		- nextNode = curr->next
- Note: the position of `nextNode = curr->next;` is important.
	- if nextNode if positioned out of the while loop, nextNode could be null.
```cpp
		 ListNode* prev = dummy;
        ListNode* curr = head;
        ListNode* nextNode = curr->next; //this could be null

        while(curr && curr->next){
            curr->next = nextNode ->next;
            nextNode ->next = curr;
            prev ->next = nextNode;

            prev = curr;
            curr = curr->next;
            nextNode = curr->next;
        }
```
- **Correct Version:**
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;

        ListNode* prev = dummy;
        ListNode* curr = head;

        while(curr && curr->next){
            ListNode* nextNode = curr->next;
            curr->next = nextNode ->next;
            nextNode ->next = curr;
            prev ->next = nextNode;

            prev = curr;
            curr = curr->next;
        }
        return dummy->next;
    }
};
```

### Problem 2: [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
- *First Idea*
	- After checking if the linkedList is not empty
	- since delete the nth Node from end, we need to locate the position
		- find the length which means O(n).
- Fast and Slow pointers.
	- delete the node after slow pointer
- **Why Do we need to move to and extra Next?**
	- If move n step, slow pointer needs to be at the nth position's previous position.
	- Need to check if fast->next exists to proceed.
```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;

        ListNode* fast = dummy;
        ListNode* slow = dummy; 

        while(n-- && fast != NULL) {
            fast = fast->next;
        }

        while (fast->next){
            fast = fast->next;
            slow = slow->next;
        }

        slow->next = slow->next->next;
        return dummy->next;

    }
};
```

### Problem 3: [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)
- The correct position depends on the number of nodes after the intersection. How to determine the position...
- Get the position of LinkedList A
- Get the nodes count of LinkedList B
- find the difference between the 2 lists, start from the position of the same remain length(length of the shorted linkedlist)
- find the position node by node, same position same value, currest spot.



### Problem 4: [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)
- I have had no idea how to find the entrance.
- After finding out how they met, using the two pointers again to move at the same speed to find the entrance it's smart.
```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while(fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                ListNode* index1 = fast;
                ListNode* index2 = head;
                while (index1 != index2) {
                    index1 = index1->next;
                    index2 = index2->next;
                }
                return index2;
        }
        return NULL;
    }
};
```
