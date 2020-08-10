---
title: How to Create and Use Array in Bash Script
zid: KB-2008041019
tags:
- cli
- bash
- array
---



#### by Rahul, [tecadmin.net](https://tecadmin.net/working-with-array-bash-script/) ▪ Thursday, September 27, 2018, 5:53 AM

An array is a data structure consist multiple elements based on key pair basis. Each array element is accessible via a key index number.

This tutorial will help you to create an Array in bash script. Also, initialize an array, add an element, update element and delete an element in the bash script.

You have two ways to create a new array in bash script. The first one is to use declare command to define an Array. This command will define an associative array named test\_array.

declare -a test\_array 

In another way, you can simply create Array by assigning elements.

test\_array=(apple orange lemon) 

Similar to other programming languages, Bash array elements can be accessed using index number starts from 0 then 1,2,3…n. This will work with the associative array which index numbers are numeric.

echo ${test\_array\[0\]} apple 

To print all elements of an Array using @ or \* instead of the specific index number.

echo ${test\_array\[@\]} apple orange lemon 

You can also access the Array elements using the [loop in the bash script](https://tecadmin.net/tutorial/bash-scripting/bash-for-loop/). A loop is useful for traversing to all array elements one by one and perform some operations on it.

for i in ${test\_array\[@\]} do echo $i done

for  i  in  ${test\_array\[@\]}

You can add any number of more elements to existing array using (+=) operating. You just need to add new elements like:

test\_array+=(mango banana) 

View the array elements after adding new:

echo ${test\_array\[@\]} apple orange lemon mango banana 

To update the array element, simply assign any new value to the existing array by the index. Let’s change the current array element at index 2 with grapes.

test\_array\[2\]=grapes 

View the array elements after adding new:

echo ${test\_array\[@\]} apple orange grapes mango banana 

You can simply remove any array elements by using the index number. To remove an element at index 2 from an array in bash script.

unset test\_array\[2\] 

View the array elements after adding new:

echo ${test\_array\[@\]} apple orange mango banana

---

Clipped on Tuesday, August 4, 2020, 10:19 AM