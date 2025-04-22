# Mercedes-AutoMart-system
The Mercedes AutoMart System is a Java console application that simulates a Mercedes-Benz dealership. It showcases core OOP concepts like inheritance, composition, aggregation, and multithreading. Users can view available car models, customize features, and get pricing details.
import java.util.Scanner;

class Car {
String model;
long price;

public void showDetails() {
System.out.println("Model: " + model);
System.out.println("Base Price: " + price + " PKR");

 }
}

class EClass extends Car {
public EClass(String type) {
model = "E-Class";
price = type.equalsIgnoreCase("new") ? 25000000 : 15000000;
}
}

class SClass extends Car {
public SClass(String type) {
model = "S-Class";
price = type.equalsIgnoreCase("new") ? 45000000 : 25000000;
}
}

class GWagon extends Car {
public GWagon(String type) {
model = "G-Wagon";
price = type.equalsIgnoreCase("new") ? 80000000 : 50000000;
}
}



class Modification {
long tirePrice = 0;
long paintPrice = 0;
long exhaustPrice = 0;

public void setTire(String tire) {
if (tire.equalsIgnoreCase("Sport Tire")) tirePrice = 500000;
else if (tire.equalsIgnoreCase("Off-Road Tire")) tirePrice = 700000;
else if (tire.equalsIgnoreCase("Classic Tire")) tirePrice = 300000;
}

public void setPaint(String paint) {
if (paint.equalsIgnoreCase("Black") || paint.equalsIgnoreCase("White") || paint.equalsIgnoreCase("Metallic Silver"))
paintPrice = 1000000;
}

public void setExhaust(String exhaust) {
if (exhaust.equalsIgnoreCase("yes")) exhaustPrice = 800000;
}

public long getTotalModificationPrice() {
return tirePrice + paintPrice + exhaustPrice;
 }

 public void showMods() {
 System.out.println("Tire Price: " + tirePrice + " PKR");
 System.out.println("Paint Price: " + paintPrice + " PKR");
 System.out.println("Exhaust Price: " + exhaustPrice + " PKR");
    }
}





class Showroom extends Thread {
Car car;
Modification mod;

Showroom(Car car, Modification mod) {
this.car = car;
this.mod = mod;
}

public void run() {
try {
System.out.println("Preparing your car... Please wait...");
Thread.sleep(3000);
car.showDetails();
mod.showMods();
System.out.println("Total Price: " + (car.price + mod.getTotalModificationPrice()) + " PKR");
System.out.println("Your car is ready!");
}
catch
(InterruptedException e) {
System.out.println("Something went wrong!");
}
}
}

public class Main {
public static void main(String[] args) {
Scanner input = new Scanner(System.in);
System.out.print("Do you want a new or used car? ");
String type = input.nextLine();

System.out.println("Available Models:" + " E-Class, S-Class, G-Wagon");
System.out.print("Which model do you want? ");
String model = input.nextLine();

Car selectedCar;
if (model.equalsIgnoreCase("E-Class")) selectedCar = new EClass(type);
else if (model.equalsIgnoreCase("S-Class")) selectedCar = new SClass(type);
else selectedCar = new GWagon(type);

Modification mod = new Modification();

System.out.print("Do you want to modify your car? (yes/no): ");
String modify = input.nextLine();
if (modify.equalsIgnoreCase("yes")) {
System.out.println("Choose Tire: Sport Tire, Off-Road Tire, Classic Tire");
mod.setTire(input.nextLine());

System.out.println("Choose Paint: Black, White, Metallic Silver");
mod.setPaint(input.nextLine());

System.out.print("Do you want Sport Exhaust? (yes/no): ");
mod.setExhaust(input.nextLine());
}



 Showroom showroom = new Showroom(selectedCar, mod);
   showroom.start();
    }
}

