
 <h3> <ins>Assignment Details</ins></h3>

**Implement a simple producer-consumer problem**

Create a Java program that simulates a producer-consumer scenario. The producer generates random numbers and puts them into a shared buffer, while the consumer takes the numbers from the buffer and calculates their sum. Use threads, synchronization, and the `wait()` and `notifyAll()` methods to ensure proper coordination between the producer and consumer.

1. Set up a new Java project in your preferred IDE or text editor.
    
2. Define a `SharedBuffer` class to handle the shared buffer between producer and consumer threads. Implement the following functionalities:
    
    a. Store and manage the buffer.
    
    b. Limit the maximum buffer size.
    
    c. Provide synchronized methods for adding elements to and removing elements from the buffer.
    
    d. Use `wait()` and `notifyAll()` methods to coordinate access to the buffer.
    
3. Implement a `Consumer` class that represents the consumer thread. This class should:
    
    a. Accept a reference to the `SharedBuffer` object.
    
    b. Retrieve numbers from the shared buffer using the appropriate synchronized method.
    
    c. Calculate the sum of the retrieved numbers.
    
4. In the `main` method or a separate `Main` class:
    
    a. Create an instance of the `SharedBuffer` class with a specified maximum size.
    
    b. Instantiate the `Producer` and `Consumer` classes, passing the `SharedBuffer` instance to both.
    
    c. Create two `Thread` objects, one for the producer and one for the consumer, using the instances created in the previous step.
    
    d. Start both threads.
    
5. Test the program to ensure that the producer generates random numbers, the consumer calculates their sum, and proper coordination is maintained between the two threads using synchronization, `wait()`, and `notifyAll()` methods.
    
6. Implement a `Producer` class that represents the producer thread. This class should:
    
    a. Accept a reference to the `SharedBuffer` object.
    
    b. Generate random numbers.
    
    c. Add the random numbers to the shared buffer using the appropriate synchronized method.


<h2> Contents</h2>

<ol> 
<li> SharedBuffer Class</li>
<li> Producer Class</li>
<li> Consumer Class</li>
<li> Main Class</li>
<li> Important Concepts From This Lesson</li>
<li> Step by Step Instructions with Code </li>
</ol>



<h2> 1. SharedBuffer Class </h2> 
<h6> 
The <strong>`SharedBuffer`</strong> class is designed to act as a shared resource between the producer and the consumer threads. It uses a queue to store items, provides synchronized methods to add and remove items and ensures proper coordination using <strong>`wait()`</strong> and <strong>`notifyAll()`</strong>.
</h6>
<ol>
	<li> Imports</li>
		<ul>
			<li> <strong>`import java.util.LinkedList;`</strong></li>
			<li> <strong>`import java.util.Queue;` </strong></li>
			<li> These imports are necessary to use the <strong>`Queue`</strong> and <strong>`LinkedList Classes`</strong> </li>
		</ul>
	<li> Class Declaration</li>
		<ul>
			<li> <strong>`public class SharedBuffer`</strong> declares a class</li>
		</ul>
	<li> Member Variables</li>
		<ul>
			<li> <strong>`private final Queue<Integer> buffer;`</strong> is a queue that holds the items</li>
			<li> <strong>`private final int maxSize;`</strong> sets the maximum size of the buffer </li>
		</ul>
	<li> Constructor</li>
		<ul>
			<li> <strong>`public SharedBuffer(int maxSize)`</strong> initializes the buffer as a <strong>`LinkedList`</strong> and sets the maximum buffer size</li>
		</ul>
	<li> add Method</li>
		<ul>
			<li> <strong>`public synchronized void add(int value) throws InterruptedException`</strong> is a synchronized methog to add items to the buffer</li>
			<li> <strong>`while (buffer.size() == maxSize)` checks if the buffer is full, if so the thread waits </li>
			<li> <strong>`buffer.add(value)`</strong> adds the value to the buffer </li>
			<li><strong>`notifyAll()`</strong> wakes up all waiting threads</li>
		</ul>
	<li> remove Method</li>
		<ul>
			<li> <strong>`public synchronized int remove() throws InterruptedException`</strong> is a synchronized method to remove items from the buffer</li>
			<li> <strong>`while (buffer.isEmpty())`</strong>  check if the buffer is empty, if so the thread waits </li>
			<li> <strong>`int value = buffer.remove()`</strong> removes and returns the value from the buffer </li>
			<li> <strong>`notifyAll()`</strong> wakes up all waiting threads
		</ul>
</ol>

<h2> 2. Producer Class </h2> 
<h6> 
The <strong>`Producer`</strong> class is responsible for generating random numbers and adding them to the shared buffer/ it runs its own thread and continuously produces numbers until it is stopped. 
</h6>

<ol>
	<li> Imports</li>
		<ul>
			<li> <strong>`import java.util.Random;`</strong> is necessary for generating random numbers</li>
		</ul>
	
	
	<li> Class Declaration</li>
		<ul>
			<li> <strong>`public class Producer implements Runnable`</strong> declares the class and implements the <strong>`Runnable`</strong> interface so it can run a thread</li>
		</ul>
	<li> Member Variables</li>
		<ul>
			<li> <strong>`private final SharedBuffer sharedbuffer`</strong> is a reference to the shared buffer</li>
			<li> <strong>`private final Random random`</strong> is a random number generator </li>
			<li> <strong>`private volatile boolean running = true`</strong> is a flag to control the loop </li>
		</ul>
	<li> Constructor</li>
		<ul>
			<li> <strong>`public Producer (SharedBuffer sharedBuffer)`</strong> initializes the shared buffer refernece and random number generator</li>
		</ul>
	<li> run Method</li>
		<ul>
			<li> <strong>` public void run()`</strong> contains the logic that will be executed when the thread starts</li>
			<li> <strong>`while (running)`</strong> is a continuous production loop controlled by the `running` flag</li>
			<li> <strong>`int value = random.nextInt(100)`</strong> generates a radnom number between 0 - 99</li>
			<li> <strong>`sharedBuffer.add(value)`</strong> adds the generated number to the buffer</li>
			<li> <strong>`System.out.printLn("Produced" + value)`</strong> prints the produced value</li>
			<li> <strong>`Thread.sleep(100)`</strong> sleeps for 100 ms to simulate production delay</li>
			<li> <strong>`catch (InterruptedExcpetion e)`</strong> catches any interruption and exits the loop if interrupted
		</ul>
	<li> stop Method</li>
		<ul>
			<li> <strong>`public void stop();`</strong> sets the <strong>`running`</strong> flag to the <strong>`false`</strong> to exit the loop</li>
		</ul>
</ol>

<h2> 3. Consumer Class </h2> 
<h6> 
The <strong>`Consumer`</strong> class is repsponsible for generating random numbers and adding them to the shared buffer/ it runs its own thread and continuously produces numbers until it is stopped. 
</h6>

<ol>
	<li> Class Declaration</li>
		<ul>
			<li> <strong>`public class Consumer implements Runnable`</strong> declares the class and implements the <strong>`Runnable`</strong> so it can run a thread</li>
		
		</ul>
	<li> Member Variables</li>
		<ul>
			<li> <strong>`private final SharedBuffer sharedBuffer`</strong> is a reference to the shared buffer</li>
			<li> <strong>`private volatile boolean running = true`</strong> is a flag to control the loop</li>
		</ul>
	<li> Constructor</li>
		<ul>
			<li> <strong>`public Consumer(SharedBuffer sharedBuffer`</strong> initializes the shared buffer reference</li>
		</ul>
	<li> run Method</li>
		<ul>
			<li> <strong>`public void run()`</strong> contains the logic that will will be executed when the thread starts</li>
			<li> <strong>`int sum = 0`</strong> initializes the sum of consumed numbers</li>
			<li> <strong>`while (running)`</strong> is a continuous consumption loop controlled by the <strong>`running`</strong> flag</li>
			<li> <strong>`int value = sharedBuffer.remove()`</strong> removes the value from the buffer </li>
			<li><strong>`system.out.println("Consumed" + value + | Current Sum: " + sum) `</strong>prints the consumed value and current sum</li>
			<li><strong>`Thread.sleep(150)" `</strong>sleeps for 150 ms to simulate consumetion delay</li>
			<li><strong>`catch (InterruptedException e)`</strong>catches any interruption and exits the loop if interrupted</li>
		</ul>
	<li> stop Method</li>
		<ul>
			<li> <strong>`public void stop()`</strong> sets the <strong> `running`</strong> flag to <strong>`false`</strong> to exit the loop</li>
		</ul>
</ol>

<h2> 4. Main Class </h2> 
<h6> 
The <strong>`Main`</strong> class coordinates the creation and starting of the Producer and Consumer threads. it also provides the mechanism to stope the threads after a certain amount of time.
</h6>

<ol>
	<li> Class Declaration</li>
		<ul>
			<li> <strong>`public class Main`</strong> declares the class</li>
		</ul>
	<li> main Method</li>
		<ul>
			<li> <strong>`public static void main(String[] args)`</strong> contains the logic that will be executed when the program starts</li>
		</ul>
	<li> SharedBuffer initialization</li>
		<ul>
			<li> <strong>`SharedBuffer sharedBuffer = new SharedBuffer(10)`</strong> creates a shared buffer with a max size of 10</li>
		</ul>
	<li> Producer and Consumer Initialization</li>
		<ul>
			<li> <strong>`Producer producer = new Producer(sharedBuffer)`</strong> creates a producer with the shared buffer</li>
			<li> <strong>`Consumer consumer = new Consumer(sharedBuffer)`</strong> creates a consumer with the shared buffer</li>
		</ul>
	<li> Thread Creation</li>
		<ul>
			<li> <strong>`Thread producerThread = new Thread(producer)`</strong>creates a thread for the producer</li>
			<li> <strong>`Thread consumerThread = new Thread(consumer)`</strong>creates a thread for the consumer</li>
		</ul>
	<li> Start Threads</li>
		<ul>
			<li> <strong>`producerThread.start()`</strong> starts the producer thread</li>
			<li> <strong>`consumerThread.start()`</strong> starts the consumer thread</li>
		</ul>
	<li> Stop Threads</li>
		<ul>
			<li> <strong>`producerThread.join()`</strong> waits for the producer thread to finish</li>
			<li> <strong>`consumerThread.join()`</strong> waits for the consumer thread to finish</li>
		</ul>
	<li> Exit message</li>
		<ul>
			<li> <strong>`System.out.println("exiting thread)`</strong> indicates the thread is stopping</li>
		</ul>
</ol>

<h2> 5. Important Concepts for This Lesson </h2> 
<ol>

<li> Multithreading</li>
	<ul>
			<li> Multithreading allows concurrent execution of two or more parts of a program to maximize the utilization of the CPU. Each part of such program is called a thread, and threads are lightweight processes within a process.
			</li>
			<li> In this exercise we used threads to run the producer and the consumer concurrently
			</li>
	</ul>
<li> Synchronization</li>
	<ul>
			<li> Is a technique used to control the access to multiple threads to shared resources. Without it, it is possible for one thread to modify a shared resource while another thread is in the middle of using or updating it.
			</li>
			<li>
			in this exercise we synchronize the `add` and `remove` methods to ensure only one thread can be modify the buffer at a time.
			</li>
	</ul>
<li> Inter-Thread Communication (wait/notify)</li>
	<ul>
			<li> 
			the `wait` and `notify` methods are used in inter=tread communication in JAVA. the `wait` method tells the calling thread to give up the lock and go to slee until some other thread enters the same monitor and calls `notify`. The `notify` method wakes up a single thread that is waiting on the objects monitor
			</li>
			<li>
				In this exercise, the producer calls `wait` if the buffer is full, and the consumer calls `wait` of the buffer is empty. `notifyAll` is called after adding or removing an item to wake up the waiting threads
	</ul>
<li> Thread Control (start, join, interrupt)</li>
	<ul>
			<li>
			`start()` begins the execution of the thread
			</li>
			<li>
			`join()` waits for a thread to finish
			</li>
			<li>
			`interrupt()` interrupts a thread, usually used to stop a thread.
			</li>
			<li>
			in this exercise, `start()` begins the execution of the producer and consumer threads. `join()` ensures  the main thread waits until the producer and consumer thread to finish before exiting. `interrupt()` handles the interruptions.
	</ul>
<li> Volatile Keyword</li>
	<ul>
			<li>
			The `volatile` keyword in JAVA is used to indicate that a variable's value will be modified by different threads. Declaring a variable as `volatile` ensures that its value is always read from the main memory and not from the threads local chache.
			</li>
			<li> 
				In this exercise the `running` flag in the producer and consumer is marked as `volatile` to ensure visibility across threads
				</li>
	</ul>
</o>

<h2> 6. Step By Step Instructions </h2>

### Building the Solution from Scratch

Now, let's build the solution step by step, considering the key concepts.

#### Step 1: SharedBuffer Class

1. **Create the class and necessary imports**:
    ```java
    import java.util.LinkedList;
    import java.util.Queue;

    public class SharedBuffer {
        private final Queue<Integer> buffer;
        private final int maxSize;
    ```

2. **Constructor to initialize the buffer**:
    ```java
        public SharedBuffer(int maxSize) {
            this.buffer = new LinkedList<>();
            this.maxSize = maxSize;
        }
    ```

3. **Synchronized add method**:
    ```java
        public synchronized void add(int value) throws InterruptedException {
            while (buffer.size() == maxSize) {
                wait(); // Wait if the buffer is full
            }
            buffer.add(value);
            notifyAll(); // Notify all waiting threads
        }
    ```

4. **Synchronized remove method**:
    ```java
        public synchronized int remove() throws InterruptedException {
            while (buffer.isEmpty()) {
                wait(); // Wait if the buffer is empty
            }
            int value = buffer.remove();
            notifyAll(); // Notify all waiting threads
            return value;
        }
    }
    ```

#### Step 2: Producer Class

1. **Create the class and necessary imports**:
    ```java
    import java.util.Random;

    public class Producer implements Runnable {
        private final SharedBuffer sharedBuffer;
        private final Random random;
        private volatile boolean running = true;
    ```

2. **Constructor to initialize shared buffer and random generator**:
    ```java
        public Producer(SharedBuffer sharedBuffer) {
            this.sharedBuffer = sharedBuffer;
            this.random = new Random();
        }
    ```

3. **Run method to continuously produce numbers**:
    ```java
        @Override
        public void run() {
            while (running) {
                try {
                    int value = random.nextInt(100);
                    sharedBuffer.add(value);
                    System.out.println("Produced: " + value);
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                    break;
                }
            }
        }
    ```

4. **Stop method to stop the thread**:
    ```java
        public void stop() {
            running = false;
        }
    }
    ```

#### Step 3: Consumer Class

1. **Create the class**:
    ```java
    public class Consumer implements Runnable {
        private final SharedBuffer sharedBuffer;
        private volatile boolean running = true;
    ```

2. **Constructor to initialize shared buffer**:
    ```java
        public Consumer(SharedBuffer sharedBuffer) {
            this.sharedBuffer = sharedBuffer;
        }
    ```

3. **Run method to continuously consume numbers**:
    ```java
        @Override
        public void run() {
            int sum = 0;
            while (running) {
                try {
                    int value = sharedBuffer.remove();
                    sum += value;
                    System.out.println("Consumed: " + value + " | Current Sum: " + sum);
                    Thread.sleep(150);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                    break;
                }
            }
        }
    ```

4. **Stop method to stop the thread**:
    ```java
        public void stop() {
            running = false;
        }
    }
    ```

#### Step 4: Main Class

1. **Create the class**:
    ```java
    public class Main {
    ```

2. **Main method to create and start threads**:
    ```java
        public static void main(String[] args) {
            SharedBuffer sharedBuffer = new SharedBuffer(10);

            Producer producer = new Producer(sharedBuffer);
            Consumer consumer = new Consumer(sharedBuffer);

            Thread producerThread = new Thread(producer);
            Thread consumerThread = new Thread(consumer);

            producerThread.start();
            consumerThread.start();

            try {
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }

            producer.stop();
            consumer.stop();

            try {
                producerThread.join();
                consumerThread.join();
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }

            System.out.println("Main thread exiting.");
        }
    }
    ```

### Summary

By breaking down the code into smaller steps and explaining each concept, you should have a clearer understanding of how the producer-consumer problem is implemented in Java. The key concepts of multithreading, synchronization, inter-thread communication, thread control, and the `volatile` keyword are essential for ensuring that the producer and consumer work together correctly without any race conditions or data inconsistencies.

