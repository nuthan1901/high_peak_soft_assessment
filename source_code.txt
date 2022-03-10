
package peaksoft;   //package name

//importing libraries
import java.io.*;   
import java.util.*;

//define a class Input
class Input {
  String name;  //Goodies name Eg Fitbit,Ipod...etc
  int price;    //price of each Godies

    //defining an constructor
  public Input(String name, int price) {
    this.name = name;
    this.price = price;
  }
    //return the values to output
  public String toString() { 
      return this.name + ": " + this.price;
  }
}

//define a main class
public class Main {
  public static void main(String[] args) throws Exception {
      
      //import input file
    FileInputStream f=new FileInputStream("C:\\Users\\user\\Documents\\NetBeansProjects\\peaksoft\\src\\peaksoft\\input.txt");   
    //call input function scanner
    Scanner s=new Scanner(f);
    int total_employees = Integer.parseInt(s.nextLine().split(": ")[1]);
    s.nextLine(); s.nextLine(); s.nextLine();

        //define datastructure arraylist and import all inputs
    ArrayList<Input> items = new ArrayList<Input>();

        //split name and price with ":" using while loop
    while(s.hasNextLine())  
    {
      String current[] = s.nextLine().split(": ");
      items.add(new Input(current[0], Integer.parseInt(current[1])));
    }
    s.close();

     //Sort the items using price
    Collections.sort(items, new Comparator<Input>(){
      public int compare(Input a, Input b) { 
        return a.price - b.price; 
      } 
    });

        //compute the logic of output
    int difference = items.get(items.size()-1).price;
    int index = 0;
    for(int i=0;i<items.size()-total_employees+1;i++) {
      int diff = items.get(total_employees+i-1).price-items.get(i).price;

      if(diff<=difference) {
        difference = diff;
        index = i;
      }
    }
    
    
        //create the output file and write the output 
    FileWriter write = new FileWriter("C:\\Users\\user\\Documents\\NetBeansProjects\\peaksoft\\src\\peaksoft\\output.txt");
    write.write("The Items selected for distribution are:\n");
    for(int i=index;i<index + total_employees; i++) {
      write.write(items.get(i).toString() + "\n");
    }
        //print the difference of max and min
    write.write("\nAnd the difference between the chosen items with maximum price and the minimum price is " + difference);
	  write.close();
  }
}