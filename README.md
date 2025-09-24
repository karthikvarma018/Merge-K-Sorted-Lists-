# Merge-K-Sorted-Lists-
Creating a Merge k Sorted Lists
import heapq

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

    # This is to make ListNode objects comparable for the heap
    def __lt__(self, other):
        return self.val < other.val

def mergeKSortedLists(lists):
    # Edge case: if lists is empty
    if not lists:
        return None
    
    # Initialize a min-heap
    heap = []
    
    # Insert the head of each list into the heap
    for l in lists:
        if l:
            heapq.heappush(heap, l)
    
    # Dummy node to simplify the merging process
    dummy = ListNode()
    current = dummy
    
    # Extract nodes from the heap and build the merged list
    while heap:
        # Pop the smallest element from the heap
        node = heapq.heappop(heap)
        current.next = node
        current = current.next
        
        # If the next node in the list exists, push it to the heap
        if node.next:
            heapq.heappush(heap, node.next)
    
    # Return the merged list starting from the next of the dummy node
    return dummy.next

# Helper function to convert LinkedList to a Python List
def linkedListToList(head):
    result = []
    while head:
        result.append(head.val)
        head = head.next
    return result

# Test case
l1 = ListNode(1, ListNode(4, ListNode(5)))
l2 = ListNode(1, ListNode(3, ListNode(4)))
l3 = ListNode(2, ListNode(6))

lists = [l1, l2, l3]
merged_head = mergeKSortedLists(lists)

# Convert the merged linked list to a Python list
result_list = linkedListToList(merged_head)

# Output the result
print(result_list)

