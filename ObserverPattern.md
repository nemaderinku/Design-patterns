# It's all about communication between objects. 

### It’s like saying, “Hey, something changed — just letting everyone know!”
Pick your favorite analogy:
> - [🍳 Cooking Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/ObserverPattern.md#-cooking-analogy)
> - [🚗 Car Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/ObserverPattern.md#-car-analogy)


## 🍳 Cooking Analogy

🔔 Real-World Analogy: The Kitchen Bell
In a busy restaurant:

1. The chef (Subject) finishes a dish and rings a bell.

2. All waiters (Observers) are listening.

3. When they hear the bell, they rush over to pick up their order.

4. The chef doesn’t care how many waiters are listening — the message gets broadcast, and everyone reacts independently.

<img src="./videos/observerPattern-cookinganalogy.gif" width="400" alt="Command Pattern Demo">

```Java
public interface Waiter {
    void notifyDishReady(String dish);
}

public class AliceWaiter implements Waiter {
    public void notifyDishReady(String dish) {
        System.out.println("Alice is serving the " + dish + ".");
    }
}

public class BobWaiter implements Waiter {
    public void notifyDishReady(String dish) {
        System.out.println("Bob is on it! Serving the " + dish + ".");
    }
}

public interface Chef {
    void addWaiter(Waiter waiter);
    void removeWaiter(Waiter waiter);
    void notifyWaiters(String dish);
}

import java.util.ArrayList;
import java.util.List;

public class HeadChef implements Chef {
    private List<Waiter> waiters = new ArrayList<>();

    public void addWaiter(Waiter waiter) {
        waiters.add(waiter);
    }

    public void removeWaiter(Waiter waiter) {
        waiters.remove(waiter);
    }

    public void notifyWaiters(String dish) {
        for (Waiter w : waiters) {
            w.notifyDishReady(dish);
        }
    }

    public void finishDish(String dish) {
        System.out.println("Chef: " + dish + " is ready!");
        notifyWaiters(dish);
    }
}

public class KitchenObserverDemo {
    public static void main(String[] args) {
        HeadChef chef = new HeadChef();

        Waiter alice = new AliceWaiter();
        Waiter bob = new BobWaiter();

        chef.addWaiter(alice);
        chef.addWaiter(bob);

        chef.finishDish("Pasta Carbonara");
    }
}
```

## 🚗 Car Analogy

1. Picture a smart car factory where the Assembly Line Manager (Subject) finishes building a car. 
2. Once it's done, they notify all departments — quality control, painting, shipping — without knowing how many are watching or what they’ll do with that info.

3. Each department subscribes to the assembly line, and when a new car rolls out, they react accordingly.


```Java
public interface Department {
    void update(String carModel);
}

public class QualityControl implements Department {
    public void update(String carModel) {
        System.out.println("🔍 QC: Inspecting the " + carModel);
    }
}

public class PaintShop implements Department {
    public void update(String carModel) {
        System.out.println("🎨 PaintShop: Painting the " + carModel);
    }
}

public class Shipping implements Department {
    public void update(String carModel) {
        System.out.println("📦 Shipping: Preparing " + carModel + " for delivery");
    }
}

public interface AssemblyLine {
    void addDepartment(Department department);
    void removeDepartment(Department department);
    void notifyDepartments(String carModel);
}

import java.util.ArrayList;
import java.util.List;

public class CarAssemblyLine implements AssemblyLine {
    private List<Department> departments = new ArrayList<>();

    public void addDepartment(Department department) {
        departments.add(department);
    }

    public void removeDepartment(Department department) {
        departments.remove(department);
    }

    public void notifyDepartments(String carModel) {
        for (Department d : departments) {
            d.update(carModel);
        }
    }

    public void completeBuild(String carModel) {
        System.out.println("🏭 Assembly Line: " + carModel + " is ready!");
        notifyDepartments(carModel);
    }
}
public class FactoryObserverDemo {
    public static void main(String[] args) {
        CarAssemblyLine line = new CarAssemblyLine();

        Department qc = new QualityControl();
        Department paint = new PaintShop();
        Department ship = new Shipping();

        line.addDepartment(qc);
        line.addDepartment(paint);
        line.addDepartment(ship);

        line.completeBuild("Electric SUV");
    }
}


```

### ✅ Why Use Observer?
Loose coupling between notifier (Subject) and responders (Observers)

Easy to add/remove subscribers

Common in UI, messaging, event systems
