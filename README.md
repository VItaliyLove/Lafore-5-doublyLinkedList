# Lafore-5-doublyLinkedList

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.nio.Buffer;

class Algorithm {

   static class Link {
       int data;
       Link next;
       Link previous;

       public Link (int newData) {
           data = newData;
       }
    }

    static class DoublyLinkList {

       Link first;
       Link last;

       public DoublyLinkList() {
           first = null;
           last = null;
       }

       public boolean isEmpty() {
           return (first == null);
       }

       public void displayForward() {
           Link current = first;
           while(current != null) {
               System.out.print(current.data + " ");
               current = current.next;
           }
           System.out.println();
       }

        public void displayBackward() {
            Link current = last;
            while(current != null) {
                System.out.print(current.data + " ");
                current = current.previous;
            }
            System.out.println();
        }


        public void insertFirst(int data) {
           Link link = new Link(data);
           if (isEmpty()) {
               last = link;
           }
           else {
               first.previous = link;
           }
           link.next = first;
           first = link;
       }

       public void insertLast(int data) {
           Link link = new Link(data);
           if (isEmpty())
               first = link;
           else {
               link.previous = last.next;
               last.next = link;
           }
           last = link;
       }

        public boolean insertAfter(int key, int data) {
           Link current = first;
           while (current.data != key) {
               current = current.next;
               if (current == null)
                   return false;
           }

           Link link = new Link(data);
           if (current == last) {
               last = link;
           }
           else {
               link.next = current.next;
               current.next.previous = link;
           }
           current.next = link;
           link.previous = current;
           return true;
        }

        public Link deleteLast() {
           Link temp = last;
           if (first.next == null)
               first = null;
           else
               last.previous.next = null;
           last = last.previous;
           return temp;
        }

        public Link deleteFirst() {
           Link temp = first;
           if (first.next == null)
               last = null;
           else
               first.next.previous = null;
           first = first.next;
           return temp;
        }

        public Link deleteKey(int key) {

           Link current = first;

           while (current.data != key) {
               current = current.next;
               if (current == null)
                   return null;
           }

           if (current == first)
               first = current.next;
           else
               current.previous.next = current.next;

           if (current == last)
               last = current.previous;
           else
               current.next.previous = current.previous;

           return current;
        }
    }

    public static void main(String[] arg) throws IOException {

       DoublyLinkList doublyLinkList = new DoublyLinkList();
       doublyLinkList.insertFirst(10);
       doublyLinkList.insertFirst(20);
       doublyLinkList.insertLast(5);
       doublyLinkList.insertAfter(5,15);
       doublyLinkList.insertAfter(10,3);
       doublyLinkList.displayForward();
       doublyLinkList.displayBackward();
       doublyLinkList.deleteKey(3);
       doublyLinkList.displayBackward();
       doublyLinkList.deleteKey(20);
       doublyLinkList.displayBackward();
       doublyLinkList.deleteKey(15);
       doublyLinkList.displayBackward();
       doublyLinkList.deleteKey(5);
       doublyLinkList.displayBackward();
       doublyLinkList.deleteKey(10);
       doublyLinkList.displayBackward();

    }
}
