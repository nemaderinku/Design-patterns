# Decouple, Delegate, Do It Later: Master the Command Pattern 

It's like writing down an order — instead of doing it immediately, you store it for execution.

> 🔀 Jump to your favorite analogy:  
> - [🍳 Cooking Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/CommandPattern.md#-cooking-analogy)
> - [🚗 Car Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/CommandPattern.md#-cooking-analogy)


## 🍳 Cooking Analogy

---
layout: default
---

<video width="640" height="360" controls>
  <source src="/Design-patterns/videos/commandPattern-cookinganalogy.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>



In a restaurant:

1. The Customer makes a request (e.g., "Make Pasta")

2. The Waiter writes it on an order ticket (the Command)

3. The Chef executes the order

<I> Basically decoupling</I>


```Java

public interface OrderCommand {
    void execute();
}


public class Chef {
    public void makePasta() {
        System.out.println("👨‍🍳 Cooking Pasta...");
    }

    public void makeBurger() {
        System.out.println("👨‍🍳 Grilling Burger...");
    }
}


public class PastaOrder implements OrderCommand {
    private Chef chef;

    public PastaOrder(Chef chef) {
        this.chef = chef;
    }

    public void execute() {
        chef.makePasta();
    }
}

public class BurgerOrder implements OrderCommand {
    private Chef chef;

    public BurgerOrder(Chef chef) {
        this.chef = chef;
    }

    public void execute() {
        chef.makeBurger();
    }
}

import java.util.ArrayList;
import java.util.List;

public class Waiter {
    private List<OrderCommand> orders = new ArrayList<>();

    public void takeOrder(OrderCommand order) {
        orders.add(order);
    }

    public void sendOrdersToKitchen() {
        System.out.println("🧾 Sending orders to the kitchen...");
        for (OrderCommand order : orders) {
            order.execute();
        }
        orders.clear();
    }
}

public class Restaurant {
    public static void main(String[] args) {
        Chef chef = new Chef();

        OrderCommand pastaOrder = new PastaOrder(chef);
        OrderCommand burgerOrder = new BurgerOrder(chef);

        Waiter waiter = new Waiter();
        waiter.takeOrder(pastaOrder);
        waiter.takeOrder(burgerOrder);

        waiter.sendOrdersToKitchen();
    }
}

```

## 🚗 Car Analogy

In a car service center:

1. A Service Advisor takes your request ("Change Oil", "Upgrade Tires")

2. They create a work order (the Command)

3. The Mechanic (Receiver) does the actual work
<I> Basically decoupling </I>


```Java
public interface ServiceCommand {
    void execute();
}

public class Mechanic {
    public void changeOil() {
        System.out.println("🔧 Changing engine oil...");
    }

    public void rotateTires() {
        System.out.println("🛞 Rotating the tires...");
    }
}

public class OilChangeCommand implements ServiceCommand {
    private Mechanic mechanic;

    public OilChangeCommand(Mechanic mechanic) {
        this.mechanic = mechanic;
    }

    public void execute() {
        mechanic.changeOil();
    }
}

public class TireRotationCommand implements ServiceCommand {
    private Mechanic mechanic;

    public TireRotationCommand(Mechanic mechanic) {
        this.mechanic = mechanic;
    }

    public void execute() {
        mechanic.rotateTires();
    }
}

public class OilChangeCommand implements ServiceCommand {
    private Mechanic mechanic;

    public OilChangeCommand(Mechanic mechanic) {
        this.mechanic = mechanic;
    }

    public void execute() {
        mechanic.changeOil();
    }
}

public class TireRotationCommand implements ServiceCommand {
    private Mechanic mechanic;

    public TireRotationCommand(Mechanic mechanic) {
        this.mechanic = mechanic;
    }

    public void execute() {
        mechanic.rotateTires();
    }
}
import java.util.ArrayList;
import java.util.List;

public class ServiceAdvisor {
    private List<ServiceCommand> commands = new ArrayList<>();

    public void addService(ServiceCommand command) {
        commands.add(command);
    }

    public void processServices() {
        System.out.println("📋 Processing service queue...");
        for (ServiceCommand command : commands) {
            command.execute();
        }
        commands.clear();
    }
}

public class CarServiceCenter {
    public static void main(String[] args) {
        Mechanic mechanic = new Mechanic();

        ServiceCommand oilChange = new OilChangeCommand(mechanic);
        ServiceCommand tireRotation = new TireRotationCommand(mechanic);

        ServiceAdvisor advisor = new ServiceAdvisor();
        advisor.addService(oilChange);
        advisor.addService(tireRotation);

        advisor.processServices();
    }
}


```

### ✅ Why Use the Command Pattern?
1. Decouples the object that invokes the action from the one that performs it

2. Enables queueing, logging, or undoing actions

3. Great for task schedulers, button actions, macro commands
