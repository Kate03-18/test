ქლასრუმი:
1.
import java.util.Arrays;


public class Main {
   public static void main(String[] args) {
       int n = 1;
       int m = 1000;
       int[] result = findPalindromeSquares(n, m);
       System.out.println(Arrays.toString(result));
   }




   public static boolean isPalindrome(int num) {
       String strNum = Integer.toString(num);
       return strNum.contentEquals(new StringBuilder(strNum).reverse());
   }


   public static int[] findPalindromeSquares(int n, int m) {
       int[] palindromes = new int[0];
       for (int num = n; num <= m; num++) {
           if (isPalindrome(num)) {
               int square = num * num;
               if (isPalindrome(square)) {
                   int[] arrNew = Arrays.copyOf(palindromes, palindromes.length + 1);


                   arrNew[palindromes.length]= num;


                   palindromes = arrNew;
               }
           }
       }
       return palindromes;
   }


}

2.


public class Main {
   public static void main(String[] args) {
       Point point = new Point(2, 3);
       Point point2 = new Point(5, 3);
       System.out.println(point);
       System.out.println(point.equals(point2));
       System.out.println(point.hashCode());
   }
}
public class Point {
   private int x;
   private int y;
   public Point(int x, int y){
       this.x = x;
       this.y = y;
   }


   public int getX() {
       return x;
   }


   public int getY() {
       return y;
   }


   public void setX(int x) {
       this.x = x;
   }


   public void setY(int y) {
       this.y = y;
   }


}

3.
import java.util.Arrays;


public class Main {
   public static void main(String[] args) {
       System.out.println(Arrays.toString(simpleDividers(88)));
   }


   public static int[] simpleDividers(int n){
       int[] m = new int[0];
       for (int i = 1; i <= n; i++) {
           boolean b = true;
           for (int j = 2; j < i ; j++) {
               if(i % j == 0){
                   b = false;
               }
           }
           if(b){
               if(n % i == 0){
                   int[] arrNew = Arrays.copyOf(m, m.length + 1);
                   arrNew[m.length]= i;
                   m = arrNew;
               }
           }
       }
       return m;
   }
}

ფურცელი:
1.
public class Main {
   public static void main(String[] args) {
       int[] l = new int[] {1, 4, 6, 8, 6};
       System.out.println(oddSum(l));
   }


   public static int oddSum(int[] n){
       int sum = 0;
       int len = 0;
       for (int i = 1; i < n.length; i = i + 2) {
           sum += n[i];
           len++;
       }
       return sum/len;
   }
}

2.
public class Main {
   public static void main(String[] args) {
       int[] l = new int[] {3, 4, 6, 8, 6};
       System.out.println(oddSum(l));
   }
   public static int oddSum(int[] n){
       int max = n[0];
       int min = n[0];
       for (int i = 1; i < n.length; i++) {
           if(max < n[i]){
               max = n[i];
           }
           if(min>n[i]){
               min = n[i];
           }
       }
       return max-min;
   }
}

3.
import org.w3c.dom.*;
import org.xml.sax.SAXException;


import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.parsers.ParserConfigurationException;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerException;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
import java.io.File;
import java.io.IOException;


public class XMLUtils {


   public static void createXML() throws ParserConfigurationException, TransformerException {


       DocumentBuilderFactory documentBuilderFactory = DocumentBuilderFactory.newInstance();
       DocumentBuilder documentBuilder = documentBuilderFactory.newDocumentBuilder();
       Document document = documentBuilder.newDocument();


       Element rootEelement = document.createElement("files");
       document.appendChild(rootEelement);


       Element flyElement = document.createElement("fly");
       Attr attr = document.createAttribute("id");
       attr.setValue("1");
       flyElement.setAttributeNode(attr);


       Element fromElement = document.createElement("from");
       Element toElement = document.createElement("to");


       fromElement.appendChild(document.createTextNode("TBILISI"));
       toElement.appendChild(document.createTextNode("STOCKHOLM"));


       flyElement.appendChild(fromElement);
       flyElement.appendChild(toElement);


       rootEelement.appendChild(flyElement);


       Element flyElement2 = document.createElement("fly");
       Attr attr2 = document.createAttribute("id");
       attr2.setValue("2");
       flyElement2.setAttributeNode(attr2);


       Element fromElement2 = document.createElement("from");
       Element toElement2 = document.createElement("to");


       fromElement2.appendChild(document.createTextNode("LISBON"));
       toElement2.appendChild(document.createTextNode("BUDAPEST"));


       flyElement2.appendChild(fromElement2);
       flyElement2.appendChild(toElement2);


       rootEelement.appendChild(flyElement2);


       TransformerFactory transformerFactory = TransformerFactory.newInstance();
       Transformer transformer = transformerFactory.newTransformer();
       DOMSource domSource = new DOMSource(document);
       StreamResult streamResult = new StreamResult(new File("C:/Users/qetiz/OneDrive/Desktop/a.xml"));


       transformer.transform(domSource, streamResult);


   }




//    public static void parseXML() throws ParserConfigurationException, IOException, SAXException {
//
//        File file = new File("C:/btu/a.xml");
//
//        DocumentBuilderFactory documentBuilderFactory = DocumentBuilderFactory.newInstance();
//        DocumentBuilder documentBuilder = documentBuilderFactory.newDocumentBuilder();
//        Document document = documentBuilder.parse(file);
//
//        document.getDocumentElement().normalize();
//
//        NodeList studentsList = document.getElementsByTagName("student");
//
//        for (int i = 0; i < studentsList.getLength(); i++) {
//            Node item = studentsList.item(i);
//            Element studentElement = (Element) item;
//            System.out.println(studentElement.getElementsByTagName("firstName").item(0).getTextContent());
//            System.out.println(studentElement.getElementsByTagName("lastName").item(0).getTextContent());
//            System.out.println(studentElement.getAttribute("groupNumber"));
//        }
//
//
//    }


}


Additional:
FileUtils - 
import java.io.*;
import java.util.Scanner;


public class FileUtils {


   public static void createFile() {
       File file = new File("file.txt");
       try {


           if (file.createNewFile()) {
               System.out.println("file created - " + file.getName());
           } else {
               System.out.println("already exists");
           }
       }
       catch (IOException e){
           System.out.println("error");
       }
   }


   public static void writeInFile(String str) {
       try {
           PrintWriter printWriter = new PrintWriter("file.txt");
           printWriter.print(str);
           printWriter.close();
       }
       catch (IOException e){
           System.out.println("error");
       }
   }


   public static int readFromFile() throws FileNotFoundException {
       Scanner scanner = new Scanner(new File("file.txt"));
       int max = scanner.nextInt();
       int min = max;
       while (scanner.hasNext()) {
           int next = scanner.nextInt();
           if(max < next){
               max = next;
           }
           if(min > next){
               min = next;
           }
       }
       scanner.close();
       return max - min;
   }


   public static void deleteFile(){
       File file = new File("file.txt");
       file.delete();
   }
}



Exceptions:
// class representing custom exception  
class InvalidAgeException  extends Exception  
{  
    public InvalidAgeException (String str)  
    {  
        // calling the constructor of parent Exception  
        super(str);  
    }  
}  
    
// class that uses custom exception InvalidAgeException  
public class TestCustomException1  
{  
  
    // method to check the age  
    static void validate (int age) throws InvalidAgeException{    
       if(age < 18){  
  
        // throw an object of user defined exception  
        throw new InvalidAgeException("age is not valid to vote");    
    }  
       else {   
        System.out.println("welcome to vote");   
        }   
     }    
  
    // main method  
    public static void main(String args[])  
    {  
        try  
        {  
            // calling the method   
            validate(13);  
        }  
        catch (InvalidAgeException ex)  
        {  
            System.out.println("Caught the exception");  
    
            // printing the message from InvalidAgeException object  
            System.out.println("Exception occured: " + ex);  
        }  
  
        System.out.println("rest of the code...");    
    }  
}  

Vargs:
class VarargsExample1{  
   
 static void display(String... values){  
  System.out.println("display method invoked ");  
 }  
  
 public static void main(String args[]){  
  
 display();//zero argument   
 display("my","name","is","varargs");//four arguments  
 }   
}  

Interface:
// Interface
interface Animal {
  public void animalSound(); // interface method (does not have a body)
  public void sleep(); // interface method (does not have a body)
}

// Pig "implements" the Animal interface
class Pig implements Animal {
  public void animalSound() {
    // The body of animalSound() is provided here
    System.out.println("The pig says: wee wee");
  }
  public void sleep() {
    // The body of sleep() is provided here
    System.out.println("Zzz");
  }
}

class Main {
  public static void main(String[] args) {
    Pig myPig = new Pig();  // Create a Pig object
    myPig.animalSound();
    myPig.sleep();
  }
}

Abstract:

abstract class Bike{  
  abstract void run();  
}  
class Honda4 extends Bike{  
void run(){System.out.println("running safely");}  
public static void main(String args[]){  
 Bike obj = new Honda4();  
 obj.run();  
}  
}  
