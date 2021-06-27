## Create a new thread
```java
Thread thread = new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("We are now in thread: " + Thread.currentThread().getName());
        System.out.println("With priority of " + Thread.currentThread().getPriority());
    }
});

thread.setName("My favorite thread");
thread.setPriority(Thread.MAX_PRIORITY);

System.out.println("Before thread start, we are in thread: " + Thread.currentThread().getName());

// this line runs asynchronously
thread.start();

System.out.println("After thread start, we are in thread: " + Thread.currentThread().getName());

Thread.sleep(5000);
```

## `Thread.sleep(5000)`
- No allocate CPU for this thread in 5 seconds

## Thread should have a specific name
```java
thread.setName("My favorite thread");
```

## Developers can adjust thread priority
```java
thread.setPriority(Thread.MAX_PRIORITY);
```

## Catch unhandled exceptions in thread
```java
Thread thread = new Thread(new Runnable() {
    @Override
    public void run() {
        throw new RuntimeException("Intentional error.");
    }
});

thread.setName("Misbehaving thread");

thread.setUncaughtExceptionHandler(new Thread.UncaughtExceptionHandler() {
    @Override
    public void uncaughtException(Thread t, Throwable e) {
        System.out.println("There was an exception happened in: " + t.getName());
        System.out.println("The error is: " + e.getMessage());
    }
});

thread.start();
```

## Another way to create new thread (using Thread Inheritance)
```java
private static class NewThread extends Thread {
    @Override
    public void run() {
        System.out.println("Hello from thread: " + this.getName());
    }
}

public static void main(String[] args) {
    Thread thread = new NewThread();
    thread.start();
}
```

## Case study: Password Hacking
![image](https://user-images.githubusercontent.com/28957748/123548250-30dc3d80-d78e-11eb-9737-f022780fb394.png)

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Random;

public class Main {

    private static class NewThread extends Thread {
        @Override
        public void run() {
            System.out.println("Hello from thread: " + this.getName());
        }
    }

    private abstract static class HackerThread extends Thread {
        protected Vault vault;

        public HackerThread(Vault vault) {
            this.vault = vault;
            this.setName(this.getClass().getSimpleName());
            this.setPriority(Thread.MAX_PRIORITY);
        }

        @Override
        public void run() {
            System.out.println("Starting hacker thread: " + this.getName());
            super.run();
        }
    }

    private static class AscendingHacker extends HackerThread {
        public AscendingHacker(Vault vault) {
            super(vault);
        }

        @Override
        public void run() {
            for (int i = 0; i < 10000; i++) {
                this.vault.checkPassword(i);
            }
        }
    }

    private static class DescendingHacker extends HackerThread {

        public DescendingHacker(Vault vault) {
            super(vault);
        }

        @Override
        public void run() {
            for (int i = 10000; i > 0; i--) {
                vault.checkPassword(i);
            }
        }
    }

    private static class Police extends Thread {
        public Police() {
            this.setName(this.getClass().getSimpleName());
            this.setPriority(Thread.MAX_PRIORITY);
        }

        @Override
        public void run() {
            for (int i = 0; i < 10; i++) {
                try {
                    System.out.println("Police is coming in: " + (10 - i) + " seconds.");
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println("Police came! Put your hands up!");
            System.exit(0);
        }
    }

    public static class Vault {
        private int password;

        public Vault(int password) {
            this.password = password;
        }

        public void checkPassword(int guess) {
            try {
                Thread.sleep(5);
                if (guess == password) {
                    System.out.println("Vault has been hacked by password: " + this.password);
                    System.exit(0);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        public void print() {
            System.out.println("Vault password is: " + this.password);
        }
    }

    public static void main(String[] args) {
        Random random = new Random();
        Vault vault = new Vault(random.nextInt(10000));
        vault.print();

        List<Thread> threads = new ArrayList<>();
        threads.add(new DescendingHacker(vault));
        threads.add(new AscendingHacker(vault));
        threads.add(new Police());

        for (Thread thread : threads) {
            thread.start();
        }
    }
}

```
