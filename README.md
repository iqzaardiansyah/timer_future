<details>
<summary>Tutorial 1 Module 10</summary>

<details>
<summary>1.2. Understanding how it works.</summary>

![1.2. Understanding how it works.](https://i.ibb.co/dpVNrnq/gambar-2024-05-03-091352792.png)
Based on the screenshot, `println!("Iqza's Komputer: hey hey");` is executed immediately after spawning the asynchronous task with `spawner.spawn(async { ... });`. This statement doesn't wait for the asynchronous task to complete; instead, it continues to execute immediately after the task is spawned.

Meanwhile, the asynchronous task `async { ... }` includes `TimerFuture::new(Duration::new(2, 0)).await;`, which creates a timer future that waits for 2 seconds before completing. This means that after the message "Iqza's Komputer: hey hey" is printed, the task waits for 2 seconds due to the timer before printing "Iqza's Komputer: howdy!" and "Iqza's Komputer: done!".

So, "Iqza's Komputer: hey hey" is printed first because it's immediately executed, while the other messages are printed after the asynchronous task completes after a 2-second delay.

</details>

<details>
<summary>1.3. Multiple Spawn and removing drop</summary>

![1.3. Multiple Spawn and removing drop 1](https://i.ibb.co/YySYnWf/gambar-2024-05-03-092309034.png)
![1.3. Multiple Spawn and removing drop 2](https://i.ibb.co/nfJynk7/gambar-2024-05-03-092557681.png)

When the line `drop(spawner);` is removed, the program does not stop because the `Executor`'s `run` method is waiting indefinitely for tasks to be sent through the `ready_queue`, but since the `spawner` is still alive, it keeps sending tasks, and none of them complete.

The `drop(spawner);` line is important because it signals the end of task spawning. When you drop the `spawner`, it closes the sending end of the channel, indicating that no more tasks will be sent. Consequently, the `Executor` eventually consumes all the tasks from the `ready_queue` and exits the `run` method when there are no more tasks to process.

Without `drop(spawner);`, the `Executor` remains blocked in its `run` method, waiting for more tasks to arrive, and the program does not terminate because there's no indication that it should stop waiting for tasks.
</details>

</details>