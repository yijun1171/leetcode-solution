**时间**:2015.3.16

**问题描述**:将链表排序,要求使用常数空间,时间复杂度是O(NlgN)

**code**:
```java  

public class SortList extends AbstractList{


    public static ListNode sort(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode mid = partition(head);
        head = sort(head);
        mid = sort(mid);
        return merge(head, mid);
    }

    //返回中间节点
    private static ListNode partition(ListNode head){
        if(head.next == null) return head;
        ListNode fast = head, slow = head, front = head;
        while(fast != null && fast.next != null){
            fast = fast.next.next;
            front = slow;
            slow = slow.next;
        }
        front.next = null;//断开链接
        return slow;
    }

    private static ListNode merge(ListNode headA, ListNode headB){
        assert headA != null && headB != null;
        ListNode result = null;
        ListNode temp = null;
        ListNode head = null;
        while (headA != null && headB != null){
            if(headA.val.compareTo(headB.val) < 0) {
                temp = headA;
                headA = headA.next;
            }
            else {
                temp = headB;
                headB = headB.next;
            }
            if(result != null) {
                result.next = temp;
                result = result.next;
            }
            else {
                result = temp;
                head = result;//记录头指针
            }
        }
        result.next = headA == null ? headB : headA;
        return head;
    }

    public static void main(String[] args){
        ListNode head = make(new Integer[]{12, 2, 5, 33, 40, 1});
        sort(head);
        show(head);
    }
}

```
**思路**:
要求时间复杂度为O(NlgN),并且常数的空间复杂度,最好的方法是归并排序,只需要操作节点的指针,不需要额外的空间.
