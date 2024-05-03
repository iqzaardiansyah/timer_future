<details>
<summary>Tutorial 1 Module 10</summary>

<details>
<summary>1.2. Understanding how it works.</summary>

![1.2. Understanding how it works.](https://i.ibb.co/dpVNrnq/gambar-2024-05-03-091352792.png)
Based on the screenshot, `println!("Iqza's Komputer: hey hey");` is executed immediately after spawning the asynchronous task with `spawner.spawn(async { ... });`. This statement doesn't wait for the asynchronous task to complete; instead, it continues to execute immediately after the task is spawned.

Meanwhile, the asynchronous task `async { ... }` includes `TimerFuture::new(Duration::new(2, 0)).await;`, which creates a timer future that waits for 2 seconds before completing. This means that after the message "Iqza's Komputer: hey hey" is printed, the task waits for 2 seconds due to the timer before printing "Iqza's Komputer: howdy!" and "Iqza's Komputer: done!".

So, "Iqza's Komputer: hey hey" is printed first because it's immediately executed, while the other messages are printed after the asynchronous task completes after a 2-second delay.

</details>

</details>