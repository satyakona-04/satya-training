package com.journaldev.javaprograms;

import java.util.Arrays;

public class JavaArraySort {

	public static void main(String[] args) {
		int[] array = {2,1,5,3,4,6,7};
		
		int[] sortedArray = bubbleSortAscending(array);
		
		System.out.println(Arrays.toString(sortedArray));
	}

	public static int[] bubbleSortAscending(int[] arr){
        int temp;
        for(int i=0; i < arr.length-1; i++){
             
            for(int j=1; j < arr.length-i; j++){
                if(arr[j-1] > arr[j]){
                    temp=arr[j-1];
                    arr[j-1] = arr[j];
                    arr[j] = temp;
                }
            }
            //check that last index has highest value in first loop,
            // second last index has second last highest value and so on
            System.out.println("Array after "+(i+1)+"th iteration:"+Arrays.toString(arr));
        }
        return arr;
    }
}
There are many sorting algorithms, bubble sort is easier to implement.
Sorting is complex and you should rely on Java API methods for sorting a collection or array for better performance that inventing the wheel again.
Also mention the use of Comparable and Comparator in sorting will add bonus points for you.
Read 3 input Strings, concat and print

package com.journaldev.javaprograms;

import java.util.Scanner;

public class ReadStringAndConcat {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter number of Strings to Concatenate:");
		int n = scanner.nextInt();
		
		String[] input = new String[n];
		for(int i=0; i<n; i++) {
			System.out.println("Please enter String number "+n+" and press enter:");
			input[i] = scanner.next();
		}
		//close Scanner and avoid resource leak
		scanner.close();
		String output = concat(input);
		System.out.println("Concatenation Result = "+output);
	}

	private static String concat(String[] input) {
		StringBuilder sb = new StringBuilder();
		for(String s : input) sb.append(s);
		return sb.toString();
	}

}
Program is flexible to concat any number of strings, that shows thinking to code reuse and keeping it flexible.
Proper messages to guide the user when someone runs the program.
Use of StringBuilder rather than String + operator for concatenation.
Closing resources as soon as we are done with it, hence avoiding memory leak. Shows good programming habits.
Remove odd numbers from integer array

package com.journaldev.javaprograms;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;

public class RemoveOddNumbers {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter comma separated numbers for input int array, for example '1,2,3,4'");
		String input = scanner.next();
		scanner.close();
		//convert to int array
		String[] inArray = input.split(",");
		int [] intArray = new int[inArray.length];
		int index = 0;
		for(String s : inArray) {
			intArray[index] = Integer.parseInt(s.trim());
			index++;
		}
		//call a function to remove odd numbers
		Integer[] result = removeOddNumbers(intArray);
		
		System.out.println(Arrays.toString(result));
	}

	private static Integer[] removeOddNumbers(int[] intArray) {
		//we will have to use list because we don't know exact size of the result array
		List<Integer> list = new ArrayList<>();
		for(int i : intArray) {
			if(i%2 == 0) list.add(i);
		}
		
		return list.toArray(new Integer[list.size()]);
	}

}
If you are reading this code, you should see that it adheres to all the points mentioned above. Try to write clean and simple code, follow best practices, naming conventions for methods and variables and you will be good.

Delete all matching elements from a list

package com.journaldev.javaprograms;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import java.util.Scanner;

public class DeleteFromList {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter comma separated list of Strings. For example 'a,b,c,b,a'");
		String input = scanner.next();
		System.out.println("Enter String to remove from the input list.");
		String strToDelete = scanner.next();
		scanner.close();

		List<Object> inputList = new ArrayList<>();
		String[] inputStrings = input.split(",");
		for (String s : inputStrings)
			inputList.add(s.trim());
		
		inputList = removeAll(inputList, strToDelete);
		System.out.println("Result List = "+inputList);
	}

	private static List<Object> removeAll(List<Object> inputList, Object objToDelete) {
		Iterator<Object> it = inputList.iterator();
		while(it.hasNext()) {
			Object obj = it.next();
			if(obj.equals(objToDelete)) it.remove();
		}
		return inputList;
	}

}
Notice the removeAll method is created for list of objects, so it will work with any type of list. This is how we write reusable code.
Using iterator to remove the element from the list.
Trimming the input to remove any accidental white spaces from input strings.
Average of numbers with rounding half-up and scale 2

package com.journaldev.javaprograms;

import java.math.BigDecimal;
import java.math.RoundingMode;
import java.util.Scanner;

public class AverageOfNumbers {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Please enter the total number of integers.");
		int count = scanner.nextInt();

		int sum = 0;

		for (int i = 0; i < count; i++) {
			System.out.println("Please enter number " + (i + 1) + ":");
			sum += scanner.nextInt();
		}
		System.out.println("Sum=" + sum + ",Count=" + count);

		BigDecimal average = new BigDecimal((double) sum / count);
		average = average.setScale(2, RoundingMode.HALF_UP);
		System.out.println("Average of entered numbers = " + average);
		scanner.close();
	}

}