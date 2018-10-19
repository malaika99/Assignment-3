/******************************************************************************

                        

#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

int data[1000];
int size=100;

void * addition(void *index)
{
    int start=(int)index;
    int end= start+size;
    int sum=0;
    for (int i=start; i<end; i++)
    {
        sum= sum + data[i];
    }
    return((void*)sum);
}

int main()
{
    int sum=0; 
    int status[10];
    pthread_t thread[10];
    for (int i=0; i<1000; i++)
            data[i]=i;
    for(int i=0; i<10; i++)
    {
        pthread_create(&thread[i], NULL, addition, (void*)(i*size));  
    }
    for (int i=0; i<10; i++)
    {
        pthread_join(thread[i],(void**) &status[i]);
    }
    for (int i=0; i<10; i++)
    {
        sum=sum+status[i];
    }
    printf("%d",sum);

    return 0;
}


