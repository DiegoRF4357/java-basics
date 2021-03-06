
# Implement a List: Solving the problem

An example how to solve a problem from a developer perspective tackling the solution from the input/output to final result enumerating all possible scenarios to develop the code.

---

## Definition of problem (Requirements)
Structure:
* Hold an infinite list of integers.
* Keeping the insertion order: Add 1, then 2: the list should contain [1,2].
* Figured out what number is next of and what is the previous of a given number.
* List all the numbers contained into the list.
* Remove a number from the list: remove only the numbers matching with the one indicated, the result nodes need to discard the removed one.

___

## Defining tasks

It is important to analyze the given information to divide the problem into sub-tasks, we can define the list of task based on the requirements

---

## Defining tasks

#### 1. Create a class: A place to hold the completed list. This can be a class. Let's use _List_ as the name of the class for now.

    * Input: Integers processed asynchronously.
     * Output: List of integers.
 
 #### 2. Add: An entry point to populate elements to the list
 
     * Input: An integer.
     * Output: List will contain the given number at the end of the list.
      
---
 
 ## Defining tasks
 
 #### 3. Remove: An entry point to remove elements from the list
 
     * Input: An integer.
     * Output: List without the given number.
 
 #### 4. Next Of: An entry point to obtain the next number of the given one.
 
     * Input: An integer.
     * Output: The number after the indicated one.
 
---
 
 ## Defining tasks
 
 #### 5. Previous Of: An entry point to obtain the previous number of the given one.
 
     * Input: An integer.
     * Output: The number before the indicated one.
 
---
 
 ### Using UML Class Diagram
 With the information we have until now, we can create a basic class UML diagram. Without attributes only actions defining inputs and outputs
 
 ![UML Diagram](https://drive.google.com/uc?export=view&id=1t7Rr0R9-KdGI4U8myKHKJA2SzzVA-LoZ)
 
---
 
 ### Definition of Priorities
 1. Define structure
 2. Add
 3. Remove
 4. NextOf
 5. PreviousOf
 6. Print
 
---
 
 ### 1. Define structure
 ````java
 interface List{ 
      void add(Integer value);
      void remove(Integer value);
      Integer nextOf(Integer value);
      Integer previousOf(Integer value);
      String print();
 }
 ````
 
---
 
 ### 1. Define structure: Alternatives
 ![List Node Example](https://drive.google.com/uc?export=view&id=1WtZuIjemWR6OgTqlW5p0UpghY7ZAUD8u)
 
---
 
 ### 1. Define structure: Alternatives
 ![List Node Example](https://drive.google.com/uc?export=view&id=1Xkm9VcsHZ95uMnk-GGPA6hHP-j4UZN9K)
 
---
 
 ### 1. Define structure
 ![List Node Example](https://drive.google.com/uc?export=view&id=1KSg3w10dZCNSV2aIYXlcbAeOhSCU6G_e)
 
---
 ### 1. Define structure
 
 ````java
 class Node{
     private Integer value;
     private Node next;
     private Node previous;
     Node(Integer value){this.value=value;}
     //Assuming sets and gets are generated
 }
 ````
 
---

 ![List Node Example](https://drive.google.com/uc?export=view&id=19gJowbyy1Oi3aNH62w1hF1J7x9xV7TIz)
 
---
 
 ### 2. Add
 Tests scenarios
 1. Adding a number when the list is empty.
 2. Adding a number when the list contains a number.
 3. Adding a null number.
 
---
 
 ### 2. Add: Adding a number when the list is empty
 ````java
 class ListImpl{
    private Node first;
     void add(Integer value){
         Node node = new Node(value);
         this.first=node;
     }
 }
 ````
 
---
 
 ### 2. Add: Adding a number when the list contains a number
 
 Redefining method to accomplish the scenarios
 
 ````java
 class ListImpl{
    private Node first;
    private Node last;
     void add(Integer value){
         Node node = new Node(value);
         if(this.last==null){//first scenario
             this.first=node;
             this.last=node;
         }else{//second scenario
            node.setPrevious(this.last);
            this.last.setNext(node);
            this.last = node;
         }
     }
 }
 ````
 
---
 
 ### 2. Add: Adding null number.
 
 Redefining method to accomplish the scenarios
 
 ````java
 class ListImpl{
    private Node first;
    private Node last;
    void add(Integer value){
        if (value == null) return;//third scenario
        Node node = new Node(value);
        if (this.last == null) {//first scenario
            this.first = node;
            this.last = node;
        } else {//second scenario
            node.setPrevious(this.last);
            this.last.setNext(node);
            this.last = node;
        }
     }
 }
 ````
 
---
 
  We need to change original diagram
 
  ![List Node Example](https://drive.google.com/uc?export=view&id=1GV2_OcXiGignEFwMOZwXSqah6V9OXgVi)


---
 
 ### 3. Remove
 Tests scenarios
 1. Remove a node in a middle position.
 3. Remove a node in the last position.
 3. Remove a node in the first position.
 4. Remove a null value.
 5. Remove no existing node.
 
---
 
 ### 3. Remove: Remove node at some middle position.
 ![UML Diagram](https://drive.google.com/uc?export=view&id=1Qmzh8slG4HlmwHwVhPHrmOeM7OC1nEoM)
 
---
 
 ### 3. Remove: Remove node at some middle position.
 
 ````java
 class ListImpl{
     Node first;
     void remove(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
                 current.getNext().setPrevious(current.getPrevious());//first scenario
                 current.getPrevious().setNext(current.getNext());
             }
            current=current.getNext();
         }
 
     }
 }
 ````
 
---
 
 ### 3. Remove: Remove node at the last position.
 ![UML Diagram](https://drive.google.com/uc?export=view&id=1z2F8VTJ-4XSSQZbGAft_-rvcwUs_1Aw9)
 
---
 
 ### 3. Remove: Remove node at the last position.
 
 ````java
 class ListImpl{
     Node first;
     void remove(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)) {
                 if(current.getNext()!=null && current.getPrevious()!=null){
                     current.getNext().setPrevious(current.getPrevious());//first scenario
                     current.getPrevious().setNext(current.getNext());
                 }else if(current.getNext()==null && current.getPrevious()!=null ){//second scenario
                     current.getPrevious().setNext(null);
             
                 }
             }
             current=current.getNext();
        }
 
     }
 }
 ````
 
---
 
 ### 3. Remove: Remove node at the first position.
 ![UML Diagram](https://drive.google.com/uc?export=view&id=10JXD4HKF8MWCveilnk31t1khoHfv6hOj)
 
---
 
 ### 3. Remove: Remove a node in the first position.
 
 ````java
 class ListImpl{
     Node first;
     void remove(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)) {
                 if(current.getNext()!=null && current.getPrevious()!=null){
                     current.getNext().setPrevious(current.getPrevious());//first scenario
                     current.getPrevious().setNext(current.getNext());
                 }else if(current.getNext()==null && current.getPrevious()!=null ){//second scenario
                     current.getPrevious().setNext(null);
                 }else if(current.getNext()!=null && current.getPrevious()==null ){//second scenario
                     current.getNext().setPrevious(null);
                     node=current.getNext();//Move reference for first node
                 }
             }
             current=current.getNext();
        }
 
     }
 }
 ````
 
---
 
 ### 3. Remove: Remove null value.
 
 ````java
 class ListImpl{
     Node first;
     void remove(Integer value){
         if(value==null)return;//fourth scenario
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)) {
                 if(current.getNext()!=null && current.getPrevious()!=null){
                     current.getNext().setPrevious(current.getPrevious());//first scenario
                     current.getPrevious().setNext(current.getNext());
                 }else if(current.getNext()==null && current.getPrevious()!=null ){//second scenario
                     current.getPrevious().setNext(null);
                 }else if(current.getNext()!=null && current.getPrevious()==null ){//third scenario
                     current.getNext().setPrevious(null);
                     node=current.getNext();//Move reference for first node
                 }
             }
             current=current.getNext();
        }
 
     }
 }
 ````
 
---
 
 ### 3. Remove: Remove non-existing node.
 
 Redefining structure to define a scenario
 ````java
 class ListImpl{
     Node first;
     boolean remove(Integer value){
         if(value==null)return;//fourth scenario
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)) {
                 if(current.getNext()!=null && current.getPrevious()!=null){
                     current.getNext().setPrevious(current.getPrevious());//first scenario
                     current.getPrevious().setNext(current.getNext());
                 }else if(current.getNext()==null && current.getPrevious()!=null ){//second scenario
                     current.getPrevious().setNext(null);
                 }else if(current.getNext()!=null && current.getPrevious()==null ){//third scenario
                     current.getNext().setPrevious(null);
                     node=current.getNext();//Move reference for first node
                 }
                 return true;//fifth scenario
             }
             current=current.getNext();
        }
         return false;//fifth scenario
     }
 }
 ````
 
---
 
 ### 3. Remove: Analyze code to identify missing scenarios
 
 Redefining structure to define a scenario
 ````java
 class ListImpl{
     Node first;
     boolean remove(Integer value){
         if(value==null)return false;//fourth scenario
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)) {
                 if(current.getNext()!=null && current.getPrevious()!=null){
                     current.getNext().setPrevious(current.getPrevious());//first scenario
                     current.getPrevious().setNext(current.getNext());
                 }else if(current.getNext()==null && current.getPrevious()!=null ){//second scenario
                     current.getPrevious().setNext(null);
                 }else if(current.getNext()!=null && current.getPrevious()==null ){//third scenario
                     current.getNext().setPrevious(null);
                     node=current.getNext();//Move reference for first node
                 }else{//sixth scenario: list only have one node
                     node=null;
                 }
                 return true;//fifth scenario
             }
            current=current.getNext();
         }
         return false;//fifth scenario
     }
 }
 ````
 
---
 
 ### 4. Next Of
 Tests scenarios
 1. Get nextOf from a middle node.
 2. Get nextOf from the first node.
 3. Get nextOf from the last node.
 4. Get the nextOf from the non-existing node.
 5. Get the nextOf from the null value.
 
---
 
 ### 4. Next of: Get nextOf from a middle node.
 
 ````java
 class ListImpl{
     Node first;
     Integer nextOf(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
                 return current.getNext().getValue();//first scenario
             }
             current=current.getNext();
         }
     return null;
     }
 }
 ````
 
---
 
 ### 4. Next of: Get nextOf from the first node.
 
 Do we need to do some changes to the second scenario?
 ````java
 class ListImpl{
     Node first;
     Integer nextOf(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
                 return current.getNext().getValue();//first and second scenario
             }
             current=current.getNext();
         }
     return null;
     }
 }
 ````
 
---
 
 ### 4. Next of: Get nextOf from the last node.
 
 ````java
 class ListImpl{
     Node first;
     Integer nextOf(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
             //first, second  and third scenario
                 return current.getNext()!=null ? current.getNext().getValue() : null;
             }
             current=current.getNext();
         }
     return null;
     }
 }
 ````
---
 
 ### 4. Next of: Get nextOf from a non-existing node.
 
 ````java
 class ListImpl{
     Node first;
     Integer nextOf(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
             //first, second  and third scenario
                 return current.getNext()!=null ? current.getNext().getValue() : null;
             }
             current=current.getNext();
         }
     return null;//Alternatively we can throw an exception to indicate value not exist into the list
     }
 }
 ````
 
---
 
 ### 4. Next of: Get nextOf from a null value.
 
 ````java
 class ListImpl{
     Node first;
     Integer nextOf(Integer value){
         if(value==null) return null;//fifth scenario: 
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
             //first, second  and third scenario
                 return current.getNext()!=null ? current.getNext().getValue() : null;
             }
             current=current.getNext();
         }
     return null;//Alternatively we can throw an exception to indicate value not exist into the list
     }
 }
 ````
 
---
 
 ### 5. Previous Of
 Tests scenarios
 1. Get previous of the last node.
 1. Get previous of the first node.
 2. Get previous of a middle node.
 4. Get previous of non-existing node.
 5. Get previous of null value.
 
---
 
 ### 5. Previous of: Get previous of middle node.
 
 ````java
 class ListImpl{
     Node first;
     Integer previousOf(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
                 return current.getPrevious().getValue();//first scenario
             }
             current=current.getNext();
         }
     return null;
     }
 }
 ````
 
---
 
 ### 5. Previous of: Get previous of the first node.
 
 Do we need to do some changes to the second scenario?
 ````java
 class ListImpl{
     Node first;
     Integer previousOf(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
                 return current.getPrevious()!=null ? current.getPrevious().getValue() : null;//first and second scenario
             }
             current=current.getNext();
         }
     return null;
     }
 }
 ````
---
 
 ### 5. Previous of: Get previous of the last node.
 
 ````java
 class ListImpl{
     Node first;
     Integer previousOf(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
             //first, second  and third scenario
                 return current.getPrevious()!=null ? current.getPrevious().getValue() : null;
             }
             current=current.getNext();
         }
     return null;
     }
 }
 ````
 
---
 
 ### 5. Previous of: Get previous of non-existing node.
 
 ````java
 class ListImpl{
     Node first;
     Integer previousOf(Integer value){
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
             //first, second  and third scenario
                 return current.getPrevious()!=null ? current.getPrevious().getValue() : null;
             }
             current=current.getNext();
         }
     return null;//Alternatively we can throw an exception to indicate value not exist into the list
     }
 }
 ````
 
---
 
 ### 5. Previous of: Get previous of null value.
 
 ````java
 class ListImpl{
     Node first;
     Integer previousOf(Integer value){
         if(value==null) return null;//fifth scenario 
         Node current=first;
         while(current!=null){
             if(current.getValue().equals(value)){
             //first, second  and third scenario
                 return current.getPrevious()!=null ? current.getPrevious().getValue() : null;
             }
             current=current.getNext();
         }
     return null;//Alternatively we can throw an exception to indicate value not exist into the list
     }
 }
 ````
 
---
 
 ### 6. Print
 Tests scenarios
 1. Build a string when the list has values
 2. Build a string when the list does not has values
 
---
 
 ### 6. Print: Build string when the list has values
 
 ````java
 class ListImpl{
     Node first;
     String print(){
         Node current = first;
         String value = "";
         while (current != null) {
             value += current.getValue() +" ";//first scenario
             current = current.getNext();
         }
         return value;
     }
 }
 ````
 
---
 
 ### 6. Print: Build string when the list does not has values
 
 ````java
 class ListImpl{
     Node node;
     String print(){
         if (first == null) return "";// second scenario
         Node current = first;
         String value = "";
         while (current != null) {
             value += current.getValue() +" ";//first scenario
             current = current.getNext();
         }
         return value;
     }
 }
 ````
 
---
 
 ### 6. Print: Optimizing
 We can fit the code according to the language specification
 ````java
 class ListImpl{
     Node node;
     String toString(){
         if (first == null) return "";// second scenario
         Node current = first;
         String value = "";
         while (current != null) {
             value += current.getValue() +" ";//first scenario
             current = current.getNext();
         }
         return value;
     }
 }
 ````
 
---

### Some interest links

https://www.baeldung.com/java-test-driven-list

---
    