#  Doubly Linked List Implementation

    class Node:
      def __init__(self, data):
          self.data = data
          self.prev = None
          self.next = None

    class DoublyLinkedList:
      def __init__(self):
          self.head = None

      def insert_at_beginning(self, data):
          new_node = Node(data)
          if self.head is None:
              self.head = new_node
          else:
              new_node.next = self.head
              self.head.prev = new_node
              self.head = new_node
  
      def insert_at_end(self, data):
          new_node = Node(data)
          if self.head is None:
              self.head = new_node
          else:
              last = self.head
              while last.next:
                  last = last.next
              last.next = new_node
              new_node.prev = last
  
      def insert_at_position(self, data, pos):
          new_node = Node(data)
          if pos == 1:
              self.insert_at_beginning(data)
          else:
              temp = self.head
              for _ in range(pos - 2):
                  if temp is None:
                      return
                  temp = temp.next
              if temp is None:
                  return
              new_node.next = temp.next
              if temp.next is not None:
                  temp.next.prev = new_node
              temp.next = new_node
              new_node.prev = temp
  
      def delete_from_beginning(self):
          if self.head is None:
              return
          if self.head.next is None:
              self.head = None
          else:
              self.head = self.head.next
              self.head.prev = None
  
      def delete_from_end(self):
          if self.head is None:
              return
          if self.head.next is None:
              self.head = None
          else:
              last = self.head
              while last.next:
                  last = last.next
              last.prev.next = None
  
      def delete_from_position(self, pos):
          if self.head is None:
              return
          if pos == 1:
              self.delete_from_beginning()
          else:
              temp = self.head
              for _ in range(pos - 2):
                  if temp is None:
                      return
                  temp = temp.next
              if temp is None or temp.next is None:
                  return
              if temp.next.next is not None:
                  temp.next.next.prev = temp
              temp.next = temp.next.next
  
      def traverse_forward(self):
          temp = self.head
          while temp:
              print(temp.data, end=" <-> ")
              temp = temp.next
          print("None")
  
      def traverse_backward(self):
          temp = self.head
          if temp is None:
              return
          while temp.next:
              temp = temp.next
          while temp:
              print(temp.data, end=" <-> ")
              temp = temp.prev
          print("None")
