# CPU

**The Central Processing Unit - the CPU is the brain of the computer.**

This is a major resource in the computer and various things compete for it's attention.

## Processes and Applications

The most obvious competitors for CPU time are the **multiple processes and applications** running on a computer. Each program—whether it’s a browser, word processor, media player, or system tool—needs computations to be performed, which requires CPU cycles. Modern operating systems use a **scheduler** to allocate CPU time to each process, often using strategies like round-robin, priority-based, or multilevel queue scheduling. When many demands are made on the CPU, it must rapidly switch between them—a process called **multitasking**—to ensure all programs make progress.

*Example:* If you’re streaming a video, downloading a file, and running a virus scan at the same time, each of these tasks is a competing process vying for CPU resources.

## Interrupts and Hardware Devices

**Hardware devices**—such as keyboards, mice, printers, network cards, and storage drives—often generate **interrupts** to signal the CPU that they require immediate attention. For instance, a network card receiving data, or a keyboard registering a keypress, can send an interrupt. The CPU must momentarily stop what it’s doing (pause the current process) to service these high-priority requests, which can create competition for the CPU’s time, particularly if there are frequent or simultaneous interrupts from multiple devices.

*Example:* While you’re playing a game, your network card may generate interrupts to process incoming chat messages, and a USB drive might signal that a file copy is complete—each diverting CPU focus from the main gameplay.


## Operating System Services & Background Tasks
Beyond user-launched applications, the **operating system itself and background services** constantly require CPU attention. These include functions such as memory management, file system operations, system updates, security scanning, indexing files for search, and handling system events. Background tasks, although often invisible to the user, compete with active applications for CPU cycles.

*Example:* While you’re editing a document, the operating system may simultaneously run background updates, system health checks, and index files—all of which can momentarily consume CPU resources and impact application performance.

## In summary  

The CPU is continuously in demand from processes/applications, hardware device interrupts, and background OS tasks. Managing this competition is a central role of the operating system, ensuring that the CPU is used efficiently and that all tasks receive fair attention.

