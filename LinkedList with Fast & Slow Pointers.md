# LinkedList with Fast & Slow Pointers

## [Rotate List](https://leetcode.com/problems/rotate-list/)

This problem is not tricky. A quick think leads us to use `fast & slow pointers`.

**1.fast & slow pointers**

```java
	public ListNode rotateRight(ListNode head, int k) {
        if(head==null)  return null;
        ListNode fast=head,slow=head;
        int size=1;//since we are already at head node
        while(fast.next!=null){
            fast=fast.next;
            size++;
        }
        for(int i=0;i<size-k%size-1;i++)
            slow=slow.next;
        fast.next=head;
        head=slow.next;
        slow.next=null;
        return head;
	}
```

**2.one pointer + circle the list**

Since there is no benefit(it doesn't reduce the pointer move operations) to use 2 pointers. The [highest voted solution](https://discuss.leetcode.com/topic/14470/my-clean-c-code-quite-standard-find-tail-and-reconnect-the-list) in leetcode suggested another method to solve this problem with only one pointer. 

First iterate through the whole list and find the `size` and `tail`. Then, we **CIRCLE** the list.. Thus we can find the newhead with only the 'tail' pointer.

```java
	public ListNode rotateRight(ListNode head, int k) {
        if(head==null)  return null;
        ListNode tail=head;
        int size=1;
        while(tail.next!=null){
            size++;
            tail=tail.next;
        }
        tail.next=head; //circle the list
        
        if((k%=size)!=0)
            for(int i=0;i<size-k;i++)
                tail=tail.next;
        head=tail.next;
        tail.next=null;
        return head;
    }
```
*TIP: the circle step is really clever!*

From above we can see, using two pointer is not really necessary (but OK) for this problem.
