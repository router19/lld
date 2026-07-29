Design a Job Scheduler (like cron or Quartz)
Pattern
PriorityQueue + Thread Pool + ReentrantLock
Approach
Entities: Job (id, priority, scheduledTime, Runnable task), JobScheduler, ThreadPool. Data structure: PriorityBlockingQueue sorted by scheduledTime. Scheduler thread: poll jobs due now, submit to thread pool. Handle: recurring jobs, cancellation, priority.workerPoolworkerPool