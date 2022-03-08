from ast import Index
from cgi import test
from os import link


class Linked_List:
    
    class __Node:
        
        def __init__(self, val):
            self.element = val
            self.successor = None
            self.predecessor = None

    def __init__(self):
        self.__header = self.__Node(None)
        self.__trailer = self.__Node(None)
        self.__header.successor = self.__trailer
        self.__trailer.predecessor = self.__header
        self.__size = 0

    def __len__(self):
        return self.__size

    def append_element(self, val):
        new_node = self.__Node(val)
        old_tail = self.__trailer.predecessor

        old_tail.successor = new_node
        new_node.predecessor = old_tail
        new_node.successor = self.__trailer
        self.__trailer.predecessor = new_node

        self.__size += 1

    def insert_element_at(self, val, index):
        # Assuming the head position (not the header node) is indexed 0, add a
        # node containing val at the specified index. If the index is not a
        # valid position within the list, raise an IndexError exception. This
        # method cannot be used to add an item at the tail position.
        if(index < 0 or index >= self.__size ):
                raise IndexError
        new_node = self.__Node(val)
        if index == 0:
            previous = self.__header
        else:
            previous = self.index_pointer(index-1)
        
        following = previous.successor
        new_node.successor = following
        new_node.predecessor = previous
        previous.successor = new_node
        following.predecessor = new_node
        self.__size += 1


    def remove_element_at(self, index):
        # Assuming the head position (not the header node) is indexed 0, remove
        # and return the value stored in the node at the specified index. If the
        # index is invalid, raise an IndexError exception. 
        if(index < 0 or index >= self.__size):
                raise IndexError
        if (index == 0):
            previous = self.__header
        else:
            previous = self.index_pointer(index-1)
        if (index == self.__size-1):
            following =  self.__trailer
        else:
            following = previous.successor.successor
        stored = previous.successor.element
        previous.successor = following
        following.predecessor = previous
        self.__size -= 1
        return(stored)

    def index_pointer(self, index):
        if(index < 0 or index >= self.__size ):
                raise IndexError
        if index >= (self.__size//2):
            answer = self.__trailer.predecessor
            for i in range(self.__size-1, index, -1):
                answer = answer.predecessor
        else:
            answer = self.__header.successor
            for i in range(0,index):
                answer = answer.successor
        return(answer)

    def get_element_at(self, index):
        # Assuming the head position (not the header node) is indexed 0, return
        # the value stored in the node at the specified index, but do not unlink
        # it from the list. If the specified index is invalid, raise an
        # IndexError exception.
            return(self.index_pointer(index).element)


    def rotate_left(self):
        # Rotate the list left one position. Conceptual indices should all
        # decrease by one, except for the head, which should become the tail.
        # For example, if the list is [ 5, 7, 9, -4 ], this method should alter
        # it to [ 7, 9, -4, 5 ]. This method should modify the list in place and
        # must not return a value.
        if self.__size !=0:
            head = self.__header.successor
            self.__header.successor = head.successor
            head.successor.predecessor = self.__header

            tail = self.__trailer.predecessor
            self.__trailer.predecessor = head
            tail.successor = head
        
    def __str__(self):
        # Return a string representation of the list's contents. An empty list
        # should appear as [ ]. A list with one element should appear as [ 5 ].
        # A list with two elements should appear as [ 5, 7 ]. You may assume
        # that the values stored inside of the node objects implement the
        # __str__() method, so you call str(val_object) on them to get their
        # string representations. 
        current = self.__header
        output = '['
        for i in range(self.__size):
            current = current.successor
            output = output + ' ' + str(current.element)
            if (self.__size > 1 and i < self.__size -1):
                output = output + ','
        return output + ' ]'

    def __iter__(self):
        # Initialize a new attribute for walking through your list 
        self.pointer = self.__header
        return self

    def __next__(self):
        # Using the attribute that you initialized in __iter__(), fetch the next
        # value and return it. If there are no more values to fetch, raise a
        # StopIteration exception. 
        if self.pointer.successor is not self.__trailer:
            self.pointer = self.pointer.successor
            return self.pointer.element
        else:
            raise StopIteration

    def __reversed__(self):
        # Construct and return a new Linked_List object whose nodes alias the
        # same objects as the nodes in this list, but in reverse order. For a
        # Linked_List object ll, Python will automatically call this function
        # when it encounters a call to reversed(ll) in an application. If
        # print(ll) displays [ 1, 2, 3, 4, 5 ], then print(reversed(ll)) should
        # display [ 5, 4, 3, 2, 1 ]. This method does not change the state of
        # the object on which it is called. Calling print(ll) again will still
        # display [ 1, 2, 3, 4, 5 ], even after calling reversed(ll). This
        # method must operate in linear time.
        new_linked_list = Linked_List()
        c = 0
        for i in self:
            if c == 0:
                new_linked_list.append_element(i)
                c+=1
            else: 
                new_linked_list.insert_element_at(i,0)
        return (new_linked_list)

if __name__ == '__main__':
    # Your test code should go here. Be sure to look at cases when the list is
    # empty, when it has one element, and when it has several elements. Do the
    # indexed methods raise exceptions when given invalid indices? Do they
    # position items correctly when given valid indices? Does the string
    # representation of your list conform to the specified format? Does removing
    # an element function correctly regardless of that element's location? Does
    # a for loop iterate through your list from head to tail? Does a for loop
    # iterate through your reversed list from tail to head? Your writeup should
    # explain why you chose the test cases. Leave all test cases in your code
    # when submitting.

    #Testing that the linked list class and string function work on a ground level
    tester = Linked_List()
    if str(tester) == '[ ]':
        print('Passed test')

    #APPEND: 
    # empty list
    tester.append_element(1)
    if str(tester) == '[ 1 ]':
        print('Passed test')
    #list with elements
    tester.append_element(2)
    tester.append_element(3)
    if str(tester) == '[ 1, 2, 3 ]' and len(tester) == 3:
        print('Passed test')

    #INSERT, test empty list...
    #tester is current [ 1, 2, 3 ]
    #appending:
    try:
        tester.insert_element_at(4,3)
    except IndexError:
        print('Cannot append with insert_element_at method')
    #out of bounds too large
    try:
        tester.insert_element_at(4,4)
    except IndexError:
        print('Index Out of Bounds')
    #normal case
    tester.insert_element_at(2.5, 2)
    if str(tester) == '[ 1, 2, 2.5, 3 ]':
        print('Passed test')
    #0 elements
    try:
        tester = Linked_List()
        tester.insert_element_at(1,0)
    except IndexError:
        print('Cannot append')

    
    #REMOVE 
    #empty
    try:
        tester = Linked_List()
        tester.remove_element_at(0)
    except IndexError:
        print('Cannot remove from empty list')
    #size one
    tester = Linked_List()
    tester.append_element(1)
    element = tester.remove_element_at(0)
    if ((str(tester) == '[ ]') and element == 1): #element tests the return value (1)
        print('Passed Test')
    #last value
    tester.append_element(1)
    tester.append_element(2)
    tester.remove_element_at(1)
    if (str(tester) == '[ 1 ]'):
        print('Passed Test')


    #LENGTH:
    #none
    tester = Linked_List()
    if not len(tester):     #len(tester) should be 0
        print('Passed Test')
    #normal case
    tester.append_element(1)
    if (len(tester)==1):
        print('Passed Test')

    #GET ELEMENT:
    #none 
    tester = Linked_List()
    try:
        tester.get_element_at(0)
    except IndexError:
        print('No elements to get')

    #normal case
    tester.append_element(1)
    tester.append_element(2)
    tester.append_element(3)
    if tester.get_element_at(2) == 3:
        print('Passed Test')

    #ITER
    # tester = [ 1, 2, 3 ]
    #normal case
    output = ''
    for i in tester:
        output += str(i) + ' '
    if output == '1 2 3 ':
        print('Passed Test')
    #0 size
    tester = Linked_List()
    output = ''
    for i in tester:
        output += str(i) + ' '
    if output == '':
        print('Passed Test')

    #REVERSE
    #empty
    if str(reversed(tester)) == '[ ]':
        print('Passed Test')
    #normal case
    tester.append_element(1)
    tester.append_element(2)
    tester.append_element(3)
    tester.append_element(4)
    if str(reversed(tester)) == '[ 4, 3, 2, 1 ]':
        print('Passed Test')
    #iterating in reverse 
    for i in reversed(tester):
        output += str(i) + ' '
    if output == '4 3 2 1 ':
        print('Passed Test')
