# From Plain to Powered-Up: Add Behavior on the Fly with Decorator Pattern

> 🔀 Jump to your favorite analogy:  
> - [🍳 Cooking Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/DecoratorPattern.md#-cooking-analogy)
> - [🚗 Car Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/DecoratorPattern.md#-cooking-analogy)


## 🍳 Cooking Analogy
Imagine you’re running a burger joint. You start with a base burger, then let customers customize it with toppings — cheese, bacon, lettuce, etc.

<img src="./videos/DecoratorPattern-cookinganalogy.gif" width="400" alt="Decorator Pattern Demo">

```Java
public interface Burger {
    String make();
}

public class BasicBurger implements Burger {
    public String make() {
        return "Bun + Patty";
    }
}

public abstract class BurgerDecorator implements Burger {
    protected Burger burger;

    public BurgerDecorator(Burger burger) {
        this.burger = burger;
    }

    public String make() {
        return burger.make();
    }
}

public class Cheese extends BurgerDecorator {
    public Cheese(Burger burger) {
        super(burger);
    }

    public String make() {
        return super.make() + " + Cheese 🧀";
    }
}

public class Bacon extends BurgerDecorator {
    public Bacon(Burger burger) {
        super(burger);
    }

    public String make() {
        return super.make() + " + Bacon 🥓";
    }
}

public class Lettuce extends BurgerDecorator {
    public Lettuce(Burger burger) {
        super(burger);
    }

    public String make() {
        return super.make() + " + Lettuce 🥬";
    }
}

public class BurgerShop {
    public static void main(String[] args) {
        Burger customBurger = new Lettuce(new Bacon(new Cheese(new BasicBurger())));
        System.out.println("Your order: " + customBurger.make());
    }
}
```


## 🚗 Car Analogy

Imagine buying a car. You start with a base model, and then choose upgrades: sunroof, sport rims, turbo engine, etc. Each upgrade wraps the base car with new features, without changing the car class itself. That’s the Decorator Pattern — layering enhancements on top of a base object.

```Java
public interface Car {
    String assemble();
}

public class BasicCar implements Car {
    public String assemble() {
        return "Base Car";
    }
}

public abstract class CarDecorator implements Car {
    protected Car car;

    public CarDecorator(Car car) {
        this.car = car;
    }

    public String assemble() {
        return car.assemble();
    }
}

public class Sunroof extends CarDecorator {
    public Sunroof(Car car) {
        super(car);
    }

    public String assemble() {
        return super.assemble() + " + Sunroof 🌞";
    }
}

public class SportRims extends CarDecorator {
    public SportRims(Car car) {
        super(car);
    }

    public String assemble() {
        return super.assemble() + " + Sport Rims 🛞";
    }
}

public class TurboEngine extends CarDecorator {
    public TurboEngine(Car car) {
        super(car);
    }

    public String assemble() {
        return super.assemble() + " + Turbo Engine 🔥";
    }
}

public class Garage {
    public static void main(String[] args) {
        Car customCar = new TurboEngine(new SportRims(new Sunroof(new BasicCar())));
        System.out.println("Your build: " + customCar.assemble());
    }
}


```

## ✅ Why Use the Decorator Pattern?
1. Add features dynamically, without subclassing

2. Combine behaviors flexibly at runtime

3. Keep code open for extension, closed for modification