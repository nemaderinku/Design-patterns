# Centralize Creation with the Factory Pattern

Manually creating objects all over your codebase? That’s a recipe for repetition and tight coupling.
The Factory Pattern is your shortcut to clean, scalable object creation — and we’ll make it easy to grasp with two fun analogies: a kitchen and a car factory. Pick one you like.

> 🔀 Jump to your favorite analogy:  
> - [🍳 Cooking Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/FactoryPattern.md#-cooking-analogy)
> - [🚗 Car Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/FactoryPattern.md#-cooking-analogy)

---

## 🍳 Cooking Analogy
Imagine a kitchen with a menu. You (the waiter) just take the customer's order — "pasta", "burger", or "salad" — and hand it off to the kitchen. The kitchen knows exactly how to prepare the dish. You don’t create or touch any ingredients yourself.

```Java
public interface Dish {
    void serve();
}

public class Pasta implements Dish {
    public void serve() {
        System.out.println("🍝 Serving a hot plate of pasta.");
    }
}

public class Burger implements Dish {
    public void serve() {
        System.out.println("🍔 Serving a juicy burger.");
    }
}

public class Salad implements Dish {
    public void serve() {
        System.out.println("🥗 Serving a fresh salad.");
    }
}

public class KitchenFactory {
    public static Dish prepareDish(String order) {
        switch (order.toLowerCase()) {
            case "pasta":
                return new Pasta();
            case "burger":
                return new Burger();
            case "salad":
                return new Salad();
            default:
                throw new IllegalArgumentException("❌ We don't serve that dish: " + order);
        }
    }
}

public class Restaurant {
    public static void main(String[] args) {
        Dish dish1 = KitchenFactory.prepareDish("pasta");
        dish1.serve();

        Dish dish2 = KitchenFactory.prepareDish("burger");
        dish2.serve();
    }
}

```
✅ Why This Works
1. The client (Restaurant) doesn't need to know how each dish is made.

2. The Factory (Kitchen) handles all object creation.

3. It's easy to add a new dish (like "taco") without touching the rest of the code.


## 🚗 Car Analogy
Picture a car manufacturing plant. You place an order for a vehicle: "SUV", "sedan", or "truck". You don’t assemble it yourself — the Car Factory does that and hands you a ready-to-drive car.

```Java
public interface Car {
    void drive();
}

public class SUV implements Car {
    public void drive() {
        System.out.println("🚙 Driving a rugged SUV.");
    }
}

public class Sedan implements Car {
    public void drive() {
        System.out.println("🚗 Cruising in a comfy sedan.");
    }
}

public class Truck implements Car {
    public void drive() {
        System.out.println("🚚 Hauling heavy loads in a truck.");
    }
}

public class CarFactory {
    public static Car buildCar(String type) {
        switch (type.toLowerCase()) {
            case "suv":
                return new SUV();
            case "sedan":
                return new Sedan();
            case "truck":
                return new Truck();
            default:
                throw new IllegalArgumentException("❌ Unknown car type: " + type);
        }
    }
}

public class Dealership {
    public static void main(String[] args) {
        Car car1 = CarFactory.buildCar("sedan");
        car1.drive();

        Car car2 = CarFactory.buildCar("truck");
        car2.drive();
    }
}

```

## ✅ Why This Works
1. The Dealership (client) doesn't worry about how cars are built.

2. The Factory hides the object creation logic.

3. You can easily add more car types later without changing client code.