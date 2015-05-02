![](docs/logjammin.gif)

This is a plugin which modify an existing task, such that it will print a formatted thread dump if your program is stuck in one place for too long.  This is especially useful in CI environments where you are not able to run `jstack` directly on the process.

```
lein jammin <seconds> test
```

If none of the threads in your tests are active for the specified duration, then it will print out a series of stack traces like this, with the historically most active thread first:

```
 == Things seem to be stuck. ==


main

                                                              sun.misc.Unsafe.park                      Unsafe.java
                                       java.util.concurrent.locks.LockSupport.park                 LockSupport.java:  186
       java.util.concurrent.locks.AbstractQueuedSynchronizer.parkAndCheckInterrupt  AbstractQueuedSynchronizer.java:  834
java.util.concurrent.locks.AbstractQueuedSynchronizer.doAcquireSharedInterruptibly  AbstractQueuedSynchronizer.java:  994
  java.util.concurrent.locks.AbstractQueuedSynchronizer.acquireSharedInterruptibly  AbstractQueuedSynchronizer.java: 1303
                                         java.util.concurrent.CountDownLatch.await              CountDownLatch.java:  236
                                                  clojure.core/promise/reify/deref                         core.clj: 6553
                                                                clojure.core/deref                         core.clj: 2200
...
```

To use this plugin, add this to your `project.clj`:


```clj
:plugins [[lein-jammin "0.1.0"]]
```

### license

Copyright © 2015 Zach Tellman

Distributed under the MIT License.
