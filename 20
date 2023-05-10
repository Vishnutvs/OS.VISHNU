#include <stdio.h>

#define MAX_PARTITIONS 10
#define MAX_PROCESSES 10

int partitions[MAX_PARTITIONS];
int processes[MAX_PROCESSES];
int allocated[MAX_PROCESSES];

int main() {
    int np, mp;
    printf("Enter the number of memory partitions: ");
    scanf("%d", &np);
    printf("Enter the size of each memory partition:\n");
    for(int i=0; i<np; i++) {
        scanf("%d", &partitions[i]);
    }
    printf("Enter the number of processes: ");
    scanf("%d", &mp);
    printf("Enter the size of each process:\n");
    for(int i=0; i<mp; i++) {
        scanf("%d", &processes[i]);
    }

    // Worst-fit algorithm
    for(int i=0; i<mp; i++) {
        int index = -1;
        for(int j=0; j<np; j++) {
            if(partitions[j] >= processes[i]) {
                if(index == -1 || partitions[j] > partitions[index]) {
                    index = j;
                }
            }
        }
        if(index != -1) {
            allocated[i] = 1;
            partitions[index] -= processes[i];
        }
    }

    // Print allocation table
    printf("\nAllocation Table:\n");
    printf("Process\t\tSize\t\tPartition\tFragment\n");
    for(int i=0; i<mp; i++) {
        printf("%d\t\t%d KB\t\t", i+1, processes[i]);
        if(allocated[i]) {
            printf("%d\t\t%d KB\n", index+1, partitions[index]);
        }
        else {
            printf("Not allocated\t-\n");
        }
    }

    // Print remaining partitions
    printf("\nRemaining partitions:\n");
    for(int i=0; i<np; i++) {
        printf("Partition %d: %d KB\n", i+1, partitions[i]);
    }

    return 0;
}

output :

Enter the number of memory partitions: 6
Enter the size of each memory partition:
300
600
350
200
750
125
Enter the number of processes: 5
Enter the size of each process:
115
500
358
200
375

Allocation Table:
Process		Size		Partition	Fragment
1		115 KB		2		235 KB
2		500 KB		5		250 KB
3		358 KB		5		-108 KB
4		200 KB		1		100 KB
5		375 KB		5		-125 KB

Remaining partitions:
Partition 1: 100 KB
Partition 2: 600 KB
Partition 3: 350 KB
Partition 4: 0 KB
Partition 5: 250 KB
Partition 6: 125 KB
