#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>

#define BUFFER_SIZE 3

int buffer[BUFFER_SIZE];
int count = 0; // the number of items in the buffer
int in = 0; // index for the next item to be produced
int out = 0; // index for the next item to be consumed

sem_t empty; // semaphore to indicate the number of empty slots in the buffer
sem_t full; // semaphore to indicate the number of full slots in the buffer
pthread_mutex_t mutex; // mutex to ensure exclusive access to the buffer

void *producer(void *arg) {
    int i, item;
    for (i = 0; i < 4; i++) {
        item = rand() % 100 + 1; // generate a random item
        sem_wait(&empty); // wait until there is an empty slot in the buffer
        pthread_mutex_lock(&mutex); // lock the buffer
        buffer[in] = item; // put the item in the buffer
        printf("Producer produced item %d at position %d\n", item, in);
        in = (in + 1) % BUFFER_SIZE; // update the index for the next item to be produced
        count++; // increase the count of items in the buffer
        pthread_mutex_unlock(&mutex); // unlock the buffer
        sem_post(&full); // signal that there is a new item in the buffer
    }
    pthread_exit(NULL);
}

void *consumer(void *arg) {
    int i, item;
    for (i = 0; i < 1; i++) {
        sem_wait(&full); // wait until there is a full slot in the buffer
        pthread_mutex_lock(&mutex); // lock the buffer
        item = buffer[out]; // get the item from the buffer
        printf("Consumer consumed item %d from position %d\n", item, out);
        out = (out + 1) % BUFFER_SIZE; // update the index for the next item to be consumed
        count--; // decrease the count of items in the buffer
        pthread_mutex_unlock(&mutex); // unlock the buffer
        sem_post(&empty); // signal that there is an empty slot in the buffer
    }
    pthread_exit(NULL);
}

int main() {
    pthread_t tid[2];
    pthread_mutex_init(&mutex, NULL);
    sem_init(&empty, 0, BUFFER_SIZE);
    sem_init(&full, 0, 0);
    printf("Consume an item in the beginning and show that the buffer is EMPTY\n");
    sem_wait(&full); // wait until there is a full slot in the buffer
    pthread_mutex_lock(&mutex); // lock the buffer
    int item = buffer[out]; // get the item from the buffer
    printf("Consumer consumed item %d from position %d\n", item, out);
    out = (out + 1) % BUFFER_SIZE; // update the index for the next item to be consumed
    count--; // decrease the count of items in the buffer
    pthread_mutex_unlock(&mutex); // unlock the buffer
    sem_post(&empty); // signal that there is an empty slot in the buffer
    printf("Produce 4 items and show that the buffer is FULL\n");
    pthread_create(&tid[0], NULL, producer, NULL);
    pthread_create(&tid[1], NULL, consumer, NULL);
    pthread_join(tid[0], NULL);
    pthread_join(tid[1], NULL);
    pthread_mutex_t
destroy(mutex);
sem_destroy(&empty);
sem_destroy(&full);
return 0;
}
output :
Consume an item in the beginning and show that the buffer is EMPTY
Consumer consumed item 76 from position 0
Produce 4 items and show that the buffer is FULL
Producer produced item 56 at position 0
Consumer consumed item 56 from position 0
Producer produced item 35 at position 1
Consumer consumed item 35 from position 1
Producer produced item 91 at position 2
Consumer consumed item 91 from position 2
Producer produced item 77 at position 0
Consumer consumed item 77 from position 0
