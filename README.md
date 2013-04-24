Leslie-Lamport
==============

Lamport's bakery algorithm is a computer algorithm devised by computer scientist Leslie Lamport, which is intended to improve the safety in the usage of shared resources among multiple threads by means of mutual exclusion.

Pseudocode


	
    // declaration and initial values of global variables
     Entering: array [1..NUM_THREADS] of bool = {false};
     Number: array [1..NUM_THREADS] of integer = {0};
 
  1  lock(integer i) {
  2      Entering[i] = true;
  3      Number[i] = 1 + max(Number[1], ..., Number[NUM_THREADS]);
  4      Entering[i] = false;
  5      for (j = 1; j <= NUM_THREADS; j++) {
  6          // Wait until thread j receives its number:
  7          while (Entering[j]) { /* nothing */ }
  8          // Wait until all threads with smaller numbers or with the same
  9          // number, but with higher priority, finish their work:
 10          while ((Number[j] != 0) && ((Number[j], j) < (Number[i], i))) { /* nothing */ }
 13      }
 14  }
 15  
 16  unlock(integer i) {
 17      Number[i] = 0;
 18  }
 19
 20  Thread(integer i) {
 21      while (true) {
 22          lock(i);
 23          // The critical section goes here...
 24          unlock(i);
 25          // non-critical section...
 26      }
 27  }
