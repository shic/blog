---
layout:     post
title:      "C Programming Basic"
date:       2016-03-07 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# Compile
Always compile with

    -Wall -Wextra and perhaps even with -Werror -pedantic-errors 

    gcc -Wall -Wextra -O2 Bootstrap.c lista.c -o boot

## Eclipse 

### How to use math.h or pthread.h in Eclipse with gcc

You should add the -lm option to GCC C Linker, NOT TO GCC C Compiler:

Project -> Properties -> C/C++ Build -> Settings -> Tool Settings (tab) -> GCC C Linker -> in the "Command" text field type: "gcc -lm" (by default there is only "gcc").

Add it to the linker options, Libraries-> add it in as a new library "m", > this will automatically add on the -l to the option.

Debug 
gcc -g try.c -o try

gdb try
break 10
run [args]
p [variabile] // Print

# C 运算符优先级

1. . ->
2. ++ -- & *

Example: *p.f === *(p.f) === p->f

# Pass string to a function



# Pass array to a function

### C语言中，数组名作为参数传递给函数时，退化为指针；需要数组大小时，需要一个参数传数组名，另一个传数组大小。

```java
struct thread_data td[MAX_THREAD_NUM];

create_threads(td,MAX_THREAD_NUM);

void create_threads(struct thread_data *td, int MAX_THREAD_NUM){
	int i;
	for(i=0; i<MAX_THREAD_NUM; ++i){
		td[i].tid
	}
	
}

```

# Error handler

```java
# define abort_on_error ( cond , msg ) do { \
	if ( cond ) { \
		int _e = errno ; \
		fprintf ( stderr , "%s ", msg ) ; \
		fprintf ( stderr , "(%d)\n", _e ) ; \
		exit ( EXIT_FAILURE ) ; \
	} \
} while (0)
```

# Library

### fopen

```java
FILE *fopen(const char *filename, const char *mode)

mode: 
  "r":   Open text file for reading. 
  "r+":   Open for reading and writing. 
  "w":    Truncate to zero length or create text file for writing.  

Return Value
This function returns a FILE pointer. Otherwise, NULL is returned and the global variable errno is set to indicate the error.
```

### open

```
       int open(const char *pathname, int flags);
       int open(const char *pathname, int flags, mode_t mode);

flags must include one of the following access modes: O_RDONLY, O_WRONLY, or O_RDWR. These request opening the file read-only, write-only, or read/write, respectively.

mode specifies the permissions to use in case a new file is created. This argument must be supplied when O_CREAT is specified in flags; if O_CREAT is not specified, then mode is ignored. The effective permissions are modified by the process's umask in the usual way: The permissions of the created file are (mode & ~umask). Note that this mode only applies to future accesses of the newly created file; the open() call that creates a read-only file may well return a read/write file descriptor.

```



### fileno

```java
int fileno(FILE *stream)
  The function examines the argument stream and returns its integer descriptor.
```



## strtol

```java
long int strtol(const char *str, char **endptr, int base)

str -- This is the string containing the representation of an integral number.

endptr -- This is the reference to an object of type char*, whose value is set by the function to the next character in str after the numerical value.

base -- This is the base, which must be between 2 and 36 inclusive, or be the special value 0.

RETURN VALUE	
	This function returns the converted integral number as a long int value, else zero value is returned.
      
    char *endpointer;
	long long ll2, ll3;
	errno = 0;
	v = strtol(argv[1], &endpointer, 0);

	if (errno == 0 && *endpointer == '\0') {
		ll2 = v * v;
		ll3 = v * v * v;
		printf("qua %lld cubo = %lld", ll2, ll3);
	}
```

## malloc

`malloc()` is essentially implemented in terms of `mmap()`, but it's a sort of intelligent library wrapper around the system call

```java
void *malloc(size_t size);

RETURN VALUE	
	The malloc() and calloc() functions return a pointer to  the  allocated memory,  which  is  suitably  aligned for any built-in type.  On error, these functions return NULL.
```

## Pipe

### pipe() creates a pipe, a unidirectional data channel that can be used for interprocess communication. 

```java
int pipe(int pipefd[2]);

//The array pipefd is used to return two file descriptors referring to the ends of the pipe.  
pipefd[0] refers to the read end of the pipe.  
pipefd[1] refers to the write end of the pipe.  

RETURN VALUE	
       On success, zero is returned.  On error, -1 is returned, and errno is set appropriately.

```

## read

```java
ssize_t read(int fd, void *buf, size_t nbyte);

RETURN VALUE
    On success, the number of bytes read is returned (zero indicates end of file), On error, -1 is returned

```

## fscanf

```java
int fscanf(FILE *stream, const char *format, ...)

RETURN VALUE
    This function returns the number of input items successfully matched and assigned, which can be fewer than provided for, or even zero in the event of an early matching failure.
```

### scanf

The C library function **int scanf(const char \*format, ...)** reads formatted input from stdin.

## fgets

Reads a line from the specified stream and stores it into the string pointed to by str

```java
char *fgets(char *str, int n, FILE *stream)

RETURN VALUE

	On success, the function returns str. 
	If the End-of-File is encountered and no characters have been read, the contents of str remain unchanged and a null pointer is returned.

	If an error occurs, a null pointer is returned.

```
## Write

```java
ssize_t write(int fd, const void *buf, size_t count);

write() writes up to count bytes from the buffer pointed buf to the file referred to by the file descriptor fd.

RETURN VALUE
       On success, the number of bytes written is returned (zero indicates nothing was written).  On error, -1 is returned, and errno is set appropriately.
```

## memcpy

```java
void *memcpy(void *dest, const void *src, size_t n);

DESCRIPTION
       The memcpy() function copies n bytes from memory area src to memory area dest.  The memory areas must not overlap.  Use memmove(3) if the memory areas do overlap.

RETURN VALUE
       The memcpy() function returns a pointer to dest.

```

## Signal

### EINTR (Error interupt)

A signal primitive fail throw the error code for this kind of failure

### sigaction

examine and change a signal action

```java
int sigaction(
	int signum, 
	const struct sigaction *act,
	struct sigaction *oldact);

RETURN VALUE
	sigaction() returns 0 on success; on error, -1 is returned
       
```

## alarm

alarm() arranges for a SIGALRM signal to be delivered to the calling process in seconds seconds.

```java
unsigned int alarm(unsigned int seconds);

RETURN VALUE
       alarm() returns the number of seconds remaining until any previously scheduled alarm was due to be delivered, or zero if there was no previously scheduled alarm.

```

## pthread

### pthread_create

```java
int pthread_create(
	pthread_t *thread, 
	const pthread_attr_t *attr,
    void *(*start_routine) (void *), 
    void *arg);
    
On success, pthread_create() returns 0; on error, it returns an error number
      
//Usage
int ret = pthread_create(&thread_id_2, NULL, &thread2, NULL);

if (ret != 0) {
	printf("Unable to create thread2");
	exit(EXIT_FAILURE);
}
```

### fork

fork(): This function creates a new process. 

```java
fork()

RETURN VALUE
	The return value is the 0 in the child and the process-id number of the child in the parent, or -1 upon error. 
```

#Practice

## Pointer

 `char** x` and `char* x[]` are two ways of expressing *the same thing*. 

## File gestion

### Open file:

```java
FILE * open_file(char *path){
    FILE *f = fopen(path,"r");
    if (f == NULL){
   	 perror(path);
   	 exit(EXIT_FAILURE);
    }
    return f;
}

FILE *f;
int fd;
fd=fileno(f);
```

### Read file data

#### Per leggere il file di formato non nativo:

##### read value:

```java
int buf;
int rc;
FILE *f;
do{
  rc = fscanf(f, "%d", &buf);
  if(rc == 1){
    printf("buf %d", buf);
  }else{
    if( !feof(f) ){
       	 fprintf(stderr, "error while reading value \n");
       	 exit(EXIT_FAILURE);
	}
  }
    
}while(!feof(f));
```

##### read line:

```java
char *get_line(FILE *f){
    char *p;
    char *buf[MAX_LINE_LENGTH];
    p=fgets(buf,MAX_LINE_LENGTH,f);
    //puts(buf);
    //puts(p);
    return p;
}
```

#### Per leggere il file di formato nativo:

```c
ssize_t read(int fd, void *buf, size_t count);

int read_int(FILE *f){
    int buf,count;
    count = read(fileno(f), &buf, sizeof(buf));
    if (count == sizeof(buf)){
   		return buf;
    }
    fprintf(stderr,"error in read_int");
    exit(EXIT_FAILURE);
}


```

#### Read only the specific data：

```java
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>

int main(void) {
	char *p;
  	int n;
  	errno = 0;
//	n = scanf("%m[1-9]", &p);
  	n = scanf("%m[a-z]", &p);
  	if (n == 1) {
      	printf("read: %s\n", p);
      	free(p);
  	} else if (errno != 0) {
      	perror("scanf");
  	} else {
      	fprintf(stderr, "No matching characters\n");
  	}

    return EXIT_SUCCESS;
}
```

​	

###String

#### Count

```java
size_t strlen(const char *s);//Do not contain character end-of-string (\0)

    char s[100]="hi";
    char s1[]="world";
    ssize_t len=strlen(s);
    printf("%d \n",len);//2
    strcpy(result,s);
    strcat(s,s1);
    int a = strcmp(s,s1);
    printf("%s \n",s);//hiworld
```

### 

```java

```

### 

```java

```

### 

```java

```

### 

```java

```

### 

```java

```

### Print

```java
	if (argc < 2) {
        fprintf(stderr, "Usage: %s str [base]\n", argv[0]);
        exit(EXIT_FAILURE);
    }
```

### Convert input to number

```java
int main(int argc, char **argv) {
	int v;
	char *endpointer;
	long long ll2, ll3;
	if (argc < 2) {
		fprintf(stderr, "Usage: %s str [base]\n", argv[0]);
		exit(EXIT_FAILURE);
	}

	errno = 0;
	v = strtol(argv[1], &endpointer, 0);//strtol, strtoll, strtoq

	if (errno == 0 && *endpointer == '\0') {
		ll2 = v * v;
		ll3 = v * v * v;
		printf("qua %lld cubo = %lld", ll2, ll3);
	}
	return EXIT_SUCCESS;
}
```



### Function execl(), execle(), execv(), execve()

#### execl, execv 

L : variable argument list
V : as an array of char*
e : variabile di ambiente

### pipe()

int pipe(int pipefd[2])
pipefd[0]: un canale aperto in lettura
pipefd[1]: un canale aperto in scrittura



### MMAP

Allocazione dinamico. 

```java
FILE fd;

int *m;

m = mmap(NULL, rcsizeof(int), PROT_READ, MAP_PRIVATE,fd0,0);

if (NULL == m){

    perror("mmap");
    exit(EXIT_FAILURE);

}

```



## Using barriers in pthreads

To start thread execution together 

```java

	#include <stdio.h> 
	#include <pthread.h> 
	#include <stdlib.h>
	#include <unistd.h>
	
	int t1=0, t2=0, t3=0, t4=0;
	pthread_barrier_t our_barrier;
	
	void *thread1() {
		sleep(2);
		printf("Enter value for t1:  ");
		scanf("%d", &t1);
		pthread_barrier_wait(&our_barrier);
		printf("\nvalues entered by the threads are  %d %d %d %d \n", t1, t2, t3,
				t4);
	}
	
	void *thread2() {
		sleep(4);
	
		printf("Enter value for t2:  ");
		scanf("%d", &t2);
		pthread_barrier_wait(&our_barrier);
	
		printf("\nvalues entered by the threads are  %d %d %d %d \n", t1, t2, t3,
				t4);
	}
	
	void *thread3() {
	
		sleep(6);
	
		printf("Enter value for t3:  ");
		scanf("%d", &t3);
		pthread_barrier_wait(&our_barrier);
	
		printf("\nvalues entered by the threads are  %d %d %d %d \n", t1, t2, t3,
				t4);
	}
	
	void *thread4() {
	
		int temp;
		sleep(8);
	
		printf("Enter value for t4:  ");
		scanf("%d", &t4);
		pthread_barrier_wait(&our_barrier);
	
		printf("\nvalues entered by the threads are  %d %d %d %d \n", t1, t2, t3,
				t4);
	}
	
	int main() {
	
		pthread_t thread_id_1, thread_id_2, thread_id_3, thread_id_4;
		pthread_attr_t attr;
		int ret;
		void *res;
		pthread_barrier_init(&our_barrier, NULL, 3);
		ret = pthread_create(&thread_id_1, NULL, &thread1, NULL);
		if (ret != 0) {
			printf("Unable to create thread1");
		}
		
		ret = pthread_create(&thread_id_2, NULL, &thread2, NULL);
		if (ret != 0) {
			printf("Unable to create thread2");
		}
		
		ret = pthread_create(&thread_id_3, NULL, &thread3, NULL);
		if (ret != 0) {
			printf("Unable to create thread3");
		}
		
		ret = pthread_create(&thread_id_4, NULL, &thread4, NULL);
		if (ret != 0) {
			printf("Unable to create thread4");
		}
		printf("\n Created threads \n");
		pthread_join(thread_id_1, NULL);
		pthread_join(thread_id_2, NULL);
		pthread_join(thread_id_3, NULL);
		pthread_join(thread_id_4, NULL);
		pthread_barrier_destroy(&our_barrier);
		return EXIT_SUCCESS;
	
```

Pthread
   	int pthread_join ( pthread_t thread, void **retval);
The pthread_join() function waits for the thread specified by thread to terminate.

### MUTEX

```java
    int pthread_mutex_init(pthread_mutex_t *restrict mutex,const pthread_mutexattr_t *restrict attr);
DESCRIPTION
     The pthread_mutex_init() function creates a new mutex, with attributes
     specified with attr.  If attr is NULL, the default attributes are used.

RETURN VALUES
     If successful, pthread_mutex_init() will return zero and put the new
     mutex id into mutex.
```

### pthread_cond_init

```java
int pthread_cond_init(pthread_cond_t *restrict cond, const pthread_condattr_t *restrict attr);

DESCRIPTION
     The pthread_cond_init() function creates a new condition variable, with
     attributes specified with attr.  If attr is NULL, the default attributes
     are used.

RETURN VALUES
     If successful, the pthread_cond_init() function will return zero and put
     the new condition variable id into cond.  Otherwise, an error number will
     be returned to indicate the error.
```

int pthread_cond_wait(pthread_cond_t *restrict cond,pthread_mutex_t *restrict mutex);

DESCRIPTION
     The pthread_cond_wait() function atomically unlocks the mutex and blocks
     the current thread on the condition specified by the cond argument.  The
     current thread unblocks only after another thread calls
     pthread_cond_signal(3) or pthread_cond_broadcast(3) with the same condi-
     tion variable.  The mutex must be locked before calling this function,
     otherwise the behavior is undefined. Before pthread_cond_wait() returns
     to the calling function, it re-acquires the mutex.

RETURN VALUES
     If successful, the pthread_cond_wait() function will return zero; 


```java
int pthread_cond_signal(pthread_cond_t *cond);
```

DESCRIPTION
     The pthread_cond_signal() function unblocks one thread waiting for the
     condition variable cond.

RETURN VALUES
     If successful, the pthread_cond_signal() function will return zero.  


int pthread_mutex_lock(pthread_mutex_t *mutex);

DESCRIPTION
     The pthread_mutex_lock() function locks mutex.  If the mutex is already
     locked, the calling thread will block until the mutex becomes available.

RETURN VALUES
     If successful, pthread_mutex_lock() will return zero.  Otherwise, an
     error number will be returned to indicate the error.

 int
     pthread_mutex_unlock(pthread_mutex_t *mutex);

DESCRIPTION
     If the current thread holds the lock on mutex, then the
     pthread_mutex_unlock() function unlocks mutex.
    
     Calling pthread_mutex_unlock() with a mutex that the calling thread does
     not hold will result in undefined behavior.

RETURN VALUES
     If successful, pthread_mutex_unlock() will return zero.  


mutex_init cond_init(empty) cond_init(full)
