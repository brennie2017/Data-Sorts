/*
 * File:   main.c
 * Author: Dr. T
 */

#define _CRT_SECURE_NO_WARNINGS

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define BUBBLE_SORT 1
#define SELECTION_SORT 2
#define INSERTION_SORT 3

#define RANDOM 1
#define ALMOST_SORTED 2
#define BACKWARDS 3

// helper functions
void printAlgorithmMenu();
int getSortAlgorithm();
int getSize();
void printDataFileMenu();
int getDataFile();
void readData(int data[], int size, int dataFile);

// iterative sorting algorithms
void bubbleSort(int array[], int count);
void selectionSort(int array[], int count);
void insertionSort(int array[], int count);
void swapElements(int firstLocation, int secondLocation, int array[]);

/*
 * Collects data for Programming Assignment 6
 */
int main(int argc, char** argv)
{
    // get sort algorithm to use
    int sortAlgorithm = getSortAlgorithm();
    
    // get number of data points to use
    printf("\n");
    int size = getSize();
    
    // get data file to use
    printf("\n");
    int dataFile = getDataFile();
    
    // read data from file
    int* data = malloc(size * sizeof(int));
    readData(data, size, dataFile);
    
    // get sort time
    clock_t startTime = clock() / (CLOCKS_PER_SEC / 1000);
    if (sortAlgorithm == BUBBLE_SORT)
    {
        bubbleSort(data, size);
    }
    else if (sortAlgorithm == SELECTION_SORT)
    {
        selectionSort(data, size);
    }
    else
    {
        insertionSort(data, size);
    }
    clock_t endTime = clock() / (CLOCKS_PER_SEC / 1000);
    clock_t elapsedTime = endTime - startTime;
    
    // output results
    FILE *outputFile = fopen("times.txt", "a");
    if (outputFile == NULL)
    {
        printf("\n");
        printf("Output file open failed\n");
        return(EXIT_FAILURE);
    }
    
    // print algorithm name
    printf("\n");
    if (sortAlgorithm == BUBBLE_SORT)
    {
        fprintf(outputFile, "%s,", "Bubble Sort");
        printf("Bubble Sort\n");
    }
    else if (sortAlgorithm == SELECTION_SORT)
    {
        fprintf(outputFile, "%s,", "Selection Sort");
        printf("Selection Sort\n");
    }
    else
    {
        fprintf(outputFile, "%s,", "Insertion Sort");
        printf("Insertion Sort\n");
    }
    
    // print size
    fprintf(outputFile, "%d,", size);
    printf("Size: %d\n", size);
    
    // print data ordering
    if (dataFile == RANDOM)
    {
        fprintf(outputFile, "%s,", "Random");
        printf("Random data\n");
    }
    else if (dataFile == ALMOST_SORTED)
    {
        fprintf(outputFile, "%s,", "Almost Sorted");
        printf("Almost sorted data\n");
    }
    else
    {
        fprintf(outputFile, "%s,", "Backwards");
        printf("Backwards data\n");
    }
    
    // print sort time
    fprintf(outputFile, "%.0Lf\n", (long double)elapsedTime);
    printf("Duration : %.0Lf milliseconds\n", (long double)elapsedTime);
    
    // close file
    fclose(outputFile);
    
    // free memory
    free(data);
    data = NULL;
    
    printf("\n");
    return (EXIT_SUCCESS);
}

/*
 * Prints the menu of algorithms
 */
void printAlgorithmMenu()
{
    printf("Sorting Algorithms\n");
    printf("------------------\n");
    printf("1  Bubble Sort\n");
    printf("2  Selection Sort\n");
    printf("3  Insertion Sort\n");
    printf("\n");
}

/*
 * Gets a sort algorithm from the user
 */
int getSortAlgorithm()
{
    int answer = 0;
    printAlgorithmMenu();
    printf("Enter algorithm number (1-3): ");
    scanf("%d", &answer);
    while (answer < 0 || answer > 3)
    {
        printf("\n");
        printf("Algorithm number must be between 1 and 3!\n");
        printf("\n");
        printAlgorithmMenu();
        printf("Enter algorithm number (1-3): ");
        scanf("%d", &answer);
    }
    return answer;
}

/*
 * Gets the number of data points to use
 */
int getSize()
{
    int size;
    printf("Enter size (multiples of 10000 up to 100000): ");
    scanf("%d", &size);
    while (size < 10000 || size > 100000 || (size % 10000 != 0))
    {
        printf("\n");
        printf("Size must be a multiple of 10000 up to 100000");
        printf("\n");
        scanf("%d", &size);
    }
    return size;
}

/*
 * Prints the menu of data files
 */
void printDataFileMenu()
{
    printf("Data Files\n");
    printf("------------------\n");
    printf("1  random.txt (random data)\n");
    printf("2  almostsorted.txt (almost sorted data)\n");
    printf("3  backwards.txt (backwards data)\n");
    printf("\n");
}

/*
 * Gets a data file from the user
 */
int getDataFile()
{
    int answer = 0;
    printDataFileMenu();
    printf("Enter data file number (1-3): ");
    scanf("%d", &answer);
    while (answer < 0 || answer > 3)
    {
        printf("\n");
        printf("Data file number must be between 1 and 3!\n");
        printf("\n");
        printDataFileMenu();
        printf("Enter data file number (1-3): ");
        scanf("%d", &answer);
    }
    return answer;
}

/*
 * Reads in size data points from the given data file
 * and puts them in the data array
 */
void readData(int data[], int size, int dataFile)
{
    char *fileName = malloc(sizeof(char) * 100);
    if (dataFile == RANDOM)
    {
        fileName = "random.txt";
    }
    else if (dataFile == ALMOST_SORTED)
    {
        fileName = "almostsorted.txt";
    }
    else
    {
        fileName = "backwards.txt";
    }
    
    // open file for reading
    FILE *inputFile = fopen(fileName, "r");
    
    // read data into array
    char currentLine[100];
    for (int i = 0; i < size; i++)
    {
        fgets(currentLine, 100, inputFile);
        data[i] = atoi(currentLine);
    }
    
    // close file
    fclose(inputFile);
}

/*
 * Sorts the given array using bubble sort
 */
void bubbleSort(int array[], int count)
{
    // work from right to left
    for (int k = count - 1; k > 0; k--)
    {
        // traverse unsorted portion of array
        for (int i = 0; i < k; i++)
        {
            // check for a swap
            if (array[i] > array[i + 1])
            {
                swapElements(i, i + 1, array);
            }
        }
    }
}

/*
 * Sorts the given array using selection sort
 */
void selectionSort(int array[], int count)
{
    // work from left to right
    for (int k = 0; k < count; k++)
    {
        int minLocation = k;
        
        // traverse unsorted portion of array
        for (int i = k + 1; i < count; i++)
        {
            // check for a new minimum location
            if (array[i] < array[minLocation])
            {
                minLocation = i;
            }
        }
        
        // swap the elements
        swapElements(k, minLocation, array);
    }
}

/*
 * Sorts the given array using insertion sort
 */
void insertionSort(int array[], int count)
{
    // process array from left to right
    for (int k = 1; k < count; k++)
    {
        // set new value to be inserted
        int value = array[k];
        
        // find insertion point for new value, shifting as we go
        int i = k - 1;
        while (i >= 0 &&
               value < array[i])
        {
            array[i + 1] = array[i];
            i--;
        }
        
        // insert new value
        array[i + 1] = value;
    }
}

/*
 * Swaps the elements at the first location and the second location
 * in the given array
 */
void swapElements(int firstLocation, int secondLocation, int array[])
{
    int temp = array[firstLocation];
    array[firstLocation] = array[secondLocation];
    array[secondLocation] = temp;
}
