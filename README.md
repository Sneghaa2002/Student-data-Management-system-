# Student-data-Management-system-

class Node:
    def _init_(self, data):
        self.left = None
        self.right = None
        self.data=data
     

    def insert(self, data):
# Compare the new value with the parent node
        if self.data:
            if data[0:7] < self.data[0:7]:
                if self.left is None:
                    self.left = Node(data)
                else:
                    self.left.insert(data)
            elif data[0:7] > self.data[0:7]:
                if self.right is None:
                    self.right = Node(data)
                else:
                    self.right.insert(data)
        else:
            self.data = data
   

# Print the tree
    def PrintTree(self):
        if self.left:
            self.left.PrintTree()
        print( self.data),
        if self.right:
            self.right.PrintTree()

    def search(self,root,key):
    # Base Cases: root is null or key is present at root
        if root is None or root.data[0:7] == key[0:7]:
            return root.data
    # Key is greater than root's key
        elif root.data[0:7] < key[0:7]:
            return self.search(root.right,key)
        elif root.data[0:7] > key[0:7]:
    # Key is smaller than root's key
            return self.search(root.left,key)

    def inorderTraversal(self, root):
        res = []
        if root:
            res = self.inorderTraversal(root.left)
            res.append(root.data)
            res = res + self.inorderTraversal(root.right)
        return res
   
    def PreorderTraversal(self, root):
        res = []
        if root:
            res.append(root.data)
            res = res + self.PreorderTraversal(root.left)
            res = res + self.PreorderTraversal(root.right)
        return res

    def PostorderTraversal(self, root):
        res = []
        if root:
            res = self.PostorderTraversal(root.left)
            res = res + self.PostorderTraversal(root.right)
            res.append(root.data)
        return res
   
    def minValueNode(self,root):
        current = root
        while (current.left is not None):
            current = current.left
        return current

    def deleteNode(self,temp, data):
        if data[0:7] < self.data[0:7]:
            if self.left:
               temp = self
               self.left.deleteNode(temp,data)
            else:
               print("Given node is not present in the tree")
        elif(data[0:7] > self.data[0:7]):
           if self.right:
            temp = self
            self.right.deleteNode(temp, data)  
           else:
               print("Given node is not present in the tree")
        else:
            if (self.left is None and self.right is None):
                if(temp.left == self):
                    temp.left = None
                else:
                    temp.right = None
                self = None
                return temp
       
            elif self.right is None :
                if(temp.left == self):
                    temp.left = self.left
                else:
                    temp.right = self.left
                self = None
                return temp
            elif self.left is None :
                if(temp.left == self):
                    temp.left = self.right
                else:
                    temp.right = self.right
                Node = None
               
            else:
                temp = self.right
                while(temp.left is not None):
                    temp = temp.left
                self.data = temp.data
                self.right.deleteNode(temp,temp.data)
               
r=1
while r!=0:
    #node creation
    print("^^^^^^^^^^^^^^Students Record DataBase^^^^^^^^^^^^^^^")
    print("1. Insert Students Detail")
    print("2. Display Students Details")
    print("3. Delete Students Details")
    print("4. Search Students Details")
    print("5. Exit")
    op = int(input("Enter your Choise : "))
    if op ==1:
        root = Node("2032001  Abi    983566778")
        root.insert("2032002  Arthi  967531899")
        root.insert("2032003  Akil   978762277")
        root.insert("2032004  Bala   872647238")
        root.insert("2032005  Bindhu 945217382")
        n=int(input("enter how many details of student to insert:"))
        for i in range(1,n+1):
          str=input("Enter the Rollno Name PhNo of the student : ")
          root.insert(str)
        print("------------------------------------------------")
        print("Rollno   name        Ph No")
        root.PrintTree()
        print("------------------------------------------------")
    elif op == 2:
        print("Display Options ")
        print("1.Print the sorted Tree")
        print("2.Print inoder Traversal")
        print("3 Print postorder Travesal")
        print("4.Print preorder Traversal")
        ch = int(input("enter your choise : "))
        if ch == 1:
            print("------------------------------------------------")
            print("Rollno   name        marks")
            root.PrintTree()
            print("------------------------------------------------")
        elif ch == 2:
            print(root.inorderTraversal(root))
        elif ch == 3:
            print(root.PostorderTraversal(root))
        elif ch == 4:
            print(root.PreorderTraversal(root))
    elif op == 3:
        print("Deletion in Students record ")
        n=int(input("enter how many details of student to be deleted:"))
        for i in range(1,n+1):
          str=input("enter the Roll No of the student to be deleted:")
          root.deleteNode(root,str)
        print("After deletion Modified Binary tree is :")
        print("------------------------------------------------")
        print("Rollno   name        PhNo")
        root.PrintTree()
        print("------------------------------------------------")
    elif op == 4:
        print("Search Students Detail ")
        str=input("Enter the students roll No : ")
        s=root.search(root,str)
        print("------------------------------------------------")
        print("Rollno   name        PhNo")
        print(s)
        print("------------------------------------------------")
    elif op == 5:
        r=0
