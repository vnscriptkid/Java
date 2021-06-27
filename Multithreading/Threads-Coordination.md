## Question list
- What kind of resources do threads consume?
- When do we need terminate threads?
- When can we interrupt a thread?
- What are deamon threads?
- Give examples about deamon threads?
- What are 2 ways of responding to interrupt signals?
- How to prevent a thread from blocking our app from exiting?

## Diagrams
- Threads interrupt

![image](https://user-images.githubusercontent.com/28957748/123553162-d1892800-d7a3-11eb-85b7-498ff3714ad2.png)

## Make one thread deamon

```java
public class Main {
    private static class BlockingTask implements Runnable {
        @Override
        public void run() {
            try {
                Thread.sleep(50000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        Thread thread = new Thread(new BlockingTask());

        thread.setDaemon(true);

        thread.start();
    }
}
```

## Detect interrupt signal from other threads using `InterruptedException`

```java
public class Main {
    private static class BlockingTask implements Runnable {
        @Override
        public void run() {
            try {
                Thread.sleep(50000);
            } catch (InterruptedException e) {
                System.out.println("Received interrupt signal: " + e.getMessage());
            }
        }
    }

    public static void main(String[] args) {
        Thread thread = new Thread(new BlockingTask());

        thread.start();

        thread.interrupt();
    }
}
```

## Long running task that can not detect interrupt signal from outside
```java
import java.math.BigInteger;

public class Main {
    private static class LongRunningTask implements Runnable {
        private BigInteger base;
        private BigInteger power;

        public LongRunningTask(BigInteger base, BigInteger power) {
            this.base = base;
            this.power = power;
        }

        @Override
        public void run() {
            BigInteger result = BigInteger.ONE;

            for (BigInteger i = BigInteger.ZERO; i.compareTo(power) != 0; i = i.add(BigInteger.ONE)) {
                result = result.multiply(base);
            }

            System.out.println("Result of " + base + "^" + power + " is: " + result);
        }


    }

    public static void main(String[] args) {
        Thread thread = new Thread(new LongRunningTask(BigInteger.valueOf(1000000), BigInteger.valueOf(100000)));

        thread.start();

        thread.interrupt();
    }
}
```

## Detect interrupt signal by explicit checking inside long-running task
```java
import java.math.BigInteger;

public class Main {
    private static class LongRunningTask implements Runnable {
        private BigInteger base;
        private BigInteger power;

        public LongRunningTask(BigInteger base, BigInteger power) {
            this.base = base;
            this.power = power;
        }

        @Override
        public void run() {
            BigInteger result = BigInteger.ONE;

            for (BigInteger i = BigInteger.ZERO; i.compareTo(power) != 0; i = i.add(BigInteger.ONE)) {
                if (Thread.currentThread().isInterrupted()) {
                    System.out.println(this.getClass().getSimpleName() + " has been interrupted");
                    return;
                }
                result = result.multiply(base);
            }

            System.out.println("Result of " + base + "^" + power + " is: " + result);
        }


    }

    public static void main(String[] args) {
        Thread thread = new Thread(new LongRunningTask(BigInteger.valueOf(1000000), BigInteger.valueOf(100000)));

        thread.start();

        thread.interrupt();
    }
}
```
