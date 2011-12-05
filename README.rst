===============================================================================
bloomfilter-redis - Easy + Time series bloom filters backed by redis bitvectors
===============================================================================

Overview
========

This is the little bloom filter we're using to filter unique views using redis.

It doesn't do anything special, but I didn't find any small and dependency-free 
bloom filter written in Python that use Redis as their backend.

Quick Benchmarks
================

Quick benchmark for ballpark figures on a MacbookPro (2x 2.66GHz) with Python 2.7,
hiredis and Redis 2.9 (unstable). Each benchmark was run with k=4 hashes per key.
Keys are random strings of 10 chars length:

Big filter with fewer values:
filling bloom filter of 1024.00kB size with 10k values
adding 10000 values took 2.09s (4790 values/sec, 208.73 us/value)
correct: 100000 / false: 0 -> 0% false positives

Small filter with a lot of values:
filling bloom filter of 500.00kB size with 100k values
adding 100000 values took 22.30s (4485 values/sec, 222.96 us/value)
correct: 100000 / false: 3 -> 0.003% false positives

4 parallel Python processes:
filling bloom filter of 1024.00kB size with 2M values
adding 2000000 values took 214.69s (9316 values/sec, 429.38 us/value)