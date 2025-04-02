# Stop Switching So Much: Elegant Transitions with the State Pattern

The State Pattern lets an object change its behavior when its internal state changes — without using giant if-else or switch-case statements.

> 🔀 Jump to your favorite analogy:  
> - [🍳 Cooking Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/StatePattern.md#-cooking-analogy)
> - [🚗 Car Analogy](https://github.com/nemaderinku/Design-patterns/blob/main/StatePattern.md#-cooking-analogy)


## 🍳 Cooking Analogy

Imagine a smart oven that behaves differently depending on its mode:

1. Preheat – warming up

2. Bake – cooking at set temperature

3. KeepWarm – holding the heat after baking

4. Off – doing nothing



You can call the same methods (like pressStart() or openDoor()), but the oven reacts differently depending on its current state.

```Java

public interface OvenState {
    void pressStart();
    void openDoor();
}

public class PreheatState implements OvenState {
    public void pressStart() {
        System.out.println("🔥 Preheating... Please wait.");
    }

    public void openDoor() {
        System.out.println("🚪 You opened the door! Stopping preheat.");
    }
}

public class BakeState implements OvenState {
    public void pressStart() {
        System.out.println("🍞 Already baking. Sit tight!");
    }

    public void openDoor() {
        System.out.println("⚠️ Opening the oven during baking. Pausing bake.");
    }
}

public class KeepWarmState implements OvenState {
    public void pressStart() {
        System.out.println("♨️ Reheating... Still keeping things warm.");
    }

    public void openDoor() {
        System.out.println("🧤 Door opened. Holding temperature.");
    }
}

public class OffState implements OvenState {
    public void pressStart() {
        System.out.println("🔌 Turning on oven and starting preheat.");
    }

    public void openDoor() {
        System.out.println("🚪 It’s off — nothing to see in here.");
    }
}

public class SmartOven {
    private OvenState currentState;

    public SmartOven(OvenState state) {
        this.currentState = state;
    }

    public void setState(OvenState newState) {
        this.currentState = newState;
    }

    public void pressStart() {
        currentState.pressStart();
    }

    public void openDoor() {
        currentState.openDoor();
    }
}
public class Kitchen {
    public static void main(String[] args) {
        SmartOven oven = new SmartOven(new OffState());

        oven.pressStart(); // Turns on & starts preheating

        oven.setState(new PreheatState());
        oven.pressStart(); // Preheating
        oven.openDoor();   // Stopping preheat

        oven.setState(new BakeState());
        oven.pressStart(); // Already baking
        oven.openDoor();   // Pausing bake

        oven.setState(new KeepWarmState());
        oven.pressStart(); // Reheating
    }
}

```

## 🚗 Car Analogy


Imagine a car with multiple driving modes:

1. Park – the car is stopped

2. Drive – moves forward

3. Reverse – backs up

4. Neutral – coasts or idles

You interact with the car the same way (press the pedal, shift gears), but the behavior changes based on the current gear (aka state). That’s the State Pattern in action.

```Java
public interface DrivingState {
    void accelerate();
    void brake();
}
public class ParkState implements DrivingState {
    public void accelerate() {
        System.out.println("🅿️ Can't move while in Park.");
    }

    public void brake() {
        System.out.println("🛑 Already stopped.");
    }
}

public class DriveState implements DrivingState {
    public void accelerate() {
        System.out.println("🚗 Accelerating forward.");
    }

    public void brake() {
        System.out.println("🛑 Slowing down.");
    }
}

public class ReverseState implements DrivingState {
    public void accelerate() {
        System.out.println("🔙 Backing up.");
    }

    public void brake() {
        System.out.println("🛑 Stopping reverse.");
    }
}

public class NeutralState implements DrivingState {
    public void accelerate() {
        System.out.println("⚠️ Car is in Neutral — revving engine but not moving.");
    }

    public void brake() {
        System.out.println("🛑 Nothing to slow — you're idling.");
    }
}
public class Car {
    private DrivingState currentState;

    public Car(DrivingState initialState) {
        this.currentState = initialState;
    }

    public void setState(DrivingState state) {
        this.currentState = state;
    }

    public void pressGas() {
        currentState.accelerate();
    }

    public void pressBrake() {
        currentState.brake();
    }
}
public class Dashboard {
    public static void main(String[] args) {
        Car car = new Car(new ParkState());

        car.pressGas();   // Can't move
        car.pressBrake(); // Already stopped

        car.setState(new DriveState());
        car.pressGas();   // Accelerating forward
        car.pressBrake(); // Slowing down

        car.setState(new ReverseState());
        car.pressGas();   // Backing up

        car.setState(new NeutralState());
        car.pressGas();   // Revving engine
    }
}

```


### ✅ Why Use the State Pattern?
1. Avoids massive if or switch blocks

2. Encapsulates behavior per state

3. Makes transitions explicit and manageable

4. Super readable and easy to extend