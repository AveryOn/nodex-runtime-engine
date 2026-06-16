# Roadmap

## 001. Node.js Runtime Environment

Сделать скрипт, который выводит версию Node.js, V8, libuv, платформу, архитектуру, количество CPU и доступную память. Зафиксировать окружение, в котором выполняются эксперименты.

## 002. Node.js Process Lifecycle

Исследовать запуск и завершение Node.js-процесса. Проверить события `beforeExit`, `exit`, активные handles и причины, по которым процесс может не завершаться.

## 003. Event Loop Phases

Реализовать эксперимент, показывающий основные фазы event loop: timers, pending callbacks, poll, check и close callbacks. Зафиксировать порядок выполнения операций.

## 004. Microtasks and Macrotasks

Сравнить выполнение `Promise.then`, `queueMicrotask`, `process.nextTick`, `setTimeout` и `setImmediate`. Показать реальный порядок выполнения.

## 005. setTimeout and setImmediate

Сравнить `setTimeout(0)` и `setImmediate()` на верхнем уровне программы и внутри I/O callback. Объяснить различия в порядке выполнения.

## 006. process.nextTick Starvation

Создать рекурсивную цепочку `process.nextTick()` и показать, как она блокирует timers и I/O. Реализовать безопасный вариант с передачей управления event loop.

## 007. Microtask Starvation

Создать длинную цепочку Promise или `queueMicrotask` и измерить её влияние на timers, I/O и event loop delay.

## 008. Timer Accuracy and Drift

Исследовать точность `setTimeout` и накопление задержки в `setInterval`. Реализовать таймер с компенсацией drift.

## 009. Blocking the Event Loop

Создать CPU-bound операцию в основном потоке. Измерить её влияние на latency, throughput, timers и event loop delay.

## 010. libuv Thread Pool

Исследовать операции, использующие thread pool: файловую систему, crypto, zlib и DNS. Показать отличие от обычного сетевого I/O.

## 011. Thread Pool Saturation

Запустить большое количество файловых и crypto-операций одновременно. Измерить latency и влияние насыщения thread pool.

## 012. UV_THREADPOOL_SIZE

Сравнить производительность при разных значениях `UV_THREADPOOL_SIZE`. Зафиксировать throughput, latency, CPU и ограничения увеличения пула.

## 013. Async Hooks

Использовать `async_hooks` для отслеживания создания, выполнения и уничтожения асинхронных ресурсов. Выводить `asyncId`, `triggerAsyncId` и тип ресурса.

## 014. Async Resource Graph

Построить граф асинхронных зависимостей между Promise, timers, I/O и другими ресурсами. Сохранять результат в JSON или Graphviz DOT.

## 015. AsyncLocalStorage

Реализовать контекст выполнения с `requestId`, `operationId` и временем начала операции. Проверить передачу контекста через Promise, timers и I/O.

## 016. AbortController and Cancellation

Реализовать отмену timers, streams и длительных асинхронных операций через `AbortController` и `AbortSignal`.

## 017. Asynchronous Error Handling

Исследовать `unhandledRejection`, `uncaughtException`, ошибки EventEmitter, streams и async callbacks. Зафиксировать правила завершения процесса после критических ошибок.

## 018. Buffer Allocation

Сравнить `Buffer.alloc()` и `Buffer.allocUnsafe()`. Исследовать производительность, инициализацию памяти и безопасность.

## 019. Buffer Encodings

Исследовать UTF-8, ASCII, Base64, Hex и другие кодировки. Сравнить длину строки, количество байтов и поведение многобайтовых символов.

## 020. Buffer Memory Sharing

Сравнить `Buffer.slice`, `Buffer.subarray`, `Buffer.from` и копирование данных. Показать случаи совместного использования памяти.

## 021. Buffer and Typed Arrays

Сравнить `Buffer`, `Uint8Array`, `ArrayBuffer` и `DataView`. Исследовать преобразования, byte offsets и endianness.

## 022. Binary Protocol

Реализовать простой бинарный протокол с заголовком, версией, типом сообщения, длиной payload и checksum. Добавить encoder, decoder и валидацию.

## 023. Custom Readable Stream

Реализовать собственный `Readable` stream. Исследовать `_read`, `push`, flowing mode, paused mode и внутренний буфер.

## 024. Custom Writable Stream

Реализовать собственный `Writable` stream. Исследовать `_write`, очередь записи, `drain`, `finish` и backpressure.

## 025. Stream Backpressure

Создать быстрый producer и медленный consumer. Сравнить обработку с учётом backpressure и без неё. Измерить использование памяти.

## 026. Stream highWaterMark

Проверить влияние `highWaterMark` на throughput, latency, память и частоту возникновения backpressure.

## 027. Transform Streams

Реализовать `Transform` stream для потоковой обработки JSON Lines или большого текстового файла без полной загрузки в память.

## 028. Stream Pipeline and Errors

Сравнить ручной `pipe()` и `stream.pipeline()`. Исследовать распространение ошибок, закрытие ресурсов и отмену pipeline.

## 029. Buffered and Streaming Processing

Обработать большой файл через `fs.readFile` и через streams. Сравнить время выполнения, RSS, heap usage и время до первого обработанного блока.

## 030. Worker Threads

Перенести CPU-bound операцию из основного потока в `worker_threads`. Сравнить event loop delay, latency и общее время выполнения.

## 031. Worker Startup Cost

Измерить стоимость создания worker, загрузки модуля, передачи сообщения и завершения worker.

## 032. Worker Data Transfer

Сравнить structured clone и transferable objects при передаче больших `ArrayBuffer` между потоками.

## 033. SharedArrayBuffer and Atomics

Реализовать общий счётчик или небольшую очередь через `SharedArrayBuffer` и `Atomics`. Показать race condition и синхронизацию.

## 034. Worker Thread Pool

Реализовать фиксированный пул worker threads с очередью задач, идентификаторами, Promise API, ошибками, таймаутами и graceful shutdown.

## 035. Worker Failures

Обработать ошибки worker, неожиданный exit, timeout, зависшие задачи и автоматическую замену завершившегося worker.

## 036. Child Processes

Сравнить `spawn`, `exec`, `execFile` и `fork`. Исследовать shell, buffering, streaming stdout, IPC и безопасность.

## 037. Process IPC

Реализовать обмен сообщениями между родительским и дочерним Node.js-процессом. Добавить команды, результаты, heartbeat и обработку ошибок.

## 038. Clustered HTTP Server

Создать HTTP-сервер через `cluster`. Сравнить один процесс и несколько workers по throughput, latency и загрузке CPU.

## 039. Cluster Worker Supervision

Реализовать контроль состояния workers, перезапуск после падения, ограничение количества рестартов и защиту от crash loop.

## 040. Graceful Cluster Restart

Реализовать последовательный перезапуск cluster workers без обрыва активных запросов.

## 041. Node.js Memory Metrics

Исследовать `rss`, `heapUsed`, `heapTotal`, `external` и `arrayBuffers`. Показать различия между V8 heap и общей памятью процесса.

## 042. Closure Memory Leak

Создать утечку памяти через замыкание. Найти удерживаемые объекты через heap snapshot и исправить проблему.

## 043. Unbounded Cache Leak

Создать неограниченный cache через `Map`. Добавить TTL, максимальный размер и удаление старых записей.

## 044. EventEmitter and Timer Leaks

Создать утечки через listeners и `setInterval`. Найти причины роста памяти и корректно освободить ресурсы.

## 045. Buffer Memory Leak

Создать сценарий роста `external` memory и RSS при стабильном `heapUsed`. Исследовать удержание Buffer-объектов.

## 046. Heap Snapshots

Снять heap snapshots до нагрузки и после неё. Найти dominators, retaining paths и типы объектов, количество которых увеличивается.

## 047. Garbage Collection

Исследовать minor GC, major GC, promotion объектов и GC pauses. Проверить влияние интенсивного выделения памяти и heap limits.

## 048. Out of Memory

Создать контролируемый OOM-сценарий с ограниченным heap. Зафиксировать поведение процесса, diagnostic output и exit code.

## 049. CPU Profiling

Создать CPU-bound нагрузку и снять CPU profile. Найти hot paths, оптимизировать код и сравнить результаты до и после.

## 050. Event Loop Delay

Измерить event loop delay в idle-режиме, под CPU-нагрузкой и под I/O-нагрузкой. Зафиксировать средние значения и percentiles.

## 051. Event Loop Utilization

Измерить event loop utilization для CPU-bound, I/O-bound и worker-thread сценариев. Сравнить с обычным CPU usage.

## 052. Performance Hooks

Использовать `performance.mark`, `performance.measure` и `PerformanceObserver` для измерения внутренних операций.

## 053. Diagnostic Reports

Генерировать `process.report` при сигнале или критической ошибке. Исследовать stack trace, active handles, память и runtime information.

## 054. Diagnostics Channel

Использовать `diagnostics_channel` для публикации внутренних runtime-событий без прямой зависимости от logger или tracer.

## 055. Active Handles

Создать незакрытые timers, sockets, servers, workers и файловые handles. Найти причины зависшего завершения процесса.

## 056. Graceful Shutdown

Реализовать корректное завершение процесса по `SIGTERM` и `SIGINT`. Закрыть HTTP server, streams, workers, timers и активные операции.

## 057. Benchmark Runner

Создать общий инструмент запуска benchmarks с warm-up, повторениями, median, mean, percentiles и standard deviation.

## 058. Benchmark Reliability

Показать влияние JIT warm-up, garbage collection, размера выборки и фоновой нагрузки на результаты benchmark.

## 059. Buffer Benchmark

Сравнить производительность allocation, copy, slice, concat, encoding и decoding для Buffer.

## 060. Streams Benchmark

Сравнить разные размеры chunks и `highWaterMark`. Измерить throughput, latency, CPU и memory usage.

## 061. Concurrency Benchmark

Сравнить последовательное выполнение, `Promise.all`, ограниченную concurrency и adaptive concurrency.

## 062. Worker Pool Benchmark

Сравнить выполнение CPU-задач в main thread и worker pool. Определить примерную точку, после которой использование worker становится выгодным.

## 063. Runtime Diagnostics Module

Собрать модуль, который предоставляет memory usage, CPU usage, event loop delay, event loop utilization, uptime и runtime versions.

## 064. Streaming Processing Engine

Реализовать потоковый pipeline для большого файла с parsing, validation, transformation, progress, cancellation и bounded memory.

## 065. CPU Task Engine

Реализовать локальный движок CPU-задач на основе worker pool с очередью, приоритетами, timeout, cancellation, metrics и graceful shutdown.

## 066. Production Incident Investigation

Смоделировать production-инцидент с ростом latency, памяти или event loop delay. Провести диагностику, найти root cause, исправить проблему и оформить технический отчёт.
