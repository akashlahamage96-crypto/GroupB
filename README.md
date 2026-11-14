# GroupB

circular queue

#include <iostream> 
using namespace std; 
#define SIZE 5  // Fixed size of the queue 
 
class CircularQueue { 
    int arr[SIZE]; 
    int front, rear; 
 
public: 
    CircularQueue() { 
        front = -1; 
        rear = -1; 
    } 
 
    // Check if queue is full 
    bool isFull() { 
        return ((front == 0 && rear == SIZE - 1) || (rear + 1 == front)); 
    } 
 
    // Check if queue is empty 
    bool isEmpty() { 
        return (front == -1); 
    } 
 
    // Enqueue operation 
    void enqueue(int value) { 
        if (isFull()) { 
            cout << "Queue is FULL! Cannot insert " << value << endl; 
            return; 
        } 
 
        if (front == -1)  // First element 
            front = 0; 
 
        rear = (rear + 1) % SIZE; // Circular increment 
        arr[rear] = value; 
        cout << "Inserted: " << value << endl; 
    } 
 
    // Dequeue operation 
    void dequeue() { 
        if (isEmpty()) { 
            cout << "Queue is EMPTY! Cannot delete." << endl; 
            return; 
        } 
 
        cout << "Deleted: " << arr[front] << endl; 
 
        if (front == rear) { 
            // Queue has only one element 
            front = -1; 
            rear = -1; 
        } else { 
            front = (front + 1) % SIZE; // Circular increment 
        } 
    } 
 
    // Display queue 
    void display() { 
        if (isEmpty()) { 
            cout << "Queue is EMPTY!" << endl; 
            return; 
        } 
 
        cout << "Queue elements: "; 
        int i = front; 
        while (true) { 
            cout << arr[i] << " "; 
            if (i == rear) 
                break; 
            i = (i + 1) % SIZE; 
        } 
        cout << endl; 
    } 
}; 
 
int main() { 
    CircularQueue q; 
    int choice, value; 
 
    do { 
        cout << "\n--- Circular Queue Menu ---\n"; 
        cout << "1. Enqueue (Insert)\n"; 
        cout << "2. Dequeue (Delete)\n"; 
        cout << "3. Display\n"; 
        cout << "4. Exit\n"; 
        cout << "Enter choice: "; 
        cin >> choice; 
 
        switch (choice) { 
            case 1: 
                cout << "Enter value to insert: "; 
                cin >> value; 
                q.enqueue(value); 
                break; 
            case 2: 
                q.dequeue(); 
                break; 
            case 3: 
                q.display(); 
                break; 
            case 4: 
                cout << "Exiting program..." << endl; 
                break; 
            default: 
                cout << "Invalid choice! Try again." << endl; 
        } 
    } while (choice != 4); 
 
    return 0; 
} 


 program2: Binary search tree


 class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
class BST:
    def __init__(self):
        self.root = None
    # Insert (Duplicate not allowed)
    def insert(self, root, key):
        if root is None:
            return Node(key)
        if key < root.data:
            root.left = self.insert(root.left, key)
        elif key > root.data:
            root.right = self.insert(root.right, key)
        else:
            print("Duplicate Entry Not Allowed :", key)
        return root
    # Search
    def search(self, root, key):
        if root is None:
            return False
        if root.data == key:
            return True
        if key < root.data:
            return self.search(root.left, key)
        return self.search(root.right, key)
    # Find minimum value node
    def minValue(self, root):
        while root.left:
            root = root.left
        return root
    # Delete
    def delete(self, root, key):
        if root is None:
            return root
        if key < root.data:
            root.left = self.delete(root.left, key)
        elif key > root.data:
            root.right = self.delete(root.right, key)
        else:
            if root.left is None:
                return root.right
            if root.right is None:
                return root.left
            temp = self.minValue(root.right)
            root.data = temp.data
            root.right = self.delete(root.right, temp.data)
        return root
    # Inorder Traversal
    def inorder(self, root):
        if root:
            self.inorder(root.left)
            print(root.data, end=" ")
            self.inorder(root.right)
    # Depth of Tree
    def depth(self, root):
        if root is None:
            return 0
        return 1 + max(self.depth(root.left),
                       self.depth(root.right))
    # Mirror Image
    def mirror(self, root):
        if root:
            root.left, root.right = root.right, root.left
            self.mirror(root.left)
            self.mirror(root.right)
    # Copy Tree
    def copyTree(self, root):
        if root is None:
            return None
        newNode = Node(root.data)
        newNode.left = self.copyTree(root.left)
        newNode.right = self.copyTree(root.right)
        return newNode
    # Parent with Child Nodes
    def parentChild(self, root):
        if root:
            if root.left or root.right:
                print("Parent:", root.data, end=" -> ")
                if root.left:
                    print("Left:", root.left.data, end=" ")
                if root.right:
                    print("Right:", root.right.data, end=" ")
                print()
            self.parentChild(root.left)
            self.parentChild(root.right)
    # Leaf Nodes
    def leafNodes(self, root):
        if root:
            if root.left is None and root.right is None:
                print(root.data, end=" ")
            self.leafNodes(root.left)
            self.leafNodes(root.right)
    # Level Wise Display
    def levelWise(self):
        if self.root is None:
            return
        q = [self.root]
        while q:
            node = q.pop(0)
            print(node.data, end=" ")
            if node.left:
                q.append(node.left)
            if node.right:
                q.append(node.right)


program3:Heap sort


def heapify(arr, n, i): 

  """Ensures the subtree rooted at index i is a max-heap.""" 
  largest = i 
  left = 2 * i + 1     # left child index 
  right = 2 * i + 2    # right child index 
  
  # Check if left child exists and is greater than root 
  if left < n and arr[left] > arr[largest]: 
     largest = left 
   
  # Check if right child exists and is greater than current largest 
  if right < n and arr[right] > arr[largest]: 
     largest = right 
   
  # If largest is not the root, swap and continue heapifying 
  if largest != i: 
     arr[i], arr[largest] = arr[largest], arr[i] 
     heapify(arr, n, largest) 
     
def heap_sort(arr): 
  n = len(arr) 
  # Build max-heap 
  for i in range(n // 2 - 1, -1, -1): 
    heapify(arr, n, i) 
  print("\nMax Heap constructed:", arr) 
  # Extract elements from heap one by one 
  for i in range(n - 1, 0, -1): 
     # Swap root (largest) with the last element 
     arr[0], arr[i] = arr[i], arr[0] 
     # Heapify the reduced heap 
     heapify(arr, i, 0) 
     print(f"Heap after removing element {n-i}:", arr) 
def main(): 
  while True: 
    print("\n--- Heap Sort Menu ---") 
    print("1. Enter array") 
    print("2. Perform Heap Sort") 
    print("3. Exit") 
    choice = input("Enter choice: ") 
    if choice == "1": 
        global arr 
        arr = list(map(int, input("Enter integers separated by space: ").split())) 
    elif choice == "2": 
       if not arr: 
          print("Array is empty! Please enter array first.") 
       else: 
          print("\nOriginal Array:", arr) 
          heap_sort(arr) 
          print("\nSorted Array (Ascending):", arr) 
   elif choice == "3": 
       print("Exiting program...") 
       break 
   else: 
      print("Invalid choice! Please try again.") 
      
if __name__ == "__main__": 
   arr = [] 
   main()


program4:merge sort



def merge(arr, left, mid, right): 
  """Merge two sorted halves of arr.""" 
  # Create temporary subarrays 
  L = arr[left:mid+1] 
  R = arr[mid+1:right+1] 
  i = j = 0 
  k = left 
  # Merge while comparing delivery times 
  while i < len(L) and j < len(R): 
    if L[i][1] <= R[j][1]:  # Compare delivery times 
       arr[k] = L[i] 
       i += 1 
    else: 
       arr[k] = R[j] 
       j += 1 
     k += 1 
 # Copy remaining elements 
 while i < len(L): 
   arr[k] = L[i] 
   i += 1 
   k += 1 
 while j < len(R): 
  arr[k] = R[j] 
   j += 1 
   k += 1 
   
def merge_sort(arr, left, right): 
  """Recursive merge sort."""  
  if left < right: 
     mid = (left + right) // 2 
     merge_sort(arr, left, mid) 
     merge_sort(arr, mid+1, right) 
     merge(arr, left, mid, right) 
     
def display_orders(orders): 
  """Pretty print the orders.""" 
  print("\nOrders:") 
  print("{:<5} {:<20} {:<15}".format("ID", "Item", "Delivery Time (min)")) 
  for order in orders: 
     print("{:<5} {:<20} {:<15}".format(order[0], order[1], order[2])) 
def main(): 
  orders = [] 
  while True: 
    print("\n--- Online Orders Merge Sort Menu ---") 
    print("1. Add Order") 
    print("2. Display Orders") 
    print("3. Sort Orders by Delivery Time") 
    print("4. Exit") 
    choice = input("Enter choice: ") 
    if choice == "1": 
        order_id = input("Enter Order ID: ") 
        item_name = input("Enter Item Name: ") 
        delivery_time = int(input("Enter Delivery Time (in minutes): ")) 
        orders.append((order_id, item_name, delivery_time)) 
    elif choice == "2": 
       if orders: 
           display_orders(orders) 
       else: 
           print("No orders available!") 
    elif choice == "3": 
       if orders: 
           merge_sort(orders, 0, len(orders)-1) 
           print("\nOrders sorted by delivery time:") 
           display_orders(orders) 
       else: 
           print("No orders to sort!") 
   elif choice == "4": 
      print("Exiting program...") 
      break 
   else: 
      print("Invalid choice! Please try again.") 

      
if __name__ == "__main__": 
  main() 



program5: fractional knapsack strategy


def fractional_knapsack(weights, profits, capacity): 
ratio = [(profits[i] / weights[i], weights[i], profits[i]) for i in range(len(weights))] 
ratio.sort(reverse=True, key=lambda x: x[0]) 
total_profit = 0 
selected_items = [] 
for r, w, p in ratio: 
if capacity <= 0: 
break 
if w <= capacity: 
capacity -= w 
total_profit += p 
selected_items.append((w, p, 1.0)) 
else: 
fraction = capacity / w 
total_profit += p * fraction 
selected_items.append((w, p, fraction)) 
capacity = 0 
return total_profit, selected_items 
def input_data(): 
n = int(input("Enter number of parcels: ")) 
weights = [] 
profits = [] 
for i in range(n): 
w = float(input(f"Enter weight of parcel {i+1}: ")) 
p = float(input(f"Enter profit of parcel {i+1}: ")) 
weights.append(w) 
profits.append(p) 
capacity = float(input("Enter truck capacity: ")) 
return weights, profits, capacity 
def display_result(selected, max_profit): 
print("\nSelected parcels:") 
for w, p, frac in selected: 
print(f"Weight: {w}, Profit: {p}, Taken: {frac*100:.2f}%") 
print(f"\nMaximum Profit: {max_profit:.2f}\n") 
# Main menu loop 
while True: 
print("\n=== Fractional Knapsack Menu ===") 
print("1. Enter Data and Calculate") 
print("2. Exit") 
choice = input("Enter choice: ") 
if choice == "1": 
weights, profits, capacity = input_data() 
max_profit, selected = fractional_knapsack(weights, profits, capacity) 
display_result(selected, max_profit) 
elif choice == "2": 
print("Exiting... Goodbye!") 
break 
else: 
print("Invalid choice. Try again.") 









program3: Heap sort algorithm

