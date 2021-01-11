# Search-an-element-in-a-sorted-and-rotated-array
An sorted array of integers was rotated an unknown number of times.  Given such an array, find the index of the element in the array in faster than linear time. If the element doesn't exist in the array, return null.  For example, given the array [13, 18, 25, 2, 8, 10] and the element 8, return 4 (the index of 8 in the array).  You can assume all the integers in the array are unique.

#include <bits/stdc++.h> 
using namespace std; 
  
// Returns index of key in arr[l..h] if 
// key is present, otherwise returns -1 
int search(int arr[], int l, int h, int key) 
{ 
    if (l > h) 
        return -1; 
  
    int mid = (l + h) / 2; 
    if (arr[mid] == key) 
        return mid; 
  
    /* If arr[l...mid] is sorted */
    if (arr[l] <= arr[mid]) { 
        /* As this subarray is sorted, we can quickly 
        check if key lies in half or other half */
        if (key >= arr[l] && key <= arr[mid]) 
            return search(arr, l, mid - 1, key); 
        /*If key not lies in first half subarray,  
           Divide other half  into two subarrays, 
           such that we can quickly check if key lies  
           in other half */
        return search(arr, mid + 1, h, key); 
    } 
  
    /* If arr[l..mid] first subarray is not sorted, then arr[mid... h] 
    must be sorted subarray */
    if (key >= arr[mid] && key <= arr[h]) 
        return search(arr, mid + 1, h, key); 
  
    return search(arr, l, mid - 1, key); 
} 
  
// Driver program 
int main() 
{ 
    int arr[] = { 4, 5, 6, 7, 8, 9, 1, 2, 3 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int key = 6; 
    int i = search(arr, 0, n - 1, key); 
  
    if (i != -1) 
        cout << "Index: " << i << endl; 
    else
        cout << "Key not found"; 
} 
