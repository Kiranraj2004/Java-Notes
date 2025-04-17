
### **Inner Classes in Java**


**Introduction:**
- Inner classes are classes defined within other classes.
- There are four types of inner classes: Member Inner Class, Static Nested Class, Local Inner Class, and Anonymous Inner Class.

**1. Member Inner Class:**
- A class defined within another class and associated with an instance of the outer class.
- Example: `Engine` class inside `Car` class.
  ```java
  public class Car {
      private String model;
      private boolean engineOn;

      public Car(String model) {
          this.model = model;
          this.engineOn = false;
      }

      public class Engine {
          public void start() {
              if (!engineOn) {
                  engineOn = true;
                  System.out.println(model + " engine started");
              } else {
                  System.out.println(model + " engine is already on");
              }
          }

          public void stop() {
              if (engineOn) {
                  engineOn = false;
                  System.out.println(model + " engine stopped");
              } else {
                  System.out.println(model + " engine is already off");
              }
          }
      }
  }
  ```

**2. Static Nested Class:**
- A class defined within another class but not associated with an instance of the outer class.
- Used for grouping classes that belong together but do not require an instance of the outer class.
- Example: `USB` class inside `Computer` class.
  ```java
  public class Computer {
      private String brand;
      private String model;

      public Computer(String brand, String model) {
          this.brand = brand;
          this.model = model;
      }

      public static class USB {
          public void displayInfo() {
              System.out.println("USB information");
          }
      }
  }
  ```

**3. Local Inner Class:**
- A class defined within a method and only accessible within that method.
- Used for encapsulating logic that is only relevant within the method.
- Example: `ReservationValidator` class inside `reserveRoom` method of `Hotel` class.
  ```java
  public class Hotel {
      private String name;
      private int totalRooms;
      private int reservedRooms;

      public Hotel(String name, int totalRooms, int reservedRooms) {
          this.name = name;
          this.totalRooms = totalRooms;
          this.reservedRooms = reservedRooms;
      }

      public void reserveRoom(String guestName, int numberOfRooms) {
          class ReservationValidator {
              public boolean validate() {
                  if (guestName == null || guestName.isEmpty()) {
                      System.out.println("Guest name cannot be empty");
                      return false;
                  }
                  if (numberOfRooms < 0) {
                      System.out.println("Number of rooms should be positive");
                      return false;
                  }
                  if (reservedRooms + numberOfRooms > totalRooms) {
                      System.out.println("Not enough rooms available");
                      return false;
                  }
                  return true;
              }
          }

          ReservationValidator validator = new ReservationValidator();
          if (validator.validate()) {
              reservedRooms += numberOfRooms;
              System.out.println("Reservation confirmed for " + guestName);
          } else {
              System.out.println("Reservation failed");
          }
      }
  }
  ```

**4. Anonymous Inner Class:**
- A class defined and instantiated in a single statement without a name.
- Used for implementing an interface or extending a class on the fly.
- Example: Implementing `Payment` interface in `ShoppingCart` class.
  ```java
  public interface Payment {
      void pay(double amount);
  }

  public class ShoppingCart {
      private double totalAmount;

      public ShoppingCart(double totalAmount) {
          this.totalAmount = totalAmount;
      }

      public void processPayment(Payment paymentMethod) {
          paymentMethod.pay(totalAmount);
      }
  }

  // Usage
  ShoppingCart cart = new ShoppingCart(150.0);
  cart.processPayment(new Payment() {
      @Override
      public void pay(double amount) {
          System.out.println("Paid " + amount + " using credit card");
      }
  });
  ```

**Key Points:**
- **Member Inner Class:** Associated with an instance of the outer class.
- **Static Nested Class:** Not associated with an instance of the outer class.
- **Local Inner Class:** Defined within a method and only accessible within that method.
- **Anonymous Inner Class:** Defined and instantiated in a single statement without a name.