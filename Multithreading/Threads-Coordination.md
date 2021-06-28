## Question list
- What kind of resources do threads consume?
- When do we need terminate threads?
- When can we interrupt a thread?
- What are deamon threads?
- Give examples about deamon threads?
- What are 2 ways of responding to interrupt signals?
- How to prevent a thread from blocking our app from exiting?
- Does System.in.read() respond to interrupt?
- Why do we need thread coordination?
    - Different threads run independently by default
    - Order of execution is out of our control

## Diagrams
- Threads interrupt

![image](https://user-images.githubusercontent.com/28957748/123553162-d1892800-d7a3-11eb-85b7-498ff3714ad2.png)

- Execution order scenarios:

![image](https://user-images.githubusercontent.com/28957748/123575240-869aff00-d7fb-11eb-9afc-2a526c16e201.png)

![image](https://user-images.githubusercontent.com/28957748/123575268-9adefc00-d7fb-11eb-8195-69a4b8c9d8a1.png)

![image](https://user-images.githubusercontent.com/28957748/123575322-b4804380-d7fb-11eb-85a3-eea5530de381.png)

![image](https://user-images.githubusercontent.com/28957748/123575370-c7931380-d7fb-11eb-856c-30c40aba242b.png)

- Thread dependency

![image](https://user-images.githubusercontent.com/28957748/123575416-e1ccf180-d7fb-11eb-8def-aedbd21dc0f2.png)

![image](https://user-images.githubusercontent.com/28957748/123575537-340e1280-d7fc-11eb-8527-dab12075a9c4.png)

![image](https://user-images.githubusercontent.com/28957748/123575567-42f4c500-d7fc-11eb-82b8-ac3632baf3f5.png)

![image](https://user-images.githubusercontent.com/28957748/123575619-530ca480-d7fc-11eb-998c-3298421a2a9e.png)

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
                return;
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
