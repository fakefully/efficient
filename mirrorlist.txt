// Write a C program to search an element in an Array using dynamic memory
// allocation. Apply different algorithm separately. Show the running time
// complexity w.r.t different input cases(best/average/worst). Finally comment
// that which one is better and why.

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Function to search using linear search
int linearSearch(int *arr, int n, int x)
{
    int i;
    for (i = 0; i < n; i++)
        if (arr[i] == x)
            return i;
    return -1;
}

// Function to search using binary search
int binarySearch(int *arr, int l, int r, int x)
{
    if (r >= l)
    {
        int mid = l + (r - l) / 2;
        if (arr[mid] == x)
            return mid;
        if (arr[mid] > x)
            return binarySearch(arr, l, mid - 1, x);
        return binarySearch(arr, mid + 1, r, x);
    }
    return -1;
}

int main()
{
    int n = 1000, i, j, x, result;
    int *arr;
    clock_t start, end;

    // Allocating memory dynamically
    arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 0;
    }

    // Initializing the array with random numbers
    srand(time(NULL));
    for (i = 0; i < n; i++)
        arr[i] = rand() % (n * 10);

    // Sorting the array
    int temp;
    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }

    // Linear Search: Best Case
    x = arr[0];
    start = clock();
    for (i = 0; i < 10000; i++)
        result = linearSearch(arr, n, x);
    end = clock();
    printf("Best case scenario for linear search: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Binary Search: Best Case
    start = clock();
    for (i = 0; i < 10000; i++)
        result = binarySearch(arr, 0, n - 1, x);
    end = clock();
    printf("Best case scenario for binary search: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Linear Search: Average Case
    x = arr[n / 2];
    start = clock();
    for (i = 0; i < 10000; i++)
        result = linearSearch(arr, n, x);
    end = clock();
    printf("Average case scenario for linear search: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Binary Search: Average Case
    start = clock();
    for (i = 0; i < 10000; i++)
        result = binarySearch(arr, 0, n - 1, x);
    end = clock();
    printf("Average case scenario for binary search: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Linear Search: Worst Case
    x = arr[n - 1];
    start = clock();
    for (i = 0; i < 10000; i++)
        result = linearSearch(arr, n, x);
    end = clock();
    printf("Worst case scenario for linear search: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Binary Search: Worst Case
    start = clock();
    for (i = 0; i < 10000; i++)
        result = binarySearch(arr, 0, n - 1, x);
    end = clock();
    printf("Worst case scenario for binary search: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    free(arr);
    return 0;
}

// OUTPUT
// Best case scenario for linear search: 0.00 ms
// Best case scenario for binary search: 0.00 ms
// Average case scenario for linear search: 17.00 ms
// Average case scenario for binary search: 2.00 ms
// Worst case scenario for linear search: 38.00 ms
// Worst case scenario for binary search: 1.00 ms

// Binary search is more efficient than linear search because
// it divides the search area in half with each iteration, reducing
// the amount of elements that need to be searched through.This
// results in a faster search time, especially as the size of
// the search area increases.

.........................................................................

# Write a Python program to search an element in an Array using
# dynamic memory allocation. Apply different algorithm separately.
# Show the running time complexity w.r.t different input cases(best/average/worst).

import random
import time

# Function to search using linear search


def linear_search(arr, x):
    for i in range(len(arr)):
        if arr[i] == x:
            return i
    return -1

# Function to search using binary search


def binary_search(arr, l, r, x):
    if r >= l:
        mid = l + (r - l) // 2
        if arr[mid] == x:
            return mid
        if arr[mid] > x:
            return binary_search(arr, l, mid - 1, x)
        return binary_search(arr, mid + 1, r, x)
    return -1


# Main function
if __name__ == "__main__":
    n = 1000
    arr = [random.randint(0, n*10) for i in range(n)]
    arr.sort()

    # Linear search : best case
    x = arr[0]
    start = time.time()
    for i in range(10000):
        result = linear_search(arr, x)
    end = time.time()
    print("Best case scenario for linear search:",
          '{:.4f}'.format(end - start), "seconds")

    # binary search : best case
    start = time.time()
    for i in range(10000):
        result = binary_search(arr, 0, n-1, x)
    end = time.time()
    print("Best case scenario for binary search:",
          '{:.4f}'.format(end - start), "seconds")

    # Linear search : average case
    x = arr[(n-1)//2]
    start = time.time()
    for i in range(10000):
        result = linear_search(arr, x)
    end = time.time()
    print("Average case scenario for linear search:",
          '{:.4f}'.format(end - start), "seconds")

    # binary search : average case
    start = time.time()
    for i in range(10000):
        result = binary_search(arr, 0, n-1, x)
    end = time.time()
    print("Average case scenario for binary search:",
          '{:.4f}'.format(end - start), "seconds")

    # Linear search : Worst case
    x = arr[n-1]
    start = time.time()
    for i in range(10000):
        result = linear_search(arr, x)
    end = time.time()
    print("Worst case scenario for linear search:",
          '{:.4f}'.format(end - start), "seconds")

    # binary search : Worst case
    start = time.time()
    for i in range(10000):
        result = binary_search(arr, 0, n-1, x)
    end = time.time()
    print("Worst case scenario for binary search:",
          '{:.4f}'.format(end - start), "seconds")

    arr.clear()

# OUTPUT
# Best case scenario for linear search: 0.0040 seconds
# Best case scenario for binary search: 0.0207 seconds
# Average case scenario for linear search: 0.1954 seconds
# Average case scenario for binary search: 0.0044 seconds
# Worst case scenario for linear search: 0.3666 seconds
# Worst case scenario for binary search: 0.0285 seconds


...........................................................

// Write a C program to perform insertion sort using dynamic memory allocation.
// Show the running time complexity w.r.t different input cases. Finally comment
// that whether it is matching with the expected complexity of O(n^2) or not.

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void insertion_sort(int *arr, int n)
{
    int i, key, j;
    for (i = 1; i < n; i++)
    {
        key = arr[i];
        j = i - 1;
        while (j >= 0 && arr[j] > key)
        {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

int main()
{
    int n = 10000, i;
    clock_t start, end;
    int *arr;

    // Allocating memory dynamically
    arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 0;
    }
    printf("Insertion sort in C\n");
    printf("Input size: %d\n", n);

    // Best Case: Array is already sorted
    for (i = 0; i < n; i++)
        arr[i] = i;
    start = clock();
    insertion_sort(arr, n);
    end = clock();
    printf("Best Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Average Case: Array is random
    for (i = 0; i < n; i++)
        arr[i] = rand() % n;
    start = clock();
    insertion_sort(arr, n);
    end = clock();
    printf("Average Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Worst Case: Array is sorted in reverse order
    for (i = 0; i < n; i++)
        arr[i] = n - i;
    start = clock();
    insertion_sort(arr, n);
    end = clock();
    printf("Worst Case %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    free(arr);
    return 0;
}

// OUTPUT
// Insertion sort in C
// Input size: 10000
// Best Case: 0.00 ms
// Average Case: 76.00 ms
// Worst Case 163.00 ms

// The expected time complexity of insertion sort is O(n^2)
// in the worst case, where n is the number of elements in the array.
// This is because in the worst case, the algorithm must make n-1
// comparisons and swaps for each element. The overall complexity
// would be O(n^2) because each comparison and swap takes O(n) time.

// But🍑 The best-case time complexity of insertion sort is O(n),
// where n is the number of elements in the array. In the best case,
// the input array is already sorted, so the algorithm will make only
// n-1 comparisons, but no swaps, resulting in a time complexity of O(n).


...........................................................................


# Write a python program to perform insertion sort using dynamic memory
# allocation. Show the running time complexity w.r.t different input cases.

import random
import time


def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key


if __name__ == "__main__":
    n = 5000
    arr = []
    print("Insertion Sort in Python")
    print("Input size:", n)

    # Best Case: Array is already sorted
    for i in range(n):
        arr.append(i)
    start = time.time()
    insertion_sort(arr)
    end = time.time()
    print("Best Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Average Case: Array is random
    for i in range(n):
        arr.append(random.randint(0, n))
    start = time.time()
    insertion_sort(arr)
    end = time.time()
    print("Average Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Worst Case: Array is sorted in reverse order
    for i in range(n):
        arr.append(n-i)
    start = time.time()
    insertion_sort(arr)
    end = time.time()
    print("Worst Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

# OUTPUT
# Insertion Sort in Python
# Input size: 5000
# Best Case: 0.0000 seconds
# Average Case: 0.7041 seconds
# Worst Case: 1.3957 seconds


.....................................................................


// Write a C program to perform selection sort using dynamic memory allocation.
// Show the running time complexity w.r.t different input cases. Finally comment
// that whether it is matching with the expected complexity of O(n^2) or not.

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void selection_sort(int *arr, int n)
{
    int i, j, min_idx;
    for (i = 0; i < n - 1; i++)
    {
        min_idx = i;
        for (j = i + 1; j < n; j++)
        {
            if (arr[j] < arr[min_idx])
                min_idx = j;
        }
        int temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}

int main()
{
    int n = 10000, i;
    clock_t start, end;
    int *arr;

    // Allocating memory dynamically
    arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 0;
    }
    printf("Selection sort in C\n");
    printf("Input size: %d\n", n);

    // Best Case: Array is already sorted
    for (i = 0; i < n; i++)
        arr[i] = i;
    start = clock();
    selection_sort(arr, n);
    end = clock();
    printf("Best Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Average Case: Array is random
    for (i = 0; i < n; i++)
        arr[i] = rand() % n;
    start = clock();
    selection_sort(arr, n);
    end = clock();
    printf("Average Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Worst Case: Array is sorted in reverse order
    for (i = 0; i < n; i++)
        arr[i] = n - i;
    start = clock();
    selection_sort(arr, n);
    end = clock();
    printf("Worst Case %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    free(arr);
    return 0;
}

// OUTPUT
// Selection sort in C
// Input size: 10000
// Best Case: 169.00 ms
// Average Case: 151.00 ms
// Worst Case 132.00 ms

// In this case, the algorithm needs to make n-1 passes through the array to sort it,
// but each pass takes O(n) time. Thus the time complexity of selection sort is O(n^2)
// in all the three cases: best, average and worst.


........................................................

# Write a python program to perform selection sort using dynamic memory
# allocation. Show the running time complexity w.r.t different input cases.

import random
import time


def selection_sort(arr):
    for i in range(len(arr)):
        min_idx = i
        for j in range(i+1, len(arr)):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]


if __name__ == "__main__":
    n = 5000
    arr = []
    print("Selection Sort in Python")
    print("Input size:", n)

    # Best Case: Array is already sorted
    for i in range(n):
        arr.append(i)
    start = time.time()
    selection_sort(arr)
    end = time.time()
    print("Best Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Average Case: Array is random
    for i in range(n):
        arr.append(random.randint(0, n))
    start = time.time()
    selection_sort(arr)
    end = time.time()
    print("Average Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Worst Case: Array is sorted in reverse order
    for i in range(n):
        arr.append(n-i)
    start = time.time()
    selection_sort(arr)
    end = time.time()
    print("Worst Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

# OUTPUT
# Selection Sort in Python
# Input size: 5000
# Best Case: 0.6708 seconds
# Average Case: 0.7661 seconds
# Worst Case: 0.7046 seconds

..........................................


// Write a C program to perform bubble sort using dynamic memory allocation.
// Show the running time complexity w.r.t different input cases. Finally comment
// that whether it is matching with the expected complexity of O(n^2) or not.

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void bubble_sort(int *arr, int n)
{
    int i, j, swap;
    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                swap = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = swap;
            }
        }
    }
}

int main()
{
    int n = 10000, i;
    clock_t start, end;
    int *arr;

    // Allocating memory dynamically
    arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 0;
    }
    printf("Bubble sort in C\n");
    printf("Input size: %d\n", n);

    // Best Case: Array is already sorted
    for (i = 0; i < n; i++)
        arr[i] = i;
    start = clock();
    bubble_sort(arr, n);
    end = clock();
    printf("Best Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Average Case: Array is random
    for (i = 0; i < n; i++)
        arr[i] = rand() % n;
    start = clock();
    bubble_sort(arr, n);
    end = clock();
    printf("Average Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Worst Case: Array is sorted in reverse order
    for (i = 0; i < n; i++)
        arr[i] = n - i;
    start = clock();
    bubble_sort(arr, n);
    end = clock();
    printf("Worst Case %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    free(arr);
    return 0;
}

// OUTPUT
// Bubble sort in C
// Input size: 10000
// Best Case: 157.00 ms
// Average Case: 236.00 ms
// Worst Case 307.00 ms

// Best Case: When the array is already sorted, the inner loop won't
// execute at all, leading to O(n) time complexity.
// Average Case: In the average case, the time complexity of Bubble Sort is O(n^2).
// Worst Case: When the array is sorted in reverse order, in each iteration,
// the largest element has to be compared n times to reach its final position,
// leading to n^2 comparisons and swaps.

...........................................


# Write a python program to perform bubble sort using dynamic memory
# allocation. Show the running time complexity w.r.t different input cases.

import random
import time


def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]


if __name__ == "__main__":
    n = 5000
    arr = []
    print("Bubble Sort in Python")
    print("Input size:", n)

    # Best Case: Array is already sorted
    for i in range(n):
        arr.append(i)
    start = time.time()
    bubble_sort(arr)
    end = time.time()
    print("Best Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Average Case: Array is random
    for i in range(n):
        arr.append(random.randint(0, n))
    start = time.time()
    bubble_sort(arr)
    end = time.time()
    print("Average Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Worst Case: Array is sorted in reverse order
    for i in range(n):
        arr.append(n-i)
    start = time.time()
    bubble_sort(arr)
    end = time.time()
    print("Worst Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

# OUTPUT
# Bubble Sort in Python
# Input size: 5000
# Best Case: 0.7951 seconds
# Average Case: 1.4894 seconds
# Worst Case: 1.9366 seconds

...................................

Critically comment that if in all the above program instead of dynamic array, if we 
use static array then whether that would effect the complexity or not. 


Using a static array instead of a dynamic array would not affect the time complexity of the sorting algorithms in the above programs. Time complexity is a measure of how the running time of an algorithm increases with the size of the input, and it does not depend on whether the array is static or dynamic.

The main difference between using a static array and a dynamic array is the way memory is allocated. In a static array, memory is allocated at compile time, while in a dynamic array, memory is allocated at runtime using functions such as malloc() or calloc(). This can affect the amount of memory required by the program and the performance of memory-related operations, but it does not affect the time complexity of the sorting algorithms.

In general, the choice between using a static array and a dynamic array depends on the specific requirements of the program, such as the size of the array and whether it needs to be resized during the execution of the program.

...........................

// Write a C program to sort a list of element in an Array using Quick Sort.
// Show the running time complexity w.r.t different input cases (best/average/worst).

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void swap(int *a, int *b)
{
    int t = *a;
    *a = *b;
    *b = t;
}

int partition(int *arr, int low, int high)
{
    int pivot = arr[high];
    int i = (low - 1);

    for (int j = low; j <= high - 1; j++)
    {
        if (arr[j] < pivot)
        {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

void quick_sort(int *arr, int low, int high)
{
    if (low < high)
    {
        int pi = partition(arr, low, high);

        quick_sort(arr, low, pi - 1);
        quick_sort(arr, pi + 1, high);
    }
}

int main()
{
    int n = 10000, i;
    clock_t start, end;
    int *arr;

    // Allocating memory dynamically
    arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 0;
    }
    printf("Quick sort in C\n");
    printf("Input size: %d\n", n);

    // Best Case: Array is already sorted
    for (i = 0; i < n; i++)
        arr[i] = i;
    start = clock();
    quick_sort(arr, 0, n - 1);
    end = clock();
    printf("Best Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Average Case: Array is random
    for (i = 0; i < n; i++)
        arr[i] = rand() % (n * 10);
    start = clock();
    quick_sort(arr, 0, n - 1);
    end = clock();
    printf("Average Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Worst Case: Array is sorted in reverse order
    for (i = 0; i < n; i++)
        arr[i] = n - i;
    start = clock();
    quick_sort(arr, 0, n - 1);
    end = clock();
    printf("Worst Case %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    free(arr);
    return 0;
}

// OUTPUT
// Quick sort in C
// Input size: 10000
// Best Case: 251.00 ms
// Average Case: 3.00 ms
// Worst Case 193.00 ms

........................

# Write a Python program to sort a list of element in an Array using Quick Sort.
# Show the running time complexity w.r.t different input cases (best/average/worst).

import random
import time


def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    else:
        pivot = arr[0]
        less = [x for x in arr[1:] if x <= pivot]
        greater = [x for x in arr[1:] if x > pivot]
        return quick_sort(less) + [pivot] + quick_sort(greater)


if __name__ == "__main__":
    n = 998
    arr = []
    print("Quick Sort in Python")
    print("Input size:", n)

    # Best Case: Array is already sorted
    for i in range(n):
        arr.append(i) 
    start = time.time()
    quick_sort(arr)
    end = time.time()
    print("Best Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Average Case: Array is random
    for i in range(n):
        arr.append(random.randint(0, n))
    start = time.time()
    quick_sort(arr)
    end = time.time()
    print("Average Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Worst Case: Array is sorted in reverse order
    for i in range(n):
        arr.append(n-i)
    start = time.time()
    quick_sort(arr)
    end = time.time()
    print("Worst Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

# OUTPUT
# Quick Sort in Python
# Input size: 998
# Best Case: 0.0375 seconds
# Average Case: 0.0026 seconds
# Worst Case: 0.0378 seconds

...............................

// Write a C program to sort a list of element in an Array using Merge Sort.
// Show the running time complexity w.r.t different input cases (best/average/worst).

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void merge(int *arr, int left, int mid, int right)
{
    int i, j, k;
    int left_size = mid - left + 1;
    int right_size = right - mid;

    int *left_array = (int *)malloc(left_size * sizeof(int));
    int *right_array = (int *)malloc(right_size * sizeof(int));

    for (i = 0; i < left_size; i++)
        left_array[i] = arr[left + i];
    for (j = 0; j < right_size; j++)
        right_array[j] = arr[mid + 1 + j];

    i = j = 0;
    k = left;
    while (i < left_size && j < right_size)
    {
        if (left_array[i] <= right_array[j])
            arr[k++] = left_array[i++];
        else
            arr[k++] = right_array[j++];
    }

    while (i < left_size)
        arr[k++] = left_array[i++];
    while (j < right_size)
        arr[k++] = right_array[j++];

    free(left_array);
    free(right_array);
}

void merge_sort(int *arr, int left, int right)
{
    if (left < right)
    {
        int mid = left + (right - left) / 2;

        merge_sort(arr, left, mid);
        merge_sort(arr, mid + 1, right);

        merge(arr, left, mid, right);
    }
}

int main()
{
    int n = 1000000, i;
    clock_t start, end;
    int *arr;

    // Allocating memory dynamically
    arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 0;
    }
    printf("Merge sort in C\n");
    printf("Input size: %d\n", n);

    // Best Case: Array is already sorted
    for (i = 0; i < n; i++)
        arr[i] = i;
    start = clock();
    merge_sort(arr, 0, n - 1);
    end = clock();
    printf("Best Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Average Case: Array is random
    for (i = 0; i < n; i++)
        arr[i] = rand() % (n * 10);
    start = clock();
    merge_sort(arr, 0, n - 1);
    end = clock();
    printf("Average Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Worst Case: Array is sorted in reverse order
    for (i = 0; i < n; i++)
        arr[i] = n - i;
    start = clock();
    merge_sort(arr, 0, n - 1);
    end = clock();
    printf("Worst Case %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    free(arr);
    return 0;
}

// OUTPUT
// Merge sort in C
// Input size: 1000000
// Best Case: 230.00 ms
// Average Case: 315.00 ms
// Worst Case 229.00 ms

............................

# Write a Python program to sort a list of element in an Array using Merge Sort.
# Show the running time complexity w.r.t different input cases (best/average/worst).

import random
import time


def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr)//2
        left = arr[:mid]
        right = arr[mid:]
        merge_sort(left)
        merge_sort(right)
        i = j = k = 0
        while i < len(left) and j < len(right):
            if left[i] < right[j]:
                arr[k] = left[i]
                i += 1
            else:
                arr[k] = right[j]
                j += 1
            k += 1
        while i < len(left):
            arr[k] = left[i]
            i += 1
            k += 1
        while j < len(right):
            arr[k] = right[j]
            j += 1
            k += 1
    return arr


if __name__ == "__main__":
    n = 100000
    arr = []
    print("Merge Sort in Python")
    print("Input size:", n)

    # Best Case: Array is already sorted
    for i in range(n):
        arr.append(i) 
    start = time.time()
    merge_sort(arr)
    end = time.time()
    print("Best Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Average Case: Array is random
    for i in range(n):
        arr.append(random.randint(0, n))
    start = time.time()
    merge_sort(arr)
    end = time.time()
    print("Average Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Worst Case: Array is sorted in reverse order
    for i in range(n):
        arr.append(n-i)
    start = time.time()
    merge_sort(arr)
    end = time.time()
    print("Worst Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

# OUTPUT
# Merge Sort in Python
# Input size: 100000
# Best Case: 0.2663 seconds
# Average Case: 0.3174 seconds
# Worst Case: 0.2670 seconds

.................................

// Write a C program to sort a list of element in an Array using Heap Sort.
// Show the running time complexity w.r.t different input cases (best/average/worst).

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

void heapify(int *arr, int n, int i)
{
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest])
        largest = left;

    if (right < n && arr[right] > arr[largest])
        largest = right;

    if (largest != i)
    {
        swap(&arr[i], &arr[largest]);

        heapify(arr, n, largest);
    }
}

void heap_sort(int *arr, int n)
{
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    for (int i = n - 1; i >= 0; i--)
    {
        swap(&arr[0], &arr[i]);

        heapify(arr, i, 0);
    }
}

int main()
{
    int n = 1000000, i;
    clock_t start, end;
    int *arr;

    // Allocating memory dynamically
    arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 0;
    }
    printf("Heap sort in C\n");
    printf("Input size: %d\n", n);

    // Best Case: Array is already sorted
    for (i = 0; i < n; i++)
        arr[i] = i;
    start = clock();
    heap_sort(arr, n);
    end = clock();
    printf("Best Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Average Case: Array is random
    for (i = 0; i < n; i++)
        arr[i] = rand() % (n * 10);
    start = clock();
    heap_sort(arr, n);
    end = clock();
    printf("Average Case: %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Worst Case: Array is sorted in reverse order
    for (i = 0; i < n; i++)
        arr[i] = n - i;
    start = clock();
    heap_sort(arr, n);
    end = clock();
    printf("Worst Case %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    free(arr);
    return 0;
}

// OUTPUT
// Heap sort in C
// Input size: 1000000
// Best Case: 255.00 ms
// Average Case: 340.00 ms
// Worst Case 243.00 ms

............................

# Write a Python program to sort a list of element in an Array using Heap Sort.
# Show the running time complexity w.r.t different input cases (best/average/worst).


import random
import time


def heapify(arr, n, i):
    largest = i
    left = 2 * i + 1
    right = 2 * i + 2
    if left < n and arr[left] > arr[largest]:
        largest = left
    if right < n and arr[right] > arr[largest]:
        largest = right
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)


def heap_sort(arr):
    n = len(arr)
    for i in range(n//2 - 1, -1, -1):
        heapify(arr, n, i)
    for i in range(n-1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]
        heapify(arr, i, 0)
    return arr


if __name__ == "__main__":
    n = 100000
    arr = []
    print("Heap Sort in Python")
    print("Input size:", n)

    # Best Case: Array is already sorted
    for i in range(n):
        arr.append(i) 
    start = time.time()
    heap_sort(arr)
    end = time.time()
    print("Best Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Average Case: Array is random
    for i in range(n):
        arr.append(random.randint(0, n))
    start = time.time()
    heap_sort(arr)
    end = time.time()
    print("Average Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Worst Case: Array is sorted in reverse order
    for i in range(n):
        arr.append(n-i)
    start = time.time()
    heap_sort(arr)
    end = time.time()
    print("Worst Case:", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

# OUTPUT
# Heap Sort in Python
# Input size: 100000
# Best Case: 0.5421 seconds
# Average Case: 0.5695 seconds
# Worst Case: 0.4919 seconds

..............................

// Write a C program to find the maximum and minimum element present
// in a list of elements using different approach. Show the running
// time complexity w.r.t different input cases (best/average/worst).
// Finally comment which one is better & why.

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Approach 1: Linear Search
void linear_search(int *arr, int n, int *max, int *min)
{
    int i;
    *max = arr[0];
    *min = arr[0];
    for (i = 1; i < n; i++)
    {
        if (arr[i] > *max)
        {
            *max = arr[i];
        }
        if (arr[i] < *min)
        {
            *min = arr[i];
        }
    }
}

// Approach 2: Divide and Conquer
void divide_and_conquer(int *arr, int l, int r, int *max, int *min)
{
    int mid;
    if (l == r)
    {
        *max = arr[l];
        *min = arr[l];
    }
    else if (r - l == 1)
    {
        if (arr[r] > arr[l])
        {
            *max = arr[r];
            *min = arr[l];
        }
        else
        {
            *max = arr[l];
            *min = arr[r];
        }
    }
    else
    {
        mid = l + (r - l) / 2;
        int left_max, left_min, right_max, right_min;
        divide_and_conquer(arr, l, mid, &left_max, &left_min);
        divide_and_conquer(arr, mid + 1, r, &right_max, &right_min);
        *max = (left_max > right_max) ? left_max : right_max;
        *min = (left_min < right_min) ? left_min : right_min;
    }
}

int main()
{
    int n = 100000000, i, max, min;
    clock_t start, end;
    int *arr;

    // Allocating memory dynamically
    arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL)
    {
        printf("Memory allocation failed\n");
        return 0;
    }
    printf("Finding max and min in C\n");
    printf("Input size: %d\n", n);

    // Best Case: Array is already sorted
    for (i = 0; i < n; i++)
        arr[i] = i;
    start = clock();
    linear_search(arr, n, &max, &min);
    end = clock();
    printf("Linear Search (Best Case): %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);
    start = clock();
    divide_and_conquer(arr, 0, n - 1, &max, &min);
    end = clock();
    printf("Divide & Conquer (Best Case): %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Average Case: Array is random
    for (i = 0; i < n; i++)
        arr[i] = rand() % (n * 10);
    start = clock();
    linear_search(arr, n, &max, &min);
    end = clock();
    printf("Linear Search (Average Case): %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);
    start = clock();
    divide_and_conquer(arr, 0, n - 1, &max, &min);
    end = clock();
    printf("Divide & Conquer (Average Case): %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    // Worst Case: Array is sorted in reverse order
    for (i = 0; i < n; i++)
        arr[i] = n - i;
    start = clock();
    linear_search(arr, n, &max, &min);
    end = clock();
    printf("Linear Search (Worst Case): %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);
    start = clock();
    divide_and_conquer(arr, 0, n - 1, &max, &min);
    end = clock();
    printf("Divide & Conquer (Worst Case): %.2f ms\n", ((double)(end - start)) * 1000 / CLOCKS_PER_SEC);

    free(arr);
    return 0;
}

// OUTPUT
// Finding max and min in C
// Input size: 100000000
// Linear Search (Best Case): 341.00 ms
// Divide & Conquer (Best Case): 670.00 ms
// Linear Search (Average Case): 269.00 ms
// Divide & Conquer (Average Case): 1536.00 ms
// Linear Search (Worst Case): 319.00 ms
// Divide & Conquer (Worst Case): 672.00 ms

// Linear Search(Best/Average/Worst):
// Time Complexity = O(n)
// Space Complexity = O(1)

// Divide & Conquer(Best/Average/Worst):
// Time Complexity = O(nlogn)
// Space Complexity = O(logn)

.............................

# Write a Python program to find the maximum and minimum element present
# in a list of elements using different approach. Show the running
# time complexity w.r.t different input cases (best/average/worst).

import random
import time

# Approach 1: Linear Search
def linear_search(arr, n):
    max = arr[0]
    min = arr[0]
    for i in range(1, n):
        if arr[i] > max:
            max = arr[i]
        if arr[i] < min:
            min = arr[i]
    return (max, min)

# Approach 2: Divide and Conquer
def divide_and_conquer(arr, l, r):
    if l == r:
        return (arr[l], arr[l])
    elif r - l == 1:
        if arr[r] > arr[l]:
            return (arr[r], arr[l])
        else:
            return (arr[l], arr[r])
    else:
        mid = l + (r - l) // 2
        left_max, left_min = divide_and_conquer(arr, l, mid)
        right_max, right_min = divide_and_conquer(arr, mid + 1, r)
        max = left_max if left_max > right_max else right_max
        min = left_min if left_min < right_min else right_min
        return (max, min)
    
if __name__=="__main__":
    n = 1000000
    arr = []
    print("Finding max and min in Python")
    print("Input size:", n)

    # Best Case: Array is already sorted
    for i in range(n):
        arr.append(i)
    start = time.time()
    result = linear_search(arr, n)
    end = time.time()
    print("Linear Search (Best Case):", '{:.4f}'.format(end - start), "seconds")
    start = time.time()
    result = divide_and_conquer(arr, 0, n - 1)
    end = time.time()
    print("Divide & Conquer (Best Case):", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Average Case: Array is random
    for i in range(n):
        arr.append(random.randint(0, n))
    start = time.time()
    result = linear_search(arr, n)
    end = time.time()
    print("Linear Search (Average Case):", '{:.4f}'.format(end - start), "seconds")
    start = time.time()
    result = divide_and_conquer(arr, 0, n - 1)
    end = time.time()
    print("Divide & Conquer (Average Case):", '{:.4f}'.format(end - start), "seconds")
    arr.clear()

    # Worst Case: Array is sorted in reverse order
    for i in range(n):
        arr.append(n - i)
    start = time.time()
    result = linear_search(arr, n)
    end = time.time()
    print("Linear Search (Worst Case):", '{:.4f}'.format(end - start), "seconds")
    start = time.time()
    result = divide_and_conquer(arr, 0, n - 1)
    end = time.time()
    print("Divide & Conquer (Worst Case):", '{:.4f}'.format(end - start), "seconds")
    arr.clear()


# OUTPUT
# Finding max and min in Python
# Input size: 1000000
# Linear Search (Best Case): 0.0623 seconds
# Divide & Conquer (Best Case): 0.3470 seconds
# Linear Search (Average Case): 0.0957 seconds
# Divide & Conquer (Average Case): 0.3358 seconds
# Linear Search (Worst Case): 0.1042 seconds
# Divide & Conquer (Worst Case): 0.3095 seconds

...................................................

// Write a C program to implement Strassen’s matrix multiplication.

#include <stdio.h>
#include <stdlib.h>

void strassen(int n, int A[][n], int B[][n], int C[][n]);
void add(int n, int A[][n], int B[][n], int C[][n]);
void subtract(int n, int A[][n], int B[][n], int C[][n]);

int main()
{
    int n = 4, i, j;
    int A[n][n], B[n][n], C[n][n];

    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            A[i][j] = i + j;
            B[i][j] = 2 * A[i][j];
        }
    }

    printf("Strassen's Matrix Multiplication in C\n", n, n);
    printf("Order of both matrices: %d * %d\n", n, n);
    strassen(n, A, B, C);

    printf("\nA matrix=\n");
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
            printf("%d\t", A[i][j]);
        printf("\n");
    }

    printf("\nB matrix=\n");
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
            printf("%d\t", B[i][j]);
        printf("\n");
    }

    printf("\nAxB matrix=\n");
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
            printf("%d\t", C[i][j]);
        printf("\n");
    }

    return 0;
}

void strassen(int n, int A[][n], int B[][n], int C[][n])
{
    if (n == 1)
    {
        C[0][0] = A[0][0] * B[0][0];
        return;
    }

    int i, j;

    int A11[n / 2][n / 2], A12[n / 2][n / 2], A21[n / 2][n / 2], A22[n / 2][n / 2];
    int B11[n / 2][n / 2], B12[n / 2][n / 2], B21[n / 2][n / 2], B22[n / 2][n / 2];
    int C11[n / 2][n / 2], C12[n / 2][n / 2], C21[n / 2][n / 2], C22[n / 2][n / 2];
    int P1[n / 2][n / 2], P2[n / 2][n / 2], P3[n / 2][n / 2], P4[n / 2][n / 2], P5[n / 2][n / 2], P6[n / 2][n / 2], P7[n / 2][n / 2];
    int temp1[n / 2][n / 2], temp2[n / 2][n / 2];

    // Divide A & B into 4 submatrices
    for (i = 0; i < n / 2; i++)
    {
        for (j = 0; j < n / 2; j++)
        {
            A11[i][j] = A[i][j];
            B11[i][j] = B[i][j];
        }
    }
    for (i = 0; i < n / 2; i++)
    {
        for (j = n / 2; j < n; j++)
        {
            A12[i][j - n / 2] = A[i][j];
            B12[i][j - n / 2] = B[i][j];
        }
    }
    for (i = n / 2; i < n; i++)
    {
        for (j = 0; j < n / 2; j++)
        {
            A21[i - n / 2][j] = A[i][j];
            B21[i - n / 2][j] = B[i][j];
        }
    }
    for (i = n / 2; i < n; i++)
    {
        for (j = n / 2; j < n; j++)
        {
            A22[i - n / 2][j - n / 2] = A[i][j];
            B22[i - n / 2][j - n / 2] = B[i][j];
        }
    }

    // Calculate the 7 products
    add(n / 2, A11, A22, temp1);
    add(n / 2, B11, B22, temp2);
    strassen(n / 2, temp1, temp2, P1);

    add(n / 2, A21, A22, temp1);
    strassen(n / 2, temp1, B11, P2);

    subtract(n / 2, B12, B22, temp1);
    strassen(n / 2, A11, temp1, P3);

    subtract(n / 2, B21, B11, temp1);
    strassen(n / 2, A22, temp1, P4);

    add(n / 2, A11, A12, temp1);
    strassen(n / 2, temp1, B22, P5);

    subtract(n / 2, A21, A11, temp1);
    add(n / 2, B11, B12, temp2);
    strassen(n / 2, temp1, temp2, P6);

    subtract(n / 2, A12, A22, temp1);
    add(n / 2, B21, B22, temp2);
    strassen(n / 2, temp1, temp2, P7);

    // Calculate the 4 quadrants of C using the products
    add(n / 2, P1, P4, temp1);
    subtract(n / 2, temp1, P5, temp2);
    add(n / 2, temp2, P7, C11);

    add(n / 2, P3, P5, C12);

    add(n / 2, P2, P4, C21);

    add(n / 2, P1, P3, temp1);
    subtract(n / 2, temp1, P2, temp2);
    add(n / 2, temp2, P6, C22);

    // Combine the 4 quadrants of C into one matrix
    for (i = 0; i < n / 2; i++)
        for (j = 0; j < n / 2; j++)
            C[i][j] = C11[i][j];
    for (i = 0; i < n / 2; i++)
        for (j = n / 2; j < n; j++)
            C[i][j] = C12[i][j - n / 2];
    for (i = n / 2; i < n; i++)
        for (j = 0; j < n / 2; j++)
            C[i][j] = C21[i - n / 2][j];
    for (i = n / 2; i < n; i++)
        for (j = n / 2; j < n; j++)
            C[i][j] = C22[i - n / 2][j - n / 2];
}

void add(int n, int A[][n], int B[][n], int C[][n])
{
    int i, j;
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
            C[i][j] = A[i][j] + B[i][j];
}

void subtract(int n, int A[][n], int B[][n], int C[][n])
{
    int i, j;
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
            C[i][j] = A[i][j] - B[i][j];
}

// OUTPUT
// Strassen's Matrix Multiplication
// Order of both matrices: 4 * 4

// A matrix=
// 0       1       2       3
// 1       2       3       4
// 2       3       4       5
// 3       4       5       6

// B matrix=
// 0       2       4       6
// 2       4       6       8
// 4       6       8       10
// 6       8       10      12

// AxB matrix=
// 28      40      52      64
// 40      60      80      100
// 52      80      108     136
// 64      100     136     172

...............................


# Write a Python program to implement Strassen’s matrix multiplication.

import numpy as np


def strassen_multiply(A, B):
    n = A.shape[0]

    # Base case: if the matrices are 1x1
    if n == 1:
        return A * B

    # Split matrices into quadrants
    A11 = A[:n//2, :n//2]
    A12 = A[:n//2, n//2:]
    A21 = A[n//2:, :n//2]
    A22 = A[n//2:, n//2:]

    B11 = B[:n//2, :n//2]
    B12 = B[:n//2, n//2:]
    B21 = B[n//2:, :n//2]
    B22 = B[n//2:, n//2:]

    # Recursively compute products of smaller matrices
    P1 = strassen_multiply(A11 + A22, B11 + B22)
    P2 = strassen_multiply(A21 + A22, B11)
    P3 = strassen_multiply(A11, B12 - B22)
    P4 = strassen_multiply(A22, B21 - B11)
    P5 = strassen_multiply(A11 + A12, B22)
    P6 = strassen_multiply(A21 - A11, B11 + B12)
    P7 = strassen_multiply(A12 - A22, B21 + B22)

    # Compute the quadrants of the product matrix
    C11 = P1 + P4 - P5 + P7
    C12 = P3 + P5
    C21 = P2 + P4
    C22 = P1 - P2 + P3 + P6

    # Combine the quadrants into a single matrix and return
    C = np.vstack((np.hstack((C11, C12)), np.hstack((C21, C22))))
    return C


if __name__ == "__main__":
    n = 4
    A = [[i+j for j in range(n)] for i in range(n)]
    B = [[2*A[i][j] for j in range(n)] for i in range(n)]
    print("Strassen's Matrix Multiplication in Python")
    print("A matrix =")
    print(A)
    print("B matrix =")
    print(B)
    A = np.array(A)
    B = np.array(B)
    C = strassen_multiply(A, B)
    C = C.tolist()
    print("A*B matrix =")
    print(C)

# OUTPUT
# Strassen's Matrix Multiplication in Python
# A matrix =
# [[0, 1, 2, 3], [1, 2, 3, 4], [2, 3, 4, 5], [3, 4, 5, 6]]
# B matrix =
# [[0, 2, 4, 6], [2, 4, 6, 8], [4, 6, 8, 10], [6, 8, 10, 12]]
# A*B matrix =
# [[28, 40, 52, 64], [40, 60, 80, 100], [52, 80, 108, 136], [64, 100, 136, 172]]

..................................................................................

// Write a C program to Implement the concept of Depth First Search algorithm.
// Apply the algorithm on the following graph:
//     A ------- D
//    / \        |\
//   /   \       | \
//  B     C      |  \
//  |     |      |   \
//  |     |      |    \
//  E --- F      G --- H

#include <stdio.h>
#include <stdbool.h>

#define nodes 8

void addEdge(int adj_matrix[nodes][nodes], char u, char v)
{
    int u_index = (int)(u - 'A');
    int v_index = (int)(v - 'A');
    adj_matrix[u_index][v_index] = 1;
    adj_matrix[v_index][u_index] = 1;
}

void dfs(int adj_matrix[nodes][nodes], bool visited[nodes], char current_node)
{
    int current = (int)(current_node - 'A');
    visited[current] = true;
    printf("Visited: %c\n", current_node);

    for (int i = 0; i < nodes; i++)
    {
        if (adj_matrix[current][i] == 1 && !visited[i])
        {
            dfs(adj_matrix, visited, (char)('A' + i));
        }
    }
}

int main()
{
    printf("DFS in C\n");
    int adj_matrix[nodes][nodes] = {0};

    addEdge(adj_matrix, 'A', 'B');
    addEdge(adj_matrix, 'A', 'C');
    addEdge(adj_matrix, 'A', 'D');
    addEdge(adj_matrix, 'B', 'E');
    addEdge(adj_matrix, 'C', 'F');
    addEdge(adj_matrix, 'E', 'F');
    addEdge(adj_matrix, 'D', 'G');
    addEdge(adj_matrix, 'D', 'H');
    addEdge(adj_matrix, 'G', 'H');

    // Perform depth-first search
    bool visited[nodes] = {false};
    dfs(adj_matrix, visited, 'A');

    return 0;
}

// OUTPUT
// DFS in C
// Visited: A
// Visited: B
// Visited: E
// Visited: F
// Visited: C
// Visited: D
// Visited: G
// Visited: H

.....................

# Write a Python program to Implement the concept of Depth First Search algorithm.
# Apply the algorithm on the following graph:
#     A ------- D
#    / \        |\
#   /   \       | \
#  B     C      |  \
#  |     |      |   \
#  |     |      |    \
#  E --- F      G --- H

def initializeMatrix(n):
    adj_matrix = []
    for i in range(n):
        row = [0] * n
        adj_matrix.append(row)
    return adj_matrix

def addEdge(adj_matrix, u, v):
    u_index = ord(u) - 65
    v_index = ord(v) - 65
    adj_matrix[u_index][v_index] = 1
    adj_matrix[v_index][u_index] = 1

def dfs(adj_matrix, start_node, visited=None):
    if visited is None:
        visited = set()
    node_index = ord(start_node) - 65
    visited.add(start_node)
    print("Visited:", start_node)
    for neighbor_index in range(len(adj_matrix[node_index])):
        if adj_matrix[node_index][neighbor_index] == 1:
            neighbor = chr(neighbor_index + 65)
            if neighbor not in visited:
                dfs(adj_matrix, neighbor, visited)


adj_matrix = initializeMatrix(8)
addEdge(adj_matrix, 'A', 'B')
addEdge(adj_matrix, 'A', 'C')
addEdge(adj_matrix, 'A', 'D')
addEdge(adj_matrix, 'B', 'E')
addEdge(adj_matrix, 'C', 'F')
addEdge(adj_matrix, 'E', 'F')
addEdge(adj_matrix, 'D', 'G')
addEdge(adj_matrix, 'D', 'H')
addEdge(adj_matrix, 'G', 'H')

print("DFS in Python")
dfs(adj_matrix, 'A')

# OUTPUT
# DFS in Python
# Visited: A
# Visited: B
# Visited: E
# Visited: F
# Visited: C
# Visited: D
# Visited: G
# Visited: H

..............................

// Write a C program to Implement the concept of Breadth First Search algorithm.
// Apply the algorithm on the following graph:
//     A ------- D
//    / \        |\
//   /   \       | \
//  B     C      |  \
//  |     |      |   \
//  |     |      |    \
//  E --- F      G --- H

#include <stdio.h>
#include <stdbool.h>

#define nodes 8

void addEdge(int adj_matrix[nodes][nodes], char u, char v)
{
    int u_index = (int)(u - 'A');
    int v_index = (int)(v - 'A');
    adj_matrix[u_index][v_index] = 1;
    adj_matrix[v_index][u_index] = 1;
}

void bfs(int adj_matrix[nodes][nodes], bool visited[nodes], char start_node)
{
    int start = (int)(start_node - 'A');
    int queue[nodes];
    int front = -1, rear = -1;
    visited[start] = true;
    queue[++rear] = start;
    while (front != rear)
    {
        int current_node = queue[++front];
        printf("Visited: %c\n", current_node + 'A');
        for (int i = 0; i < nodes; i++)
        {
            if (adj_matrix[current_node][i] == 1 && !visited[i])
            {
                visited[i] = true;
                queue[++rear] = i;
            }
        }
    }
}

int main()
{
    printf("BFS in C\n");
    int adj_matrix[nodes][nodes] = {0};

    addEdge(adj_matrix, 'A', 'B');
    addEdge(adj_matrix, 'A', 'C');
    addEdge(adj_matrix, 'A', 'D');
    addEdge(adj_matrix, 'B', 'E');
    addEdge(adj_matrix, 'C', 'F');
    addEdge(adj_matrix, 'E', 'F');
    addEdge(adj_matrix, 'D', 'G');
    addEdge(adj_matrix, 'D', 'H');
    addEdge(adj_matrix, 'G', 'H');

    bool visited[nodes] = {false};
    bfs(adj_matrix, visited, 'A');

    return 0;
}

// OUTPUT
// BFS in C
// Visited: A
// Visited: B
// Visited: C
// Visited: D
// Visited: E
// Visited: F
// Visited: G
// Visited: H

.....................................

# Write a Python program to Implement the concept of Breadth First Search algorithm.
# Apply the algorithm on the following graph:
#     A ------- D
#    / \        |\
#   /   \       | \
#  B     C      |  \
#  |     |      |   \
#  |     |      |    \
#  E --- F      G --- H

from collections import deque

def initializeMatrix(n):
    adj_matrix = []
    for i in range(n):
        row = [0] * n
        adj_matrix.append(row)
    return adj_matrix

def addEdge(adj_matrix, u, v):
    u_index = ord(u) - 65
    v_index = ord(v) - 65
    adj_matrix[u_index][v_index] = 1
    adj_matrix[v_index][u_index] = 1

def bfs(adj_matrix, start_node):
    n = len(adj_matrix)
    visited = [False] * n
    queue = deque([start_node])
    while queue:
        node = queue.popleft()
        node_index = ord(node) - 65
        if not visited[node_index]:
            visited[node_index] = True
            print("Visited:",node)
            for neighbor_index in range(n):
                if adj_matrix[node_index][neighbor_index] == 1 and not visited[neighbor_index]:
                    neighbor = chr(neighbor_index + 65)
                    queue.append(neighbor)

adj_matrix = initializeMatrix(8)
addEdge(adj_matrix, 'A', 'B')
addEdge(adj_matrix, 'A', 'C')
addEdge(adj_matrix, 'A', 'D')
addEdge(adj_matrix, 'B', 'E')
addEdge(adj_matrix, 'C', 'F')
addEdge(adj_matrix, 'E', 'F')
addEdge(adj_matrix, 'D', 'G')
addEdge(adj_matrix, 'D', 'H')
addEdge(adj_matrix, 'G', 'H')

print("BFS in Python")
bfs(adj_matrix, 'A')

# OUTPUT
# BFS in Python
# Visited: A
# Visited: B
# Visited: C
# Visited: D
# Visited: E
# Visited: F
# Visited: G
# Visited: H

................................

// Write a C program to implement the concept of Kruskal’s algorithm.
// Apply it to find the MST for the following graph.

//          2
//   A ------------ B
//   | \           / \ 
//   |  \         /   \ 
//  7|   \2      /     \ 
//   |    \     /5      \ 7
//   |     \   /         \ 
//   |      \ /           \ 
//   C ----- D ----------- E
//       5           4

#include <stdio.h>
#include <stdlib.h>

struct graph
{
    char src;
    char dest;
    int weight;
};

int comparator(const void *p1, const void *p2)
{
    const struct graph *x = p1;
    const struct graph *y = p2;
    return x->weight - y->weight;
}

void makeSet(int parent[], int rank[], int n)
{
    for (int i = 0; i < n; i++)
    {
        parent[i] = i;
        rank[i] = 0;
    }
}

int findParent(int parent[], int component)
{
    if (parent[component] == component)
        return component;

    return parent[component] = findParent(parent, parent[component]);
}

void unionSet(int u, int v, int parent[], int rank[], int n)
{
    u = findParent(parent, u);
    v = findParent(parent, v);
    if (rank[u] < rank[v])
        parent[u] = v;
    else if (rank[u] > rank[v])
        parent[v] = u;
    else
    {
        parent[v] = u;
        rank[u]++;
    }
}

void kruskalMST(int v, int n, struct graph g[])
{

    qsort(g, n, sizeof(g[0]), comparator);
    int parent[v];
    int rank[v];
    makeSet(parent, rank, n);

    int minCost = 0;

    printf("Edges \tWeight\n");
    for (int i = 0; i < n; i++)
    {
        char v1 = g[i].src;
        char v2 = g[i].dest;
        int wt = g[i].weight;
        int p1 = v1 - 'A';
        int p2 = v2 - 'A';
        if (findParent(parent, p1) != findParent(parent, p2))
        {
            unionSet(p1, p2, parent, rank, v);
            minCost += wt;
            printf("%c - %c \t%d\n", v1, v2, wt);
        }
    }
    printf("Minimum Spanning Tree: %d\n", minCost);
}

int main()
{
    printf("Kruskal's Algorithm in C\n");
    int vertices = 5;
    struct graph g[] =
        {
            {'A', 'B', 2},
            {'A', 'C', 7},
            {'A', 'D', 2},
            {'B', 'D', 5},
            {'B', 'E', 7},
            {'C', 'D', 5},
            {'D', 'E', 4}};
    int numEdges = sizeof(g) / sizeof(struct graph);
    kruskalMST(vertices, numEdges, g);

    return 0;
}

// OUTPUT
// Kruskal's Algorithm in C
// Edges   Weight
// A - D   2
// A - B   2
// D - E   4
// C - D   5
// Minimum Spanning Tree: 13

..............................

# Write a Python program to implement the concept of Kruskal’s algorithm.
# Apply it to find the MST for the following graph.

#          2
#   A ------------ B
#   | \           / \
#   |  \         /   \
#  7|   \2      /     \
#   |    \     /5      \ 7
#   |     \   /         \
#   |      \ /           \
#   C ----- D ----------- E
#       5           4

class Graph:
    def __init__(self, vertices):
        self.V = vertices
        self.graph = []

    def addEdge(self, u, v, w):
        u_index = ord(u) - 65
        v_index = ord(v) - 65
        self.graph.append([u_index, v_index, w])

    def find(self, parent, i):
        if parent[i] != i:
            parent[i] = self.find(parent, parent[i])
        return parent[i]

    def union(self, parent, rank, x, y):
        if rank[x] < rank[y]:
            parent[x] = y
        elif rank[x] > rank[y]:
            parent[y] = x
        else:
            parent[y] = x
            rank[x] += 1

    def kruskalMST(self):
        result = []
        i = 0
        e = 0
        self.graph = sorted(self.graph, key=lambda item: item[2])
        parent = []
        rank = []
        for node in range(self.V):
            parent.append(node)
            rank.append(0)
        while e < self.V - 1:
            u, v, w = self.graph[i]
            i = i + 1
            x = self.find(parent, u)
            y = self.find(parent, v)
            if x != y:
                e = e + 1
                result.append([u, v, w])
                self.union(parent, rank, x, y)
        minimumCost = 0
        print("Edge \tWeight")
        for u, v, weight in result:
            minimumCost += weight
            print(f"{chr(u+65)} - {chr(v+65)} \t{weight}")
        print("Minimum Spanning Tree:", minimumCost)


if __name__ == '__main__':
    print("Kruskal's algorithm in Python")
    g = Graph(5)
    g.addEdge('A', 'B', 2)
    g.addEdge('A', 'C', 7)
    g.addEdge('A', 'D', 2)
    g.addEdge('B', 'D', 5)
    g.addEdge('B', 'E', 7)
    g.addEdge('C', 'D', 5)
    g.addEdge('D', 'E', 4)
    g.kruskalMST()


# OUTPUT
# Kruskal's algorithm in Python
# Edge    Weight
# A - B   2
# A - D   2
# D - E   4
# C - D   5
# Minimum Spanning Tree: 13

...............................

// Write a C program to implement the concept of Prim’s algorithm.
// Apply it to find the MST for the following graph.

//          2
//   A ------------ B
//   | \           / \ 
//   |  \         /   \ 
//  7|   \2      /     \ 
//   |    \     /5      \ 7
//   |     \   /         \ 
//   |      \ /           \ 
//   C ----- D ----------- E
//       5           4
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

struct graph
{
    char src;
    char dest;
    int weight;
};

void primMST(int v, int n, struct graph g[])
{
    int adjMat[v][v], visited[v];
    int i, j;

    for (i = 0; i < v; i++)
    {
        for (j = 0; j < v; j++)
        {
            adjMat[i][j] = 0;
        }
        visited[i] = 0;
    }

    for (i = 0; i < n; i++)
    {
        int v1 = g[i].src - 'A';
        int v2 = g[i].dest - 'A';
        int wt = g[i].weight;
        adjMat[v1][v2] = adjMat[v2][v1] = wt;
    }
    int dist[v];
    int parent[v];
    for (i = 0; i < v; i++)
    {
        dist[i] = INT_MAX;
        parent[i] = -1;
    }
    dist[0] = 0;
    for (i = 0; i < n - 1; i++)
    {
        int minDist = INT_MAX;
        int minIndex = -1;
        for (j = 0; j < v; j++)
        {
            if (!visited[j] && dist[j] < minDist)
            {
                minDist = dist[j];
                minIndex = j;
            }
        }
        visited[minIndex] = 1;
        for (j = 0; j < v; j++)
        {
            if (adjMat[minIndex][j] && !visited[j] && adjMat[minIndex][j] < dist[j])
            {
                dist[j] = adjMat[minIndex][j];
                parent[j] = minIndex;
            }
        }
    }

    int minCost = 0;
    printf("Edges \tWeight\n");
    for (i = 1; i < v; i++)
    {
        if (parent[i] != -1)
        {
            char v1 = parent[i] + 'A';
            char v2 = i + 'A';
            int wt = adjMat[i][parent[i]];
            minCost += wt;
            printf("%c - %c \t%d\n", v1, v2, wt);
        }
    }
    printf("Minimum Spanning Tree: %d\n", minCost);
}

int main()
{
    printf("Prim's Algorithm in C\n");

    int vertices = 5;
    struct graph g[] =
        {
            {'A', 'B', 2},
            {'A', 'C', 7},
            {'A', 'D', 2},
            {'B', 'D', 5},
            {'B', 'E', 7},
            {'C', 'D', 5},
            {'D', 'E', 4}};

    int numEdges = sizeof(g) / sizeof(struct graph);
    primMST(vertices, numEdges, g);
    return 0;
}

// Prim's Algorithm in C
// Edges   Weight
// A - B   2
// D - C   5
// A - D   2
// D - E   4
// Minimum Spanning Tree: 13

.................................

# Write a Python program to implement the concept of Prim’s algorithm.
# Apply it to find the MST for the following graph.

#          2
#   A ------------ B
#   | \           / \
#   |  \         /   \
#  7|   \2      /     \
#   |    \     /5      \ 7
#   |     \   /         \
#   |      \ /           \
#   C ----- D ----------- E
#       5           4

class Graph:
    def __init__(self, v):
        self.V = v
        self.graph = [[0 for j in range(v)] for i in range(v)]

    def addEdge(self, u, v, w):
        u_index = ord(u) - 65
        v_index = ord(v) - 65
        self.graph[u_index][v_index] = w
        self.graph[v_index][u_index] = w

    def printMST(self, parent):
        print("Edge \tWeight")
        for i in range(1, self.V):
            print(
                f"{chr(parent[i]+65)} - {chr(i+65)} \t{self.graph[i][parent[i]]}")

    def minKey(self, key, mstSet):
        min = float('inf')
        min_index = -1
        for v in range(self.V):
            if key[v] < min and mstSet[v] == False:
                min = key[v]
                min_index = v
        return min_index

    def primMST(self):
        key = [float('inf')] * self.V
        parent = [None] * self.V
        key[0] = 0
        mstSet = [False] * self.V
        parent[0] = -1
        for i in range(self.V):
            u = self.minKey(key, mstSet)
            mstSet[u] = True
            for v in range(self.V):
                if self.graph[u][v] > 0 and mstSet[v] == False and key[v] > self.graph[u][v]:
                    key[v] = self.graph[u][v]
                    parent[v] = u
        self.printMST(parent)
        total_cost = sum([self.graph[i][parent[i]] for i in range(1, self.V)])
        print("Total minimum cost:", total_cost)


if __name__ == '__main__':
    print("Prim's algorithm in Python")
    g = Graph(5)
    g.addEdge('A', 'B', 2)
    g.addEdge('A', 'C', 7)
    g.addEdge('A', 'D', 2)
    g.addEdge('B', 'D', 5)
    g.addEdge('B', 'E', 7)
    g.addEdge('C', 'D', 5)
    g.addEdge('D', 'E', 4)
    g.primMST()


# OUTPUT
# Prim's algorithm in Python
# Edge    Weight
# A - B   2
# D - C   5
# A - D   2
# D - E   4
# Total minimum cost: 13

..................................

// Solve the following instances of the 0/1 Knapsack problem given the Knapsack capacity W=7
// Item  Weight  Value
// 1     3       10
// 2     2       12

#include <stdio.h>
#include <string.h>

struct Item
{
    int weight, value;
};

int knapSack(int W, struct Item arr[], int n)
{
    int dp[W + 1];
    memset(dp, 0, sizeof(dp));
    for (int i = 1; i < n + 1; i++)
    {
        for (int w = W; w >= 0; w--)
        {
            if (arr[i - 1].weight <= w)
                dp[w] = (dp[w] > (dp[w - arr[i - 1].weight] + arr[i - 1].value)) ? dp[w] : (dp[w - arr[i - 1].weight] + arr[i - 1].value);
        }
    }
    return dp[W];
}

int main()
{
    struct Item arr[] = {{3, 10}, {2, 12}};
    int W = 7;
    int n = sizeof(arr) / sizeof(struct Item);
    printf("0/1 Knapsack problem in C\n");
    printf("Knapsack Capacity: %d\n", W);
    printf("Item\tWeight\tValue\n");
    for (int i = 0; i < n; i++)
        printf("%d \t%d \t%d \n", i + 1, arr[i].weight, arr[i].value);
    printf("Maximum profit: %d\n", knapSack(W, arr, n));
    return 0;
}

// OUTPUT
// 0/1 Knapsack problem in C
// Knapsack Capacity: 7
// Item    Weight  Value
// 1       3       10
// 2       2       12
// Maximum profit: 22

................................

# Solve the following instances of the 0/1 Knapsack problem given the Knapsack capacity W = 7
# Item  Weight  Value
# 1     3       10
# 2     2       12

def knapSack(W, wt, val, n):
    dp = [0 for i in range(W+1)]
    for i in range(1, n+1):
        for w in range(W, 0, -1):
            if wt[i-1] <= w:
                dp[w] = max(dp[w], dp[w-wt[i-1]]+val[i-1])
    return dp[W]


if __name__ == '__main__':
    profit = [10, 12]
    weight = [3, 2]
    W = 7
    n = len(profit)
    print("0/1 Knapsack problem in Python")
    print("Knapsack Capacity:", W)
    print("Item\tWeight\tValue")
    for i in range(n):
        print(f"{i+1}\t{weight[i]}\t{profit[i]}")
    print(f"Maximum profit: {knapSack(W, weight, profit, n)}")


# OUTPUT
# 0/1 Knapsack problem in Python
# Knapsack Capacity: 7
# Item    Weight  Value
# 1       3       10
# 2       2       12
# Maximum profit: 22

..............................

// Implement a greedy algorithm and find the optimal solution to the fractional Knapsack
// instance n=7, m=15, (p1 p2 p3 p4 ......p7)=(1,5,10,10,5,7,8) and
// (w1,w2..........w7)=(3,2,5,7,2,8, 4).

#include <stdio.h>
#include <stdlib.h>

struct Item
{
    int value, weight;
};

int cmp(const void *a, const void *b)
{
    struct Item *itemA = (struct Item *)a;
    struct Item *itemB = (struct Item *)b;

    double r1 = (double)itemA->value / (double)itemA->weight;
    double r2 = (double)itemB->value / (double)itemB->weight;

    if (r1 > r2)
        return -1;
    else if (r1 < r2)
        return 1;
    else
        return 0;
}

double fractionalKnapsack(int W, struct Item arr[], int N)
{
    qsort(arr, N, sizeof(struct Item), cmp);
    double finalvalue = 0.0;
    for (int i = 0; i < N; i++)
    {
        if (arr[i].weight <= W)
        {
            W -= arr[i].weight;
            finalvalue += arr[i].value;
        }
        else
        {
            finalvalue += arr[i].value * ((double)W / (double)arr[i].weight);
            break;
        }
    }
    return finalvalue;
}

int main()
{
    int W = 15;
    struct Item arr[] = {{1, 3}, {5, 2}, {10, 5}, {10, 7}, {5, 2}, {7, 8}, {8, 4}};
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("Fractional Knapsack in C\n");
    printf("Knapsack Capacity: %d\n", W);
    printf("Item\tWeight\tValue\n");
    for (int i = 0; i < n; i++)
        printf("%d \t%d \t%d \n", i + 1, arr[i].weight, arr[i].value);
    printf("Maximum profit: %f", fractionalKnapsack(W, arr, n));
    return 0;
}

// OUTPUT
// Fractional Knapsack in C
// Knapsack Capacity: 15
// Item    Weight  Value
// 1       3       1
// 2       2       5
// 3       5       10
// 4       7       10
// 5       2       5
// 6       8       7
// 7       4       8
// Maximum profit: 30.857143

.................................

# Implement a greedy algorithm and find the optimal solution to the fractional Knapsack
# instance n = 7, m = 15, (p1 p2 p3 p4 ......p7) = (1, 5, 10, 10, 5, 7, 8) and
# (w1, w2..........w7) = (3, 2, 5, 7, 2, 8, 4).

class Item:
    def __init__(self, value, weight):
        self.value = value
        self.weight = weight
        self.ratio = value / weight


def fractional_knapsack(capacity, items):
    items.sort(key=lambda x: x.ratio, reverse=True)
    max_value = 0
    for item in items:
        if capacity == 0:
            return max_value
        elif item.weight <= capacity:
            capacity -= item.weight
            max_value += item.value
        else:
            max_value += capacity * item.ratio
            capacity = 0
    return max_value


if __name__ == "__main__":
    W = 15
    values = [1, 5, 10, 10, 5, 7, 8]
    weights = [3, 2, 5, 7, 2, 8, 4]
    items = [Item(values[i], weights[i]) for i in range(len(values))]
    n = len(weights)
    print("Fractional Knapsack in Python")
    print("Knapsack Capacity:", W)
    print("Item\tWeight\tValue")
    for i in range(n):
        print(f"{i+1}\t{weights[i]}\t{values[i]}")
    max_value = fractional_knapsack(W, items)
    print("Maximum profit:", max_value)


# OUTPUT
# Fractional Knapsack in Python
# Knapsack Capacity: 15
# Item    Weight  Value
# 1       3       1
# 2       2       5
# 3       5       10
# 4       7       10
# 5       2       5
# 6       8       7
# 7       4       8
# Maximum profit: 30.857142857142858

......................................

// Solve the following instance of "job scheduling with deadlines" problem:
// n = 7, profits (p1, p2, p3, p4, p5, p6, p7) = (3, 5, 20, 18, 1, 6, and 30)
// and deadlines (d1, d2, d3, d4, d5, d6, d7) = (1, 3, 4, 3, 2, 1, and 2).
// Schedule the jobs in such a way to get maximum profit.
// (Here only one machine is available)

#include <stdio.h>
#include <stdlib.h>

struct Job
{
    int id;
    int profit;
    int deadline;
};

int cmpfunc(const void *a, const void *b)
{
    struct Job *jobA = (struct Job *)a;
    struct Job *jobB = (struct Job *)b;
    return jobB->profit - jobA->profit;
}

void schedule_jobs(struct Job *jobs, int n)
{
    qsort(jobs, n, sizeof(struct Job), cmpfunc);
    int max_deadline = 0;
    for (int i = 0; i < n; i++)
    {
        if (jobs[i].deadline > max_deadline)
            max_deadline = jobs[i].deadline;
    }
    int *schedule = (int *)calloc(max_deadline, sizeof(int));
    for (int i = 0; i < n; i++)
    {
        int deadline = jobs[i].deadline - 1;
        while (deadline >= 0 && schedule[deadline] != 0)
            deadline--;
        if (deadline >= 0)
            schedule[deadline] = jobs[i].id;
    }

    printf("Scheduled jobs: ");
    int total_profit = 0;
    for (int i = 0; i < max_deadline; i++)
    {
        if (schedule[i] != 0)
        {
            printf("Job%d ", schedule[i]);
            for (int j = 0; j < n; j++)
            {
                if (jobs[j].id == schedule[i])
                {
                    total_profit += jobs[j].profit;
                    break;
                }
            }
        }
    }
    printf("\nTotal profit: %d\n", total_profit);
    free(schedule);
}

int main()
{
    printf("Job Scheduling with Deadlines in C\n");
    struct Job jobs[] = {{1, 3, 1}, {2, 5, 3}, {3, 20, 4}, {4, 18, 3}, {5, 1, 2}, {6, 6, 1}, {7, 30, 2}};
    int n = sizeof(jobs) / sizeof(struct Job);
    schedule_jobs(jobs, n);
    return 0;
}

// OUTPUT
// Job Scheduling with Deadlines in C
// Scheduled jobs: Job6 Job7 Job4 Job3
// Total profit: 74

........................................

# Solve the following instance of "job scheduling with deadlines" problem:
# n = 7, profits(p1, p2, p3, p4, p5, p6, p7) = (3, 5, 20, 18, 1, 6, and 30)
# and deadlines(d1, d2, d3, d4, d5, d6, d7) = (1, 3, 4, 3, 2, 1, and 2).
# Schedule the jobs in such a way to get maximum profit.
# (Here only one machine is available)

def schedule_jobs(profits, deadlines):
    jobs = list(zip(profits, deadlines))
    jobs = sorted(jobs, key=lambda x: x[0], reverse=True)
    slots = [False] * (max(deadlines) + 1)
    total_profit = 0
    scheduled_jobs = []
    for job in jobs:
        for i in range(job[1], 0, -1):
            if slots[i] == False:
                slots[i] = True
                total_profit += job[0]
                scheduled_jobs.append(job)
                break
    return (scheduled_jobs, total_profit)


print("Job Scheduling with Deadlines in Python")
profits = [3, 5, 20, 18, 1, 6, 30]
deadlines = [1, 3, 4, 3, 2, 1, 2]
scheduled_jobs, total_profit = schedule_jobs(profits, deadlines)
print("Scheduled jobs:", scheduled_jobs)
print("Total profit:", total_profit)

# OUTPUT
# Job Scheduling with Deadlines in Python
# Scheduled jobs: [(30, 2), (20, 4), (18, 3), (6, 1)]
# Total profit: 74

.....................................................

// Apply Dijkstra's Algorithm in C to find out the shortest
// path from node 'A' to all other nodes of the graph.

//         3
//   A ---------> B
//   |           /| \ 
//   |         /  |  \8
//   |     3 /    |   \ 
//  5|     /     5|    > C
//   |   /        |   /
//   | /          |  /2
//   v<           v /
//   E ---------> D
//         4

#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

struct graph
{
    char src;
    char dest;
    int weight;
};

int minDistance(int dist[], int visited[], int V)
{
    int min = INT_MAX, min_index;

    for (int v = 0; v < V; v++)
        if (visited[v] == 0 && dist[v] <= min)
            min = dist[v], min_index = v;

    return min_index;
}

void dijkstra(struct graph g[], int n, int V, int src)
{
    int adjMat[V][V];
    int dist[V];
    int visited[V];
    src = src - 'A';

    for (int i = 0; i < V; i++)
    {
        dist[i] = INT_MAX;
        visited[i] = 0;
        for (int j = 0; j < V; j++)
            adjMat[i][j] = 0;
    }
    dist[src] = 0;

    for (int i = 0; i < n; i++)
        adjMat[g[i].src - 'A'][g[i].dest - 'A'] = g[i].weight;

    for (int count = 0; count < V - 1; count++)
    {
        int u = minDistance(dist, visited, V);
        visited[u] = 1;
        for (int v = 0; v < V; v++)
        {
            if (!visited[v] && adjMat[u][v] && dist[u] != INT_MAX && dist[u] + adjMat[u][v] < dist[v])
                dist[v] = dist[u] + adjMat[u][v];
        }
    }

    printf("Vertex \t Distance from '%c'\n", src + 'A');
    for (int i = 0; i < V; i++)
        printf("%c \t %d\n", 'A' + i, dist[i]);
}

int main()
{
    printf("Dijkstra's Algorithm in C\n");
    int vertices = 5;
    struct graph g[] =
        {{'A', 'B', 3},
         {'A', 'E', 5},
         {'B', 'C', 8},
         {'B', 'D', 5},
         {'B', 'E', 3},
         {'D', 'C', 2},
         {'E', 'D', 4}};

    int numEdges = sizeof(g) / sizeof(g[0]);
    dijkstra(g, numEdges, vertices, 'A');
    return 0;
}

// OUTPUT
// Dijkstra's Algorithm in C
// Vertex   Distance from 'A'
// A        0
// B        3
// C        10
// D        8
// E        5


...............................


# Apply Dijkstra's Algorithm in Python to find out the shortest
# path from node 'A' to all other nodes of the graph.

#         3
#   A ---------> B
#   |           /| \
#   |         /  |  \8
#   |     3 /    |   \
#  5|     /     5|    > C
#   |   /        |   /
#   | /          |  /2
#   v<           v /
#   E ---------> D

import sys


class Graph:
    def __init__(self, vertices):
        self.V = vertices
        self.graph = [[0 for column in range(vertices)]
                      for row in range(vertices)]

    def add_edge(self, u, v, w):
        self.graph[ord(u) - 65][ord(v) - 65] = w

    def min_distance(self, dist, sptSet):
        min = sys.maxsize
        min_index = -1

        for v in range(self.V):
            if dist[v] < min and sptSet[v] == False:
                min = dist[v]
                min_index = v

        return min_index

    def dijkstra(self, src):
        dist = [sys.maxsize] * (self.V)
        dist[src] = 0
        sptSet = [False] * (self.V)
        for i in range(self.V):
            u = self.min_distance(dist, sptSet)
            sptSet[u] = True
            for v in range(self.V):
                if self.graph[u][v] > 0 and sptSet[v] == False and dist[v] > dist[u] + self.graph[u][v]:
                    dist[v] = dist[u] + self.graph[u][v]

        print(f"Vertex \tDistance from '{chr(src+65)}'")
        for node in range(self.V):
            print(f"{chr(node+65)} \t {dist[node]}")


if __name__ == '__main__':
    g = Graph(5)
    g.add_edge('A', 'B', 3)
    g.add_edge('A', 'E', 5)
    g.add_edge('B', 'C', 8)
    g.add_edge('B', 'D', 5)
    g.add_edge('B', 'E', 3)
    g.add_edge('D', 'C', 2)
    g.add_edge('E', 'D', 4)

    print("Dijkstra's algorithm in Python")
    start = ord('A')-65
    g.dijkstra(start)


# OUTPUT
# Dijkstra's algorithm in Python
# Vertex  Distance from A
# A        0
# B        3
# C        10
# D        8
# E        5

..................................

// Find out the minimal number of scaler Multiplication needed to multiply
// these matrices. The dimension of the matrices are 8 x 12, 12 x 13, 13 x 14,
// and 14 x 19. Apply Dynamic Programming (Bottom-up) approach.
// Here input is an array storing dimensions of the matrices like p={8,12,13,14,19}

#include <stdio.h>
#include <limits.h>

int mcm(int arr[], int n)
{
    int dp[n][n];
    for (int i = 1; i < n; i++)
        dp[i][i] = 0;

    for (int i = n - 1; i > 0; i--)
    {
        for (int j = i + 1; j < n; j++)
        {
            dp[i][j] = INT_MAX;
            for (int k = i; k < j; k++)
            {
                int steps = (arr[i - 1] * arr[k] * arr[j]) + dp[i][k] + dp[k + 1][j];
                if (steps < dp[i][j])
                    dp[i][j] = steps;
            }
        }
    }
    return dp[1][n - 1];
}

int main()
{
    printf("Matrix Chain Multiplication in C\n");
    int arr[] = {8, 12, 13, 14, 19};
    int n = sizeof(arr) / sizeof(arr[0]);
    int ans = mcm(arr, n);
    printf("Minimal number of scaler multiplications: %d", ans);
}

// OUTPUT
// Matrix Chain Multiplication in C
// Minimal number of scaler multiplications : 4832

.................................................

# Find out the minimal number of scaler Multiplication needed to multiply
# these matrices. The dimension of the matrices are 8 x 12, 12 x 13, 13 x 14,
# and 14 x 19. Apply Dynamic Programming(Bottom-up) approach.
# Here input is an array storing dimensions of the matrices like p = {8, 12, 13, 14, 19}


import sys


def mcm(arr):
    n = len(arr)
    dp = [[0 for j in range(n)] for i in range(n)]

    for i in range(n-1, 0, -1):
        for j in range(i+1, n):
            dp[i][j] = sys.maxsize
            for k in range(i, j):
                steps = dp[i][k] + dp[k+1][j] + arr[i-1]*arr[k]*arr[j]
                if steps < dp[i][j]:
                    dp[i][j] = steps
    return dp[1][n-1]


print("Matrix Chain Multiplication in Python")
arr = [8, 12, 13, 14, 19]
ans = mcm(arr)
print("Minimal number of scaler multiplications:", ans)

# OUTPUT
# Matrix Chain Multiplication in Python
# Minimal number of scaler multiplications: 4832

................................................

// For the given set of items and knapsack capacity = 5 kg,
// find the optimal solution for the 0/1 knapsack problem
// making use of dynamic programming approach.
// weight = [ 2, 3, 4, 5 ] and value = [ 3, 4, 5, 6 ]

#include <stdio.h>
#include <limits.h>
#define MAX(x, y) ((x) > (y) ? (x) : (y))

int knapsack(int wt[], int val[], int n, int maxWeight)
{
    int prev[maxWeight + 1];
    int take, notTake, W;
    for (int i = 0; i <= wt[0]; i++)
        prev[i] = 0;
    for (W = wt[0]; W <= maxWeight; W++)
        prev[W] = val[0];

    for (int ind = 1; ind < n; ind++)
    {
        for (W = maxWeight; W >= 0; W--)
        {
            notTake = prev[W];
            take = INT_MIN;
            if (wt[ind] <= W)
                take = val[ind] + prev[W - wt[ind]];
            prev[W] = MAX(take, notTake);
        }
    }
    return prev[maxWeight];
}

int main()
{
    printf("0/1 Knapsack problem in C\n");
    int wt[] = {2, 3, 4, 5};
    int val[] = {3, 4, 5, 6};
    int maxWeight = 5;
    int n = sizeof(wt) / sizeof(wt[0]);

    int profit = knapsack(wt, val, n, maxWeight);
    printf("Maximum Profit: %d", profit);
    return 0;
}

// OUTPUT
// 0/1 Knapsack problem in C
// Maximum Profit: 7

.......................................

# For the given set of items and knapsack capacity = 5 kg,
# find the optimal solution for the 0/1 knapsack problem
# making use of dynamic programming approach.
# weight = [2, 3, 4, 5] and value = [3, 4, 5, 6]


def knapsack(wt, val, n, maxWeight):
    prev = [0] * (maxWeight + 1)
    for i in range(wt[0], maxWeight + 1):
        prev[i] = val[0]

    for ind in range(1, n):
        for W in range(maxWeight, -1, -1):
            notTake = prev[W]
            take = float('-inf')
            if wt[ind] <= W:
                take = val[ind] + prev[W - wt[ind]]
            prev[W] = max(take, notTake)

    return prev[maxWeight]


print("0/1 Knapsack problem in Pyhton")
wt = [2, 3, 4, 5]
val = [3, 4, 5, 6]
maxWeight = 5
n = len(wt)

profit = knapsack(wt, val, n, maxWeight)
print("Maximum Profit:", profit)

# OUTPUT
# 0/1 Knapsack problem in Pyhton
# Maximum Profit: 7

.....................................

// Using dynamic programming determine longest common
// subsequence of (ABCBADCDF) and (CBAF).

#include <stdio.h>
#include <string.h>
#define MAX(x, y) ((x) > (y) ? (x) : (y))

void lcs(char s1[], char s2[])
{
    int n = strlen(s1);
    int m = strlen(s2);
    int dp[n + 1][m + 1];
    for (int i = 0; i <= n; i++)
        dp[i][0] = 0;
    for (int j = 0; j <= m; j++)
        dp[0][j] = 0;
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            if (s1[i - 1] == s2[j - 1])
                dp[i][j] = 1 + dp[i - 1][j - 1];
            else
                dp[i][j] = MAX(dp[i - 1][j], dp[i][j - 1]);
        }
    }

    int len = dp[n][m];
    char ans[len + 1];
    ans[len] = '\0';
    int index = len - 1;
    int i = n, j = m;

    while (i > 0 && j > 0)
    {
        if (s1[i - 1] == s2[j - 1])
        {
            ans[index] = s1[i - 1];
            index--, i--, j--;
        }
        else if (dp[i - 1][j] > dp[i][j - 1])
            i--;
        else
            j--;
    }

    printf("String 1: %s\n", s1);
    printf("String 2: %s\n", s2);
    printf("Longest common subsequence is: %s\n", ans);
}

int main()
{
    printf("LCS in C\n");
    lcs("ABCBADCDF", "CBAF");
    return 0;
}

// OUTPUT
// LCS in C
// String 1: ABCBADCDF
// String 2: CBAF
// Longest common subsequence is: CBAF

..........................................


# Using dynamic programming determine longest common
# subsequence of (ABCBADCDF) and (CBAF).

def lcs(s1, s2):
    n, m = len(s1), len(s2)
    dp = [[0] * (m + 1) for _ in range(n + 1)]
    for i in range(1, n + 1):
        for j in range(1, m + 1):
            if s1[i - 1] == s2[j - 1]:
                dp[i][j] = 1 + dp[i - 1][j - 1]
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

    length = dp[n][m]
    ans = [''] * (length + 1)
    i, j = n, m
    while i > 0 and j > 0:
        if s1[i - 1] == s2[j - 1]:
            ans[length] = s1[i - 1]
            length -= 1
            i -= 1
            j -= 1
        elif dp[i - 1][j] > dp[i][j - 1]:
            i -= 1
        else:
            j -= 1

    return ''.join(ans[1:])


print("LCS in python")
s1 = 'ABCBADCDF'
s2 = 'CBAF'
lcs_str = lcs(s1, s2)
print("String 1:", s1)
print("String 2:", s2)
print("Longest common subsequence is:", lcs_str)

# OUTPUT
# LCS in python
# String 1: ABCBADCDF
# String 2: CBAF
# Longest common subsequence is: CBAF

.........................................


// A circuit which passes through every vertex exactly
// once is called a Hamilton circuit. A minimum weight
// Hamilton circuit is a Hamilton circuit that has the
// smallest possible weight of all Hamilton circuits.
// In graph theory terms, the TSP is the problem of
// finding a minimum weight Hamilton circuit. Apply dynamic
// programming to find out the minimum weight Hamiltonian circuit.

/*

            1
          / | \
         /  |  \
        /   |10 \
    20 /    |    \
      /     2     \18
     /    /   \    \
    /   /       \   \
   /  /12        6\  \
  / /               \ \
  4 ----------------- 3
           18

*/

#include <stdio.h>
#include <limits.h>

#define MIN(x, y) ((x) < (y) ? (x) : (y))
#define V 4

int tsp(int graph[][V], int dp[][1 << V], int mask, int pos)
{
    if (mask == (1 << V) - 1)
        return graph[pos][0];
    if (dp[pos][mask] != -1)
        return dp[pos][mask];
    int min_weight = INT_MAX;
    for (int i = 0; i < V; i++)
    {
        if ((mask & (1 << i)) == 0)
        {
            int weight = graph[pos][i] + tsp(graph, dp, mask | (1 << i), i);
            min_weight = MIN(min_weight, weight);
        }
    }
    return dp[pos][mask] = min_weight;
}

int main()
{
    int graph[V][V] = {{0, 10, 18, 20},
                       {10, 0, 6, 12},
                       {18, 6, 0, 18},
                       {20, 12, 18, 0}};

    int dp[V][1 << V];
    for (int i = 0; i < V; i++)
        for (int j = 0; j < (1 << V); j++)
            dp[i][j] = -1;

    printf("Travelling Salesman Problem (TSP) in C\n");
    int min_weight = tsp(graph, dp, 1, 0);
    printf("Minimum weight Hamiltonian circuit: %d", min_weight);
    return 0;
}

// OUTPUT
// Travelling Salesman Problem (TSP) in C
// Minimum weight Hamiltonian circuit: 54


..............................................

# A circuit which passes through every vertex exactly
# once is called a Hamilton circuit. A minimum weight
# Hamilton circuit is a Hamilton circuit that has the
# smallest possible weight of all Hamilton circuits.
# In graph theory terms, the TSP is the problem of
# finding a minimum weight Hamilton circuit. Apply dynamic
# programming to find out the minimum weight Hamiltonian circuit.

'''

            1
          / | \
         /  |  \
        /   |10 \
    20 /    |    \
      /     2     \ 18
     /    /   \    \
    /   /       \   \
   /  /12        6\  \
  / /               \ \
  4 ----------------- 3
           18           

'''
import math


def tsp(adj_matrix):
    n = len(adj_matrix)
    dp = [[math.inf] * n for _ in range(2**n)]
    dp[1][0] = 0

    for mask in range(1, 2**n):
        for last in range(n):
            if not (mask & (1 << last)):
                continue
            for curr in range(n):
                if curr == last or not (mask & (1 << curr)):
                    continue
                dp[mask][curr] = min(dp[mask][curr], dp[mask ^ (
                    1 << curr)][last] + adj_matrix[last][curr])

    ans = math.inf
    for last in range(n):
        ans = min(ans, dp[2**n - 1][last] + adj_matrix[last][0])
    return ans


adj_matrix = [[0, 10, 18, 20],
              [10, 0, 6, 12],
              [18, 6, 0, 18],
              [20, 12, 18, 0]]

print("Travelling Salesman Problem (TSP) in Python")
print("Minimum weight Hamiltonian circuit:", tsp(adj_matrix))

# Output:
# Travelling Salesman Problem (TSP) in Python
# Minimum weight Hamiltonian circuit: 54

.................................................


// Apply Floyd Warshall algorithm to find out shortest
// path between every pairs of vertices of the graph
// shown below. The graph is stored in adjacency matrix.

//   ---               ---
//   | 0   3   8   ∞  -4 |
//   | ∞   0   ∞   1   7 |
//   | ∞   4   0   ∞   ∞ |
//   | 2   ∞  -5   0   ∞ |
//   | ∞   ∞   ∞   6   0 |
//   ---               ---

#include <stdio.h>
#include <limits.h>

#define V 5
#define INF INT_MAX

void floydWarshall(int graph[V][V])
{
    int dist[V][V];
    int i, j, k;

    for (i = 0; i < V; i++)
        for (j = 0; j < V; j++)
            dist[i][j] = graph[i][j];

    for (k = 0; k < V; k++)
        for (i = 0; i < V; i++)
            for (j = 0; j < V; j++)
                if (dist[i][k] != INF && dist[k][j] != INF && dist[i][k] + dist[k][j] < dist[i][j])
                    dist[i][j] = dist[i][k] + dist[k][j];

    printf("Shortest path matrix:\n");
    for (i = 0; i < V; i++)
    {
        for (j = 0; j < V; j++)
        {
            if (dist[i][j] == INF)
                printf("INF\t");
            else
                printf("%d\t", dist[i][j]);
        }
        printf("\n");
    }
}

int main()
{
    int graph[V][V] = {{0, 3, 8, INF, -4},
                       {INF, 0, INF, 1, 7},
                       {INF, 4, 0, INF, INF},
                       {2, INF, -5, 0, INF},
                       {INF, INF, INF, 6, 0}};

    printf("Floyd Warshall algorithm in C\n");
    floydWarshall(graph);
    return 0;
}

// Output:
// Floyd Warshall algorithm in C
// Shortest path matrix:
// 0       1       -3      2       -4
// 3       0       -4      1       -1
// 7       4       0       5       3
// 2       -1      -5      0       -2
// 8       5       1       6       0


.........................................


# Apply Floyd Warshall algorithm to find out shortest
# path between every pairs of vertices of the graph
# shown below. The graph is stored in adjacency matrix.

#   ---               ---
#   | 0   3   8   ∞  -4 |
#   | ∞   0   ∞   1   7 |
#   | ∞   4   0   ∞   ∞ |
#   | 2   ∞  -5   0   ∞ |
#   | ∞   ∞   ∞   6   0 |
#   ---               ---


INF = float('inf')


def floyd_warshall(adj_matrix):
    n = len(adj_matrix)
    dist = [[INF] * n for _ in range(n)]

    for i in range(n):
        for j in range(n):
            dist[i][j] = adj_matrix[i][j]

    for k in range(n):
        for i in range(n):
            for j in range(n):
                if dist[i][k] != INF and dist[k][j] != INF:
                    dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])

    return dist


adj_matrix = [[0, 3, 8, INF, -4],
              [INF, 0, INF, 1, 7],
              [INF, 4, 0, INF, INF],
              [2, INF, -5, 0, INF],
              [INF, INF, INF, 6, 0]]

print("Floyd Warshall algorithm in Python")
result = floyd_warshall(adj_matrix)
print("Shortest path matrix:")
for row in result:
    print(row)

# Output
# Floyd Warshall algorithm in Python
# Shortest path matrix:
# [0, 1, -3, 2, -4]
# [3, 0, -4, 1, -1]
# [7, 4, 0, 5, 3]
# [2, -1, -5, 0, -2]
# [8, 5, 1, 6, 0]


.......................................


// N - Queens problem is to place n - queens in
// such a manner on an n x n chessboard that no
// queens attack each other by being in the same
// row, column or diagonal. Apply Backtracking to
// generate all possible valid assignment of a 4- Queen problem.

#include <stdio.h>
#include <stdbool.h>

bool isSafe(int n, int board[][n], int row, int col)
{
    int i, j;

    for (i = 0; i < col; i++)
        if (board[row][i])
            return false;

    for (i = row, j = col; i >= 0 && j >= 0; i--, j--)
        if (board[i][j])
            return false;

    for (i = row, j = col; j >= 0 && i < n; i++, j--)
        if (board[i][j])
            return false;

    return true;
}

void printSolution(int n, int board[][n])
{
    static int solCount = 0;
    printf("Solution %d:\n", ++solCount);
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
            printf("%d ", board[i][j]);
        printf("\n");
    }
    printf("\n");
}

void solveNQueensUtil(int n, int board[][n], int col)
{
    if (col >= n)
    {
        printSolution(n, board);
        return;
    }

    for (int i = 0; i < n; i++)
    {
        if (isSafe(n, board, i, col))
        {
            board[i][col] = 1;
            solveNQueensUtil(n, board, col + 1);
            board[i][col] = 0;
        }
    }
}

void solveNQueens(int n)
{
    int board[n][n];
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            board[i][j] = 0;

    solveNQueensUtil(n, board, 0);
}

int main()
{
    int n;
    printf("N-Queen Problem in C\n");
    printf("Enter the value of N: ");
    scanf("%d", &n);
    solveNQueens(n);
    return 0;
}

// OUTPUT
// N-Queen Problem in C
// Enter the value of N: 4
// Solution 1:
// 0 0 1 0
// 1 0 0 0
// 0 0 0 1
// 0 1 0 0

// Solution 2:
// 0 1 0 0
// 0 0 0 1
// 1 0 0 0
// 0 0 1 0


............................


# N - Queens problem is to place n - queens in
# such a manner on an n x n chessboard that no
# queens attack each other by being in the same
# row, column or diagonal. Apply Backtracking to
# generate all possible valid assignment of a 4- Queen problem.


def is_valid(board, row, col, n):
    for i in range(row):
        if board[i][col] == 1:
            return False
    for i, j in zip(range(row, -1, -1), range(col, -1, -1)):
        if board[i][j] == 1:
            return False
    for i, j in zip(range(row, -1, -1), range(col, n)):
        if board[i][j] == 1:
            return False
    return True


def solve(board, row, n, solutions):
    if row == n:
        solutions.append([row[:] for row in board])
        return
    for col in range(n):
        if is_valid(board, row, col, n):
            board[row][col] = 1
            solve(board, row+1, n, solutions)
            board[row][col] = 0


def n_queens(n):
    board = [[0] * n for _ in range(n)]
    solutions = []
    solve(board, 0, n, solutions)
    return solutions


print("N - Queens Problem in Python")
n = int(input("Enter the value of N: "))
ans = n_queens(n)
count = len(ans)
if count == 0:
    print("No solution")
else:
    count = 1
    for i in ans:
        print("Solution:", count)
        for j in i:
            print(j)
        print()
        count += 1


# N - Queens Problem in Python
# Solution: 1
# [0, 1, 0, 0]
# [0, 0, 0, 1]
# [1, 0, 0, 0]
# [0, 0, 1, 0]

# Solution: 2
# [0, 0, 1, 0]
# [1, 0, 0, 0]
# [0, 0, 0, 1]
# [0, 1, 0, 0]



....................


// We are given a graph, we need to assign colors to the vertices of the graph. In the graph coloring
// problem, we have a graph and m colors, we need to find a way to color the vertices of the graph
// using the m colors such that any two adjacent vertices are not having the same color.
// Apply Backtracking to generate all possible valid coloring of the following graph. Here m = 3.

/*
    0-------1
    |      /|
    |    /  |
    |  /    |
    |/      |
    3-------2
*/

#include <stdio.h>
#include <stdbool.h>

#define V 4

bool isSafe(bool graph[V][V], int color[], int v, int c)
{
    for (int i = 0; i < V; i++)
        if (graph[v][i] && c == color[i])
            return false;
    return true;
}

void printColorings(int color[], int count)
{
    printf("Coloring %d: ", count);
    for (int i = 0; i < V; i++)
        printf("%d ", color[i]);
    printf("\n");
}

void graphColoringUtil(bool graph[V][V], int m, int v, int color[], int *count)
{
    if (v == V)
    {
        *count += 1;
        printColorings(color, *count);
        return;
    }

    for (int c = 1; c <= m; c++)
    {
        if (isSafe(graph, color, v, c))
        {
            color[v] = c;
            graphColoringUtil(graph, m, v + 1, color, count);
            color[v] = 0;
        }
    }
}

void graphColoring(bool graph[V][V], int m)
{
    int color[V] = {0};
    int count = 0;
    graphColoringUtil(graph, m, 0, color, &count);
    if (count == 0)
        printf("No valid coloring found.\n");
}

int main()
{
    bool graph[V][V] = {
        {0, 1, 0, 1},
        {1, 0, 1, 1},
        {0, 1, 0, 1},
        {1, 1, 1, 0}
    };

    int m = 3;

    printf("M-Coloring Graph problem in C\n");
    graphColoring(graph, m);
    return 0;
}

// OUTPUT
// M-Coloring Graph problem in C
// Coloring 1: 1 2 1 3
// Coloring 2: 1 3 1 2
// Coloring 3: 2 1 2 3
// Coloring 4: 2 3 2 1
// Coloring 5: 3 1 3 2
// Coloring 6: 3 2 3 1


..................................


# We are given a graph, we need to assign colors
# to the vertices of the graph. In the graph coloring
# problem, we have a graph and m colors, we need to
# find a way to color the vertices of the graph
# using the m colors such that any two adjacent
# vertices are not having the same color.
# Apply Backtracking to generate all possible
# valid coloring of the following graph. Here m = 3.

'''
    0-------1
    |      /|
    |    /  |
    |  /    |
    |/      |
    3-------2 
'''


def is_valid(graph, colors, vertex, color):
    for i in range(len(graph)):
        if graph[vertex][i] == 1 and colors[i] == color:
            return False
    return True


def solve(graph, colors, vertex, m, solutions):
    if vertex == len(graph):
        solutions.append(colors[:])
        return
    for color in range(1, m+1):
        if is_valid(graph, colors, vertex, color):
            colors[vertex] = color
            solve(graph, colors, vertex+1, m, solutions)
            colors[vertex] = 0


def graph_coloring(graph, m):
    colors = [0] * len(graph)
    solutions = []
    solve(graph, colors, 0, m, solutions)
    return solutions


print("M - Coloring Problem in Python")
graph = [[0, 1, 0, 1],
         [1, 0, 1, 1],
         [0, 1, 0, 1],
         [1, 1, 1, 0]]
m = 3
ans = graph_coloring(graph, m)
count = len(ans)
if count == 0:
    print("No solution")
else:
    count = 1
    for i in ans:
        print("Coloring", count, ":", i)
        count += 1

# Output:
# M - Coloring Problem in Python
# Coloring 1 : [1, 2, 1, 3]
# Coloring 2 : [1, 3, 1, 2]
# Coloring 3 : [2, 1, 2, 3]
# Coloring 4 : [2, 3, 2, 1]
# Coloring 5 : [3, 1, 3, 2]
# Coloring 6 : [3, 2, 3, 1]


...........................................
