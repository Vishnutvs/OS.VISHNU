#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>

#define NUM_THREADS 2

int shared_data = 10; // shared integer
sem_t mutex; // semaphore

void* thread1_func(void* arg) {
    int data;
    sem_wait(&mutex); // acquire lock
    data = shared_data; // read shared data
    shared_data = data * 2; // double the shared data
    printf("Thread 1: read %d, doubled it to %d\n", data, shared_data);
    sem_post(&mutex); // release lock
    pthread_exit(NULL);
}

void* thread2_func(void* arg) {
    int data;
    sem_wait(&mutex); // acquire lock
    data = shared_data; // read shared data
    shared_data = data * 5; // multiply the shared data by 5
    printf("Thread 2: read %d, multiplied it to %d\n", data, shared_data);
    sem_post(&mutex); // release lock
    pthread_exit(NULL);
}

int main() {
    pthread_t threads[NUM_THREADS];
    sem_init(&mutex, 0, 1); // initialize semaphore to 1

    // create threads
    pthread_create(&threads[0], NULL, thread1_func, NULL);
    pthread_create(&threads[1], NULL, thread2_func, NULL);

    // wait for threads to finish
    pthread_join(threads[0], NULL);
    pthread_join(threads[1], NULL);

    sem_destroy(&mutex); // destroy semaphore
    return 0;
}
output:

Thread 1: read 10, doubled it to 20
Thread 2: read 20, multiplied it to 100
