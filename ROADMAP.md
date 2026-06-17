# Roadmap

## 001. Node.js Runtime Environment

Create a script that outputs the Node.js version, V8, libuv, platform, architecture, CPU count, and available memory. Record the environment in which the experiments are performed.

## 002. Node.js Process Lifecycle

Research the startup and shutdown of a Node.js process. Check the `beforeExit` and `exit` events, active handles, and the reasons why the process may not terminate.

## 003. Event Loop Phases

Implement an experiment showing the main event loop phases: timers, pending callbacks, poll, check, and close callbacks. Record the order of operation execution.

## 004. Microtasks and Macrotasks

Compare the execution of `Promise.then`, `queueMicrotask`, `process.nextTick`, `setTimeout`, and `setImmediate`. Show the actual execution order.

## 005. setTimeout and setImmediate

Compare `setTimeout(0)` and `setImmediate()` at the top level of the program and inside an I/O callback. Explain the differences in execution order.

## 006. process.nextTick Starvation

Create a recursive `process.nextTick()` chain and show how it blocks timers and I/O. Implement a safe version that yields control to the event loop.

## 007. Microtask Starvation

Create a long Promise or `queueMicrotask` chain and measure its impact on timers, I/O, and event loop delay.

## 008. Timer Accuracy and Drift

Research the accuracy of `setTimeout` and the accumulation of delay in `setInterval`. Implement a timer with drift compensation.

## 009. Blocking the Event Loop

Create a CPU-bound operation in the main thread. Measure its impact on latency, throughput, timers, and event loop delay.

## 010. libuv Thread Pool

Research operations that use the thread pool: file system, crypto, zlib, and DNS. Show the difference from regular network I/O.

## 011. Thread Pool Saturation

Run a large number of file and crypto operations simultaneously. Measure latency and the impact of thread pool saturation.

## 012. UV_THREADPOOL_SIZE

Compare performance with different `UV_THREADPOOL_SIZE` values. Record throughput, latency, CPU, and the limitations of increasing the pool.

## 013. Async Hooks

Use `async_hooks` to track the creation, execution, and destruction of asynchronous resources. Output `asyncId`, `triggerAsyncId`, and the resource type.

## 014. Async Resource Graph

Build a graph of asynchronous dependencies between Promise, timers, I/O, and other resources. Save the result as JSON or Graphviz DOT.

## 015. AsyncLocalStorage

Implement an execution context with `requestId`, `operationId`, and operation start time. Check context propagation through Promise, timers, and I/O.

## 016. AbortController and Cancellation

Implement cancellation of timers, streams, and long-running asynchronous operations through `AbortController` and `AbortSignal`.

## 017. Asynchronous Error Handling

Research `unhandledRejection`, `uncaughtException`, EventEmitter errors, streams, and async callbacks. Record process termination rules after critical errors.

## 018. Buffer Allocation

Compare `Buffer.alloc()` and `Buffer.allocUnsafe()`. Research performance, memory initialization, and security.

## 019. Buffer Encodings

Research UTF-8, ASCII, Base64, Hex, and other encodings. Compare string length, byte count, and the behavior of multibyte characters.

## 020. Buffer Memory Sharing

Compare `Buffer.slice`, `Buffer.subarray`, `Buffer.from`, and data copying. Show cases of shared memory usage.

## 021. Buffer and Typed Arrays

Compare `Buffer`, `Uint8Array`, `ArrayBuffer`, and `DataView`. Research conversions, byte offsets, and endianness.

## 022. Binary Protocol

Implement a simple binary protocol with a header, version, message type, payload length, and checksum. Add an encoder, decoder, and validation.

## 023. Custom Readable Stream

Implement a custom `Readable` stream. Research `_read`, `push`, flowing mode, paused mode, and the internal buffer.

## 024. Custom Writable Stream

Implement a custom `Writable` stream. Research `_write`, the write queue, `drain`, `finish`, and backpressure.

## 025. Stream Backpressure

Create a fast producer and a slow consumer. Compare processing with and without backpressure. Measure memory usage.

## 026. Stream highWaterMark

Check the impact of `highWaterMark` on throughput, latency, memory, and the frequency of backpressure.

## 027. Transform Streams

Implement a `Transform` stream for streaming processing of JSON Lines or a large text file without loading it entirely into memory.

## 028. Stream Pipeline and Errors

Compare manual `pipe()` and `stream.pipeline()`. Research error propagation, resource closing, and pipeline cancellation.

## 029. Buffered and Streaming Processing

Process a large file through `fs.readFile` and through streams. Compare execution time, RSS, heap usage, and time to the first processed block.

## 030. Worker Threads

Move a CPU-bound operation from the main thread to `worker_threads`. Compare event loop delay, latency, and total execution time.

## 031. Worker Startup Cost

Measure the cost of creating a worker, loading a module, passing a message, and terminating the worker.

## 032. Worker Data Transfer

Compare structured clone and transferable objects when transferring large `ArrayBuffer` instances between threads.

## 033. SharedArrayBuffer and Atomics

Implement a shared counter or a small queue through `SharedArrayBuffer` and `Atomics`. Show a race condition and synchronization.

## 034. Worker Thread Pool

Implement a fixed worker thread pool with a task queue, identifiers, Promise API, errors, timeouts, and graceful shutdown.

## 035. Worker Failures

Handle worker errors, unexpected exit, timeout, stuck tasks, and automatic replacement of a terminated worker.

## 036. Child Processes

Compare `spawn`, `exec`, `execFile`, and `fork`. Research shell usage, buffering, streaming stdout, IPC, and security.

## 037. Process IPC

Implement message exchange between a parent and child Node.js process. Add commands, results, heartbeat, and error handling.

## 038. Clustered HTTP Server

Create an HTTP server through `cluster`. Compare one process and multiple workers by throughput, latency, and CPU utilization.

## 039. Cluster Worker Supervision

Implement worker state monitoring, restart after failure, restart count limits, and crash loop protection.

## 040. Graceful Cluster Restart

Implement sequential restart of cluster workers without interrupting active requests.

## 041. Node.js Memory Metrics

Research `rss`, `heapUsed`, `heapTotal`, `external`, and `arrayBuffers`. Show the differences between the V8 heap and total process memory.

## 042. Closure Memory Leak

Create a memory leak through a closure. Find retained objects through a heap snapshot and fix the problem.

## 043. Unbounded Cache Leak

Create an unbounded cache through `Map`. Add TTL, a maximum size, and removal of old entries.

## 044. EventEmitter and Timer Leaks

Create leaks through listeners and `setInterval`. Find the causes of memory growth and correctly release resources.

## 045. Buffer Memory Leak

Create a scenario of growing `external` memory and RSS with stable `heapUsed`. Research retained Buffer objects.

## 046. Heap Snapshots

Take heap snapshots before and after load. Find dominators, retaining paths, and object types whose count increases.

## 047. Garbage Collection

Research minor GC, major GC, object promotion, and GC pauses. Check the impact of intensive memory allocation and heap limits.

## 048. Out of Memory

Create a controlled OOM scenario with a limited heap. Record process behavior, diagnostic output, and exit code.

## 049. CPU Profiling

Create a CPU-bound load and capture a CPU profile. Find hot paths, optimize the code, and compare results before and after.

## 050. Event Loop Delay

Measure event loop delay while idle, under CPU load, and under I/O load. Record average values and percentiles.

## 051. Event Loop Utilization

Measure event loop utilization for CPU-bound, I/O-bound, and worker-thread scenarios. Compare it with regular CPU usage.

## 052. Performance Hooks

Use `performance.mark`, `performance.measure`, and `PerformanceObserver` to measure internal operations.

## 053. Diagnostic Reports

Generate `process.report` on a signal or critical error. Research the stack trace, active handles, memory, and runtime information.

## 054. Diagnostics Channel

Use `diagnostics_channel` to publish internal runtime events without a direct dependency on a logger or tracer.

## 055. Active Handles

Create unclosed timers, sockets, servers, workers, and file handles. Find the causes of a hanging process shutdown.

## 056. Graceful Shutdown

Implement correct process termination on `SIGTERM` and `SIGINT`. Close the HTTP server, streams, workers, timers, and active operations.

## 057. Benchmark Runner

Create a common benchmark runner with warm-up, repetitions, median, mean, percentiles, and standard deviation.

## 058. Benchmark Reliability

Show the impact of JIT warm-up, garbage collection, sample size, and background load on benchmark results.

## 059. Buffer Benchmark

Compare the performance of allocation, copy, slice, concat, encoding, and decoding for Buffer.

## 060. Streams Benchmark

Compare different chunk sizes and `highWaterMark`. Measure throughput, latency, CPU, and memory usage.

## 061. Concurrency Benchmark

Compare sequential execution, `Promise.all`, limited concurrency, and adaptive concurrency.

## 062. Worker Pool Benchmark

Compare the execution of CPU tasks in the main thread and in a worker pool. Determine the approximate point after which using a worker becomes beneficial.

## 063. Runtime Diagnostics Module

Build a module that provides memory usage, CPU usage, event loop delay, event loop utilization, uptime, and runtime versions.

## 064. Streaming Processing Engine

Implement a streaming pipeline for a large file with parsing, validation, transformation, progress, cancellation, and bounded memory.

## 065. CPU Task Engine

Implement a local CPU task engine based on a worker pool with a queue, priorities, timeout, cancellation, metrics, and graceful shutdown.

## 066. Production Incident Investigation

Simulate a production incident with increasing latency, memory usage, or event loop delay. Perform diagnostics, find the root cause, fix the problem, and prepare a technical report.
