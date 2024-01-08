ქლასრუმი:

Final:

package com.example.java_ketevan_zurashvili;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.chart.PieChart;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.stage.Stage;

import java.sql.*;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

import javafx.scene.layout.*;

public class HelloApplication extends Application {

    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("Product Store Application");

        // Create UI components
        TextField productNameTextField = new TextField();
        TextField priceTextField = new TextField();
        TextField quantityTextField = new TextField();
        Button addButton = new Button("Add Product");

        PieChart pieChart = new PieChart();

        // Set up layout
        VBox vBox = new VBox();
        vBox.setSpacing(10);
        vBox.getChildren().addAll(
                new Label("Product Name:"),
                productNameTextField,
                new Label("Price:"),
                priceTextField,
                new Label("Quantity:"),
                quantityTextField,
                addButton,
                pieChart
        );

        // Set up event handling
        addButton.setOnAction(e -> {
            // Add product to the database (implement this method)
            addProductToDatabase(
                    productNameTextField.getText(),
                    Double.parseDouble(priceTextField.getText()),
                    Integer.parseInt(quantityTextField.getText())
            );

            // Update pie chart (implement this method)
            updatePieChart(pieChart);
        });

        // Set up scene
        Scene scene = new Scene(vBox, 400, 400);
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    private void addProductToDatabase(String name, double price, int quantity) {
        String url = "jdbc:mysql://localhost:3306/keti";
        String user = "root";
        String password = null;

        try (Connection connection = DriverManager.getConnection(url, user, password)) {
            String query = "INSERT INTO products (name, price, quantity) VALUES (?, ?, ?)";
            try (PreparedStatement preparedStatement = connection.prepareStatement(query)) {
                preparedStatement.setString(1, name);
                preparedStatement.setDouble(2, price);
                preparedStatement.setInt(3, quantity);
                preparedStatement.executeUpdate();
            }
        } catch (SQLException e) {
            e.printStackTrace(); // Handle the exception appropriately in a real application
        }
    }

    private void updatePieChart(PieChart pieChart) {
        String url = "jdbc:mysql://localhost:3306/keti"; // Change the URL accordingly
        String user = "root";
        String password = null;

        List<Product> productList = new ArrayList();
        Map<String, Integer> productQuantities = new HashMap<>();

        try (Connection connection = DriverManager.getConnection(url, user, password)) {
            String query = "SELECT name, quantity FROM products";
            Statement statement = connection.createStatement();
            ResultSet resultSet = statement.executeQuery(query);

            while (resultSet.next()) {
                String productName = resultSet.getString("name");
                int quantity = resultSet.getInt("quantity");
                productList.add(new Product(productName, quantity));
            }
            System.out.println(productList);
            productQuantities = productList.stream()
                    .collect(Collectors.groupingBy(Product::getName, Collectors.summingInt(Product::getQuantity)));
        } catch (SQLException e) {
            e.printStackTrace(); // Handle the exception appropriately in a real application
        }

        // Update the PieChart data
        pieChart.getData().clear();
        productQuantities.forEach((productName, totalQuantity) ->
                pieChart.getData().add(new PieChart.Data(productName + " - " + totalQuantity + " pieces", totalQuantity)));
    }


}

------

package com.example.java_ketevan_zurashvili;

public class Product {
    private String name;
    private String description;
    private float price;
    private int quantity;

    public Product(String name, int quantity){
        this.name = name;
        this.quantity = quantity;
    }

    public String getName() {
        return name;
    }

    public int getQuantity() {
        return quantity;
    }
}

Tests:

public class MyMath {


   public int sum(int... numbers){
       int s  = 0;
       for (int i = 0; i < numbers.length; i++) {
           s += numbers[i];
       }
       return s;
   }


   public int calcRectangleArea(int a, int b){
       return a * b;
   }
}


import org.junit.jupiter.api.*;


public class MyMathTest {
   private static MyMath myMath;


   @BeforeAll
   public  static void setUp(){
       myMath = new MyMath();
   }


   @BeforeEach
   public void beforeEach(){
       System.out.printf("BeforeEach");
   }


   @Test
   public void testSome(){
       int sum = myMath.sum(1,2,3);
       Assertions.assertEquals(6, sum);
   }


   @RepeatedTest(5)
   public void testAreaCalc(){
       int area = myMath.calcRectangleArea(5,10);
       Assertions.assertEquals(50, area);
   }


   @AfterEach
   public void afterEach(){
       System.out.printf("AfterEach");
   }


   @AfterAll
   public static void afterAll(){
       myMath = null;
   }
}


Javafx:

package com.example.demo3;


import javafx.application.Application;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.scene.Group;
import javafx.scene.PerspectiveCamera;
import javafx.scene.Scene;
import javafx.scene.chart.PieChart;
import javafx.scene.layout.StackPane;
import javafx.scene.paint.Color;
import javafx.scene.shape.Box;
import javafx.stage.Stage;


public class HelloApplication extends Application {


   @Override
   public void start(Stage stage) {


// //        Box


//        Box box = new Box();
//
//        box.setTranslateX(150);
//        box.setTranslateY(230);
//        box.setTranslateZ(100);
//        box.setHeight(100);
//        box.setWidth(60);
//        box.setDepth(120);
//
//        PerspectiveCamera camera = new PerspectiveCamera();
//
//        camera.setTranslateX(100);
//        camera.setTranslateY(100);
//        camera.setTranslateZ(50);
//
//        Group root =  new Group();
//
//        root.getChildren().add(box);
//
//        Scene scene = new Scene(root, 500, 400, Color.AQUA);
//
//        scene.setCamera(camera);
//
//        stage.setTitle("Hello!");
//        stage.setScene(scene); // Use setScene instead of getScene
//        stage.show();


	// grid
/*Label first_name=new Label("First Name");
Label last_name=new Label("Last Name");
TextField tf1=new TextField();
TextField tf2=new TextField();
Button Submit=new Button ("Submit");
GridPane root=new GridPane();
Scene scene = new Scene(root,400,200);
root.addRow(0, first_name,tf1);
root.addRow(1, last_name,tf2);
root.addRow(2, Submit);
Submit.setOnAction(e -> {
  


});


stage.setScene(scene);
stage.show();*/




/ //       PieChart


       StackPane root = new StackPane();


       PieChart piechart = new PieChart();


       piechart.setData(getData());


       root.getChildren().add(piechart);


       Scene scene = new Scene(root, 500, 400, Color.AQUA);


       stage.setTitle("Hello!");
       stage.setScene(scene); // Use setScene instead of getScene
       stage.show();


   }


   private ObservableList<PieChart.Data> getData(){
       ObservableList<PieChart.Data> list = FXCollections.observableArrayList();
       list.add(new PieChart.Data("C#", 40));
       list.add(new PieChart.Data("Java", 30));
       list.add(new PieChart.Data("JavaScript", 30));
       return list;
   }


   public static void main(String[] args) {
       launch();
   }
}




Stream:
import java.sql.SQLOutput;
import java.util.*;
import java.util.stream.Collectors;
import java.util.stream.IntStream;
import java.util.stream.Stream;


public class Main {
   public static void main(String[] args){


//        Stream.of(1,2,3,4);
//        Arrays.asList(1,2,3,4,5).stream();
//        Stream<String> build = Stream.<String>builder().add("Str1").add("Str2").build();


//        Stream.generate(() -> 4).limit(10).forEach(s-> System.out.println(s));


//        Stream.iterate(1, e -> ++e).limit(30).forEach(s -> System.out.println(s));


//        IntStream.range(1,6).forEach(s -> System.out.println(s));


       Collection<String> cars = Arrays.asList("Mercedes", "Porsche", "BMW", "Maserati", "Bugatti");


//        Optional<String> firstElement = cars.stream().findFirst();


//        if(firstElement.isPresent()){
//            System.out.println(firstElement.get());
//        }else{
//            System.out.println("First element does not exist.");
//        }




//        long count = cars.stream().count();
//        System.out.println(count);


//        cars.stream().filter(s -> s.length() > 3).forEach(s -> System.out.println(s));


//        cars.stream().filter(s -> s.length() > 3).skip(2).forEach(s -> System.out.println(s));


//        cars.stream().filter(s -> s.length() > 3).skip(2).map(s -> s.length() * 2).filter(s-> s > 15).forEach(s -> System.out.println(s));
//        Set<Integer> collect = cars.stream().filter(s -> s.length() > 3).skip(2).map(s -> s.length() * 2).filter(s-> s > 15).collect(Collectors.toSet());
//        Map<String, Integer> collect = cars.stream().collect(Collectors.toMap(s -> s, s -> s.length()));


   }
}


Annotations:
import java.lang.reflect.Method;


public class Main {


   public static void main(String[] args) throws NoSuchMethodException {
       Utils utils = new Utils();


       Method method = utils.getClass().getMethod("printStr");


       MyAnnotation myAnnotation = method.getAnnotation(MyAnnotation.class);


       System.out.println(myAnnotation.value());
       System.out.println(myAnnotation.value1());
       Person person = new Person(2L, "aa","df");




   }
}

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;


@Target(value = {ElementType.FIELD, ElementType.METHOD, ElementType.CONSTRUCTOR})
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
   int value() default 0;
   String value1();
}

public class Utils {


   @MyAnnotation(value = 20, value1 = "string")
   public static void printStr(){
       System.out.println("String!");
   }
}

import lombok.*;


import java.lang.annotation.Target;


//@Getter
//@Setter
//@NoArgsConstructor
//@ToString
//@EqualsAndHashCode
//@AllArgsConstructor
//ან
@Data
@AllArgsConstructor
public class Person {


   private Long id;
   private String firstName;
   private String lastName;
}



databases:

// XAMPP


//-- Switch to the new database
//        USE your_database_name;
//
//        -- Create the 'student' table
//        CREATE TABLE student (
//        id INT NOT NULL AUTO_INCREMENT,
//        first_name VARCHAR(255),
//        last_name VARCHAR(255),
//        PRIMARY KEY (id)
//        );




import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;


public class Main {
   private  final static String url = "jdbc:mysql://localhost:3306/btu";
   private final static String name = "root";
   private final static String password = null;
   public static void main(String[] args) throws SQLException {


       Connection connection = DriverManager.getConnection(url, name, password);




       Statement statement = connection.createStatement();
       statement.executeUpdate("INSERT into student2(first_name, last_name) values ('Jano', 'Avladze')");


       statement.close();


       connection.close();


   }
}




import java.sql.*;


public class Main2 {


   private  final static String url = "jdbc:mysql://localhost:3306/btu";
   private final static String name = "root";
   private final static String password = null;
   public static void main(String[] args) throws SQLException {


       Connection connection = DriverManager.getConnection(url, name, password);


       Statement statement = connection.createStatement();
//        statement.executeUpdate("update student2 set first_name='Jani' where id=1");
//        statement.executeUpdate("delete  from student2 where id=1");


       ResultSet resultSet = statement.executeQuery("select * from student2");


       while (resultSet.next()){
           System.out.println(resultSet.getInt("id"));
           System.out.println(resultSet.getString("first_name"));
           System.out.println(resultSet.getString("last_name"));
       }


       resultSet.close();


       statement.close();


       connection.close();
   }
}


1.

Server:
import java.io.IOException;


// Press Shift twice to open the Search Everywhere dialog and type show whitespaces,
// then press Enter. You can now see whitespace characters in your code.
public class Main {
   public static void main(String[] args) throws IOException {


       MyServerSocket serverSocket = new MyServerSocket();
       serverSocket.startServer(4000);
   }


}


import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;


public class MyServerSocket {
   private ServerSocket serverSocket;
   private Socket clientSocket;
   private PrintWriter out;
   private BufferedReader in;


   public void startServer(int port) throws IOException {
       serverSocket = new ServerSocket(port);
       clientSocket = serverSocket.accept();
       out = new PrintWriter(clientSocket.getOutputStream(),  true);
       in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));


       String message = in.readLine();


       if(message.equals("Hello server"))
       {
           out.println("Hello client");


       }
       else {
           out.println("Error");
       }
   }


   public void close() throws IOException{
       serverSocket.close();
       clientSocket.close();
       in.close();
       out.close();
   }
}

Client:
import java.io.IOException;


// Press Shift twice to open the Search Everywhere dialog and type show whitespaces,
// then press Enter. You can now see whitespace characters in your code.
public class Main {


   public static void main(String[] args) throws IOException {




       MyClientSocket serverSocket = new MyClientSocket();
       serverSocket.startConnection("127.0.0.1", 4000);
       serverSocket.sendMessage("Hello server");
   }
}

import java.io.BufferedReader;
       import java.io.IOException;
       import java.io.InputStreamReader;
       import java.io.PrintWriter;
       import java.net.Socket;


public class MyClientSocket {
   private Socket clientSocket;
   private PrintWriter out;
   private BufferedReader in;
   void startConnection(String ip, int port) throws IOException {
       clientSocket = new Socket(ip, port);
       out = new PrintWriter(clientSocket.getOutputStream(),  true);
       in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
   }


   public void sendMessage(String message) throws IOException {
       out.println(message);
       String inMessage = in.readLine();
       System.out.println(inMessage);


   }


   public void close() throws IOException {
       clientSocket.close();
       in.close();
       out.close();
   }
}



2.
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.InetAddress;
import java.net.MulticastSocket;
import java.nio.charset.StandardCharsets;


public class ReadThread  implements Runnable{
   private static final int MAX_LEN = 1000;
   private MulticastSocket socket;
   private InetAddress group;
   private int port;
   public ReadThread(MulticastSocket socket, InetAddress group, int port){
       this.socket = socket;
       this.group =group;
       this.port = port;
   }
   @Override
   public void run(){
       while (true){
           byte[] buffer = new byte[ReadThread.MAX_LEN];
           DatagramPacket datagramPacket = new DatagramPacket(buffer, buffer.length, group, port);
           try {
               socket.receive(datagramPacket);
               String massage = new String(buffer, 0, datagramPacket.getLength(), StandardCharsets.UTF_8);
               if(massage.startsWith(GroupChat.name)){
                   System.out.println(massage);
               }
               System.out.println(massage);
           } catch (IOException e) {
               throw new RuntimeException(e);
           }
       }


   }
}

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.InetAddress;
import java.net.MulticastSocket;
import java.nio.charset.StandardCharsets;


public class ReadThread  implements Runnable{
   private static final int MAX_LEN = 1000;
   private MulticastSocket socket;
   private InetAddress group;
   private int port;
   public ReadThread(MulticastSocket socket, InetAddress group, int port){
       this.socket = socket;
       this.group =group;
       this.port = port;
   }
   @Override
   public void run(){
       while (true){
           byte[] buffer = new byte[ReadThread.MAX_LEN];
           DatagramPacket datagramPacket = new DatagramPacket(buffer, buffer.length, group, port);
           try {
               socket.receive(datagramPacket);
               String massage = new String(buffer, 0, datagramPacket.getLength(), StandardCharsets.UTF_8);
               if(massage.startsWith(GroupChat.name)){
                   System.out.println(massage);
               }
               System.out.println(massage);
           } catch (IOException e) {
               throw new RuntimeException(e);
           }
       }


   }
}



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
https://www.javatpoint.com/custom-exception

Collections:
https://www.geeksforgeeks.org/collections-in-java-2/?authuser=0


Quiz:
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;


public class Main {
   public static void main(String[] args) {
       List<Employee> employees = EmployeeManager.getEmployees();
       for (int i = 0; i < employees.size(); i++) {
           System.out.println(employees.get(i));
       }


       Map<String, Double> collect = employees.stream()
               .filter(s -> s.getAge() > 18 && s.getAge() < 30)
               .sorted((s1, s2) ->  (int) (s1.getSalary() - s2.getSalary()))
               .skip(1)
               .peek(s -> s.setSalary(s.getSalary() + 100))
               .collect(Collectors.toMap(
                       s -> s.getFirstName() + " " + s.getLastName(),
                       Employee::getSalary
               ));
       collect.forEach((key, value) -> System.out.println("Key: " + key + ", Salary: " + value));


   }
}







import java.util.List;


public class EmployeeManager {


   public static List<Employee> getEmployees() {
       List<Employee> employees = List.of(
               new Employee(1, "Nina", "Niashvili", 21, 50000.0),
               new Employee(2, "Ana", "Aptsiauri", 26, 45000.0),
               new Employee(3, "Mindia", "Aptsiauri", 26, 60000.0),
               new Employee(4, "Gela", "Geladze", 40, 55000.0),
               new Employee(5, "Babi", "Bregvadze", 37, 48000.0)
       );
       return employees;
   }
}


import lombok.*;


@Data
@NoArgsConstructor
@AllArgsConstructor
@Getter
@Setter
public class Employee {
   private long id;
   private String firstName;
   private String lastName;
   private int age;
   private double salary;
}



Last YEar code:

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class ProductDescriptionApp extends Application {

    private TextField productNameField;
    private ComboBox<String> productTypeComboBox;

    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("Product Description App");

        GridPane grid = createGridPane();
        createForm(grid);
        createTable(grid);

        Scene scene = new Scene(grid, 400, 300);
        primaryStage.setScene(scene);

        primaryStage.show();
    }

    private GridPane createGridPane() {
        GridPane grid = new GridPane();
        grid.setPadding(new Insets(10, 10, 10, 10));
        grid.setVgap(5);
        grid.setHgap(5);

        return grid;
    }

    private void createForm(GridPane grid) {
        Label productNameLabel = new Label("Product Name:");
        productNameField = new TextField();
        productNameField.setPromptText("Enter product name");

        Label productTypeLabel = new Label("Product Type:");
        productTypeComboBox = new ComboBox<>();
        productTypeComboBox.getItems().addAll("Shampoo", "Toy", "Condom", "Pillow");
        productTypeComboBox.setPromptText("Select product type");

        Button addButton = new Button("Add");
        addButton.setOnAction(e -> addProductToDatabase());

        grid.add(productNameLabel, 0, 0);
        grid.add(productNameField, 1, 0);
        grid.add(productTypeLabel, 0, 1);
        grid.add(productTypeComboBox, 1, 1);
        grid.add(addButton, 1, 2);
    }

    private void createTable(GridPane grid) {
        // Add a table to display products (if needed)
        // You can use TableView or other controls for this purpose
    }

    private void addProductToDatabase() {
        String productName = productNameField.getText();
        String productType = productTypeComboBox.getValue();

        if (productName.isEmpty() || productType == null) {
            showAlert("Error", "Please enter product information.");
            return;
        }

        try {
            // Replace the URL, username, and password with your database information
            String url = "jdbc:mysql://your_database_host:your_database_port/your_database_name";
            String username = "your_username";
            String password = "your_password";

            Connection connection = DriverManager.getConnection(url, username, password);

            // Replace "products" with your actual table name
            String insertQuery = "INSERT INTO products (name, type) VALUES (?, ?)";
            try (PreparedStatement preparedStatement = connection.prepareStatement(insertQuery)) {
                preparedStatement.setString(1, productName);
                preparedStatement.setString(2, productType);

                int rowsAffected = preparedStatement.executeUpdate();
                if (rowsAffected > 0) {
                    showAlert("Success", "Product added to the database.");
                    productNameField.clear();
                    productTypeComboBox.getSelectionModel().clearSelection();
                } else {
                    showAlert("Error", "Failed to add product to the database.");
                }
            }
        } catch (SQLException e) {
            showAlert("Error", "Database error: " + e.getMessage());
        }
    }

    private void showAlert(String title, String content) {
        Alert alert = new Alert(Alert.AlertType.INFORMATION);
        alert.setTitle(title);
        alert.setHeaderText(null);
        alert.setContentText(content);
        alert.showAndWait();
    }
}

