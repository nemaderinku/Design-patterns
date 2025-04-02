# Cleaner Logic with Strategy Pattern

Tired of messy if-else chains? In this guide, we’ll clean up a cluttered block of logic using the **Strategy Pattern** — explained through two analogies. Choose your flavor:

> 🔀 Jump to your favorite analogy:  
> - [🍳 Cooking Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/StrategyPattern.md#-cooking-analogy)
> - [🚗 Car Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/StrategyPattern.md#-cooking-analogy)

---

## 🍳 Cooking Analogy
🧠 Stop Overcooking Your If-Else: A Recipe for Cleaner Logic with the Strategy Pattern


```java
public class ActionService {
    public void perform(String mode) {
        if ("grill".equalsIgnoreCase(mode)) {
            System.out.println("Grilling the food...");
        } else if ("bake".equalsIgnoreCase(mode)) {
            System.out.println("Baking the food...");
        } else if ("fry".equalsIgnoreCase(mode)) {
            System.out.println("Frying the food...");
        } else {
            System.out.println("Unknown method.");
        }
    }
}

public interface CookingStrategy {
    void cook();
}

public class GrillStrategy implements CookingStrategy {
    public void cook() {
        System.out.println("Grilling the food to perfection 🔥");
    }
}

public class BakeStrategy implements CookingStrategy {
    public void cook() {
        System.out.println("Baking the dish until golden and crispy 🍞");
    }
}

public class FryStrategy implements CookingStrategy {
    public void cook() {
        System.out.println("Frying with sizzling oil 🍳");
    }
}

public class Chef {
    private CookingStrategy cookingMethod;

    public void setCookingMethod(CookingStrategy method) {
        this.cookingMethod = method;
    }

    public void prepareDish() {
        if (cookingMethod != null) {
            cookingMethod.cook();
        } else {
            System.out.println("No cooking method selected! 😬");
        }
    }
}

public class Kitchen {
    public static void main(String[] args) {
        Chef chef = new Chef();

        chef.setCookingMethod(new GrillStrategy());
        chef.prepareDish();

        chef.setCookingMethod(new BakeStrategy());
        chef.prepareDish();

        chef.setCookingMethod(new FryStrategy());
        chef.prepareDish();
    }
}
```
Grilling the food to perfection 🔥

Baking the dish until golden and crispy 🍞

Frying with sizzling oil 🍳


## 🚗 Car Analogy
🏎️ Too Many Ifs on the Road? Drive Clean with Strategy Pattern
Now imagine a car with different driving modes (sport, eco, comfort). Instead of a giant conditional block to handle each mode, the driver selects a driving strategy to control how the car behaves.

```java
public interface DrivingMode {
    void drive();
}

public class SportMode implements DrivingMode {
    public void drive() {
        System.out.println("Sport Mode – fast acceleration and tight handling 🏎️");
    }
}

public class EcoMode implements DrivingMode {
    public void drive() {
        System.out.println("Eco Mode – smooth and fuel-efficient 🚗");
    }
}

public class ComfortMode implements DrivingMode {
    public void drive() {
        System.out.println("Comfort Mode – relaxed driving experience 🛋️");
    }
}

public class Driver {
    private DrivingMode mode;

    public void setMode(DrivingMode mode) {
        this.mode = mode;
    }

    public void driveCar() {
        if (mode != null) {
            mode.drive();
        } else {
            System.out.println("No driving mode selected!");
        }
    }
}

public class Dashboard {
    public static void main(String[] args) {
        Driver driver = new Driver();

        driver.setMode(new SportMode());
        driver.driveCar();

        driver.setMode(new EcoMode());
        driver.driveCar();

        driver.setMode(new ComfortMode());
        driver.driveCar();
    }
}

```
Sport Mode – fast acceleration and tight handling 🏎️

Eco Mode – smooth and fuel-efficient 🚗

Comfort Mode – relaxed driving experience 🛋️


### 💡 Why Strategy Pattern Rocks
Open/Closed Principle: Add new behaviors (e.g., a new cooking method or driving mode) without modifying existing code.
Clean Code: Eliminate if-else chains for better readability.
Easy Testing: Each strategy is independent and can be tested in isolation.
Flexible: Switch behaviors dynamically at runtime.

### ⚠️ When Not to Use It
When you only have a couple of simple conditions.
When behaviors are unlikely to change.
When you want to avoid the overhead of extra classes.

