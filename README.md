Download Link: https://assignmentchef.com/product/solved-eecs2031-lab6-structures-self-referential-structures-linked-list-in-c
<br>
<strong>Part I Pointer Arrays</strong> <strong>Problem A  </strong>

<strong>Motivation </strong>

It is usually a bit challenging to understand arrays of pointers, especially arrays of char pointers – how to access the pointee strings, what type of pointers can be assigned to the array and how to access the pointee strings via the pointer, and what a pointer array decays to etc. This practice aims at helping you get started.

<strong>  </strong>

<strong>Specification  </strong>

<ol>

 <li>Download file c. Read the first 30 lines of code, which provides a recap of pointer basics. Observe/recall that,

  <ol>

   <li>to print a scalar variable such as an integer variable via its pointer p, the argument to printf is the “pointee level” *p</li>

   <li>to print an char array (string) arr, the argument to printf is at the “pointer level”, i.e., array name arr or p where p = arr = &amp;arr[0]</li>

  </ol></li>

</ol>

Argument to library functions such as strlen strcpy is also at the “pointer level”

<ol>

 <li>to print an element of an array arr , e.g., a char in a string, the int in the int array, the argument to printf is at the “pointee level”, and there are several ways of doing that.</li>

</ol>

The basic rule is that

arr[i] == *(arr+i) == *(p+i)  where p = arr = &amp;arr[0]




<ol start="2">

 <li>Next, complete the “array of pointer to int” section (line 45 – line 70) by following the comments.

  <ul>

   <li>Hint: note that after initialization, arrP[0]  contains the pointer (i.e., address) of i, and arrP[1] contains the pointer to j and so on.  Now according to observation a above, to print the value of a scalar variable such as j, we pass a “piontee level” argument to printf. Hence  *arrP[1]. Moreover, according to 1.c, arrP[1] == *(arrP+1), so the argument can also be in the form of **(arrP+1).</li>

   <li>Hint2: If we want to declare a pointer pp0 that points to the first element of arrP, i.e., pp0 = &amp;arrP[0], what type of pp0 should it be? Since arrP[0] is a pointer to int, pp0 will contain  address &amp; of a pointer, so pp0 should be a <u>pointer to pointer</u>.  Also since array name arrP == &amp;arrP[0],  we can write pp0 = arrP Now according to 1.c above,  arrP[i] == *(arrP+i) == *(pp0+i). Hence to print value of j,  we can also pass **(pp0+1) as argument  to printf.</li>

  </ul></li>

</ol>




<ol start="3">

 <li>Next, complete the “array of char pointers” section (line 70 – line 110) by following the comments.

  <ul>

   <li>Hint3: note that for pointer array planets, after initialization, planets[0]  contains a pointer to string “Mercury” (more formally, planets[0]  stores the starting address of “Mercury” which is the address of its first element ‘M’).  Likewise planets[1]  contains the pointer to string “Venus” and so on.</li>

  </ul></li>

</ol>

Now according to observation 1.b above, to print a char array (string) we pass as argument to printf the array name or a pointer to the string (“pointer level”).  Thus to print “Mercury” we pass as argument to printf  a pointer to “Mercury”, which is planets[0] or *(planets+0),  and to print “Venus”, we pass as argument to printf a pointer to “Venus”, which is planets[1]  or *(planets+1), and so on.

<ul>

 <li>The reasoning for the type of pp0 described above (Hint 2), can help determine the type of pp and how to print the strings via pp.</li>

</ul>

<ol start="4">

 <li>Since planets[1] is a pointer to “Venus”, it is interesting to think about, following pointer arithmetic, what planets[1]+3 is, and what if  we pass planets[1]+3  to  printf(“%s”, )?

  <ul>

   <li>Consequently, what *(planets[1]+3) is?  Convince yourself that they are the former is the address of letter u in “Venus”.</li>

   <li>The last block shows how to use ‘pure’ pointer notations to access at the character level. Convince yourself that although they look quite daunting, they make sense. Notice that the parentheses are necessary to enforce the order of evaluation.</li>

  </ul></li>

</ol>




<ul>

 <li>One way to derive the pure pointer notations, as mentioned in class, is to ‘assume’ the same charcter can be accessed from planets[1][3] (actually this is the case), and then replace the brackts using the pointer notation.</li>

</ul>




<strong>Sample Inputs/Outputs</strong>  The final outputs of the program should be

red 329 % <strong>a.out</strong>

10




70 70 70

30 30 30

50 50 50

hello hello hello

5 5 5 llo llo llo

3 3 3  h h h e e e o o o

<a href="#_Toc27645">1                                                                             1 </a>

<a href="#_Toc27646">3                                                                             3 </a>

<a href="#_Toc27647">5                                                                             5 </a>




<h1><a name="_Toc27645"></a>1</h1>

<h1><a name="_Toc27646"></a>3</h1>

<h1><a name="_Toc27647"></a>5</h1>




Mercury Mercury 7 7

Venus  Venus

Jupiter  Jupiter Saturn  Saturn

Neptune  Neptune




Mercury Venus Jupiter iter  iter  iter




M i U o M  M i  i U  U o  o red 330 %

<strong>Submit your program using</strong><strong>   </strong><strong>submit 2031A lab6 lab6A.c</strong> <strong> </strong>

<strong>Problem B  </strong>

<strong>Subject      </strong>

Similarities and differences between 2D char array and array of char pointers, both of which can be used to store rows of input strings.

<strong> </strong>

<strong>Specification </strong>

Write an ANSI-C program that uses 2D array to read and store user input strings line by line, until a line of xxx is entered (similar to lab4).  The program then reorders the rows of inputs.

<strong> </strong>

<strong>Implementation </strong>

Download the file lab6B.c to start off. Assume that there are at least 4 lines of inputs (excluding the terminator line xxx) and there are no more than 30 lines of inputs.   Also assume that each line contains no more than MAXCOLS characters.  Note:  each line of input may contain spaces.

<ul>

 <li>Use a table-like <strong>2D array</strong> to store the user inputs. That is, similar to lab4, define char inputs[MAXLINES][MAXCOLS].</li>

 <li>First print the memory allocation for the 2D array using sizeof. You should get 1500 (bytes), as shown in the sample output.</li>

 <li>Use fgets to read in a line into the table row directly. Note that a trailing 
 is read in.</li>

 <li>When all the inputs have been read in (indicated by input line xxx), exchange data in row 0 and row 1 in main(), and then send the array to a function exchange2D() to exchange the data in the other rows, as shown below. Assume the inputs contain at least 4 lines.</li>

 <li>Define a function void exchange2D(char[][MAXCOLS], int n)which takes as</li>

</ul>

argument an 2D array, and swaps the data in the first n adjacent rows, except the first two rows, i.e., starting from 3<sup>rd</sup> row. Specifically, swaps the 3rd row with the 4th row, swaps the 5th row with the 6th row and so on. If n is an odd number, then the last row is not swapped.

<ul>

 <li>Define a function void print2D(char[][MAXCOLS], int n)which takes as argument a 2D array, and then prints the first n rows of the array on stdout.</li>

</ul>

Use this function in main to display all the stored rows of the array, both before and after swapping and sorting.




Notice that for the 2D array, similar to general 1D array, when passing to a function, we also need an extra argument n to indicate the function where to stop the processing, as there no

“terminator row” in the 2D array.

<strong> </strong>

<strong>Sample Inputs/Outputs: </strong>

red 329 % <strong>a.out </strong>sizeof inputs: 1500




Enter string: <strong>giraffes 0 </strong>

Enter string: <strong>zebras 1</strong>

Enter string: <strong>monkeys 2 </strong>

Enter string: <strong>kangaroos 3</strong>

Enter string: <strong>do you like them? 4</strong>

Enter string: <strong>yes 5 </strong>

Enter string: <strong>thank you 6 </strong>

Enter string: <strong>bye 7 </strong>

Enter string: <strong>xxx </strong>




[0]: giraffes 0

[1]: zebras 1

[2]: monkeys 2

[3]: kangaroos  3

[4]: do you like them? 4

[5]: yes 5

[6]: thank you 6

[7]: bye  7




== after swapping ==

[0]: zebras 1

[1]: giraffes 0

[2]: kangaroos 3

[3]: monkeys 2

[4]: yes 5

[5]: do you like them? 4

[6]: bye 7

[7]: thank you 6




red 330 % <strong>a.out &lt; inputB.txt </strong>sizeof inputs: 1500




Enter string: Enter string: Enter string: Enter string: Enter string:

Enter string: Enter string: Enter string: Enter string:

[0]: giraffes are high 0

[1]: mosquitos are annoying 1

[2]: monkeys are smart 2

[3]: kangaroos are funny 3

[4]: dogs are friendly 4

[5]: hippos are huge 5

[6]: cobras are scary 6

[7]: fox 7

[8]: elephants are heavy 8

[9]: hens 9

[10]: bison 10




== after swapping ==

[0]: mosquitos are annoying 1

[1]: giraffes are high 0

[2]: kangaroos are funny 3

[3]: monkeys are smart 2 [4]: hippos are huge 5

[5]: dogs are friendly 4

[6]: fox 7

[7]: cobras are scary 6

[8]: hens 9

[9]: elephants are heavy 8

[10]: bison 10 red 331 %

Submit your program using     <strong>submit 2031A lab6 lab6B.c </strong>

After you submitted, as an additional practice, change the formal argument in one of the function definitions (and the corresponding declaration) from char[][MAXCOLs] to char [][], for example, void exchange2D(char[][]), and compile. What do you get?

<strong> </strong>

<strong>Problem C   (25 pts) </strong>

<strong>Subject   </strong>

Similarities and differences between 2D char array and array of char pointers.

Store strings using Array of (char) Pointers. Pass array of pointers to functions.  Swap records of pointer arrays.

<strong> </strong>

<strong>Specification </strong>

Write an ANSI-C program that reorders the pointees of a pointer array.




<strong>Implementation </strong>

<ul>

 <li>Download the program cand start from there. Observe how an array of char pointers is declared and initialized.</li>

 <li>In main, first exchange pointees of the first (element [0]) and the 2<sup>nd</sup> (element [1]) pointers of the pointer array. For example, if the first pointer points to “Hello” and the second pointer points to “World”, then after exchange, the first pointer points to “World” and the 2<sup>nd</sup> pointer points to “Hello”.</li>

 <li>Then, send the pointer array to function exchangeParr() to exchange some other pointees as given below.</li>

 <li>Define a function void exchangeParr(char * pArr[], int n)which takes as</li>

</ul>

argument an array of char pointers, and swaps the pointees pointed by the first n pointers, except the first two pointers, i.e., starting from the 3<sup>rd</sup> pointer. That is, swap the pointee of the 3<sup>rd</sup> element pointer with that of the fourth element pointer, pointee of 5<sup>th</sup> element pointer with that of the 6<sup>th</sup> etc. If n is an odd number then the last pointee is not swapped. o You should accomplish the swapping without copying/moving the original string data.  Thus the function should have <em>O(1)</em> time complexity. Specifically, you should not use library functions or loops to do the swapping. This is one of the potential advantages of using pointer arrays against 2-D arrays.  <strong>You can use array index notation [], and/or pointer notation in the function. </strong>

<ul>

 <li>Define a function void printParr(char pArr[], int n) which takes as argument</li>

</ul>

an array of char pointers, and prints the first n pointees of pArr on stdout, one line for each pointee of the array.  <strong>You can use array index notation [], or pointer notation. </strong>Use this function in main to display all the pointees pointed by the pointer array, both before and after swapping.

Note that since pArr is a ‘general array’ which contains no terminator token, we need to pass n as additional argument for the length information.

<ul>

 <li>Define a function void printParr2(char ** pArr, int n) which takes as</li>

</ul>

argument an array of char pointers, and prints the first n pointees of records on stdout, one line for each pointee of the array.  <strong>Use pointer notation only, don’t use array index notation [] in this function. </strong>

Use this function in main to display all the pointees pointed by the pointer array, after the swapping.

Note that the argument is declared as a pointer to pointer char **, which is what an array of char pointer char *[] is “decayed” to when it is passed to a function (why? Recall that array name contains the address of its first element. Thus when array is passed function, it is decayed to the address of its first element. Since this is a pointer array, the first element is a pointer, so address of a pointer, i.e., a pointer to pointer, is received by the function.)




<strong>Sample Inputs/Outputs: </strong>

red 329 % <strong>a.out </strong>

sizeof char*: 8, size of pointer array: 88




<ul>

 <li>-*-&gt; giraffes are high 0</li>

 <li>-*-&gt; mosquitos are annoying 1</li>

 <li>-*-&gt; monkeys are smart 2</li>

 <li>-*-&gt; kangaroos are funny 3</li>

 <li>-*-&gt; dogs are friendly 4</li>

 <li>-*-&gt; hippos are huge 5</li>

 <li>-*-&gt; cobras are scary 6</li>

 <li>-*-&gt; fox 7</li>

 <li>-*-&gt; elephants are heavy 8</li>

 <li>-*-&gt; hens 9</li>

 <li>-*-&gt; bison 10</li>

</ul>




== after swapping ==

<ul>

 <li>-*-&gt; mosquitos are annoying 1</li>

 <li>-*-&gt; giraffes are high 0</li>

 <li>-*-&gt; kangaroos are funny 3</li>

 <li>-*-&gt; monkeys are smart 2</li>

 <li>-*-&gt; hippos are huge 5</li>

 <li>-*-&gt; dogs are friendly 4</li>

 <li>-*-&gt; fox 7</li>

 <li>-*-&gt; cobras are scary 6</li>

 <li>-*-&gt; hens 9</li>

 <li>-*-&gt; elephants are heavy 8</li>

 <li>-*-&gt; bison 10</li>

</ul>




<ul>

 <li>-*-&gt; mosquitos are annoying 1</li>

 <li>-*-&gt; giraffes are high 0</li>

 <li>-*-&gt; kangaroos are funny 3</li>

 <li>-*-&gt; monkeys are smart 2</li>

 <li>-*-&gt; hippos are huge 5</li>

 <li>-*-&gt; dogs are friendly 4</li>

 <li>-*-&gt; fox 7</li>

 <li>-*-&gt; cobras are scary 6</li>

 <li>-*-&gt; hens 9</li>

 <li>-*-&gt; elephants are heavy 8</li>

 <li>-*-&gt; bison 10 red 330 %</li>

</ul>

Submit your program using     <strong> submit 2031A lab6 lab6C.c </strong>

<strong> </strong><strong>Problem D   (25 pts) </strong>

<strong>Subject:</strong><strong>  </strong>

Command line arguments (program parameters) and pass pointer arrays to functions.

<strong> </strong>

<strong>Background: </strong>

Command line argument is a parameter supplied to the program when it is invoked. Commandline arguments are given after the name of the executable program (e.g. a.out) in commandline shell of Operating Systems.  In addition to scanf, fgets, command line argument provides another way for the program to interact with users.

<strong> </strong>

<strong>Specification  </strong>

Write a (short) ANSI-C program that reads command line inputs, which begins with either sum or diff,  followed by two or more integer literals. The program then outputs the sum of the input integers if the arguments begin with sum, or the difference of the integers if the arguments begin with diff.

<strong> </strong>

<strong>Implementation </strong>

<ul>

 <li>In main, first display the total number of command-line arguments, excluding the executable file name. Then, if the command-line arguments begin with sum, list the integer literals separated by + sign, and then call function getSum() to get the sum of the integer literals. If the command-line arguments begin with diff, list the integer literals separated by – sign, and then call function getDiff() to get the difference of the integer literals</li>

 <li>Define a function int getSum(char *[], int n), which takes as argument an array of n char pointers where, except the first two pointers, all other pointers point to strings of integer literals, and then returns the sum of the integer literals.</li>

 <li>Define a function int getDiff(char *[], int n), which takes as argument an array of n char pointers where, except the first two pointers, all other pointers point to strings of integer literals, and then returns “difference” of the integers. <strong>Here we define the difference as the result of the first integer literal (pointed by the 3<sup>rd</sup> pointers) minus all the other pointed integers. </strong></li>

</ul>




<ul>

 <li>Do not use global variables.</li>

 <li>Name your program lab6Dargv.c</li>

 <li>Assume all command-line arguments begin with either sum or diff, followed by two or more integer literals.</li>

</ul>

<strong> </strong>

<strong>Sample Inputs/Outputs:    </strong>

red 377 % <strong>gcc lab6Dargv.c </strong>red 378 % <strong>a.out sum 1 3 </strong>

There are 3 arguments (excluding “a.out”)

<ul>

 <li>+ 3 = 4</li>

</ul>

red 379 % <strong>a.out sum 2 3 4 23 11 32 345 17 220 5</strong> There are 11 arguments (excluding “a.out”)

<ul>

 <li>+ 3 + 4 + 23 + 11 + 32 + 345 + 17 + 220 + 5</li>

</ul>

= 662

red 380 % <strong>a.out diff 1 3 </strong>

There are 3 arguments (excluding “a.out”)

1 – 3

= -2 red 379 % <strong>a.out diff 345 11 3 4 </strong>

There are 5 arguments (excluding “a.out”)

345 – 11 – 3 – 4

= 327

red 380 % <strong>gcc lab6Dargv.c -o xyz.out </strong>red 381 % <strong>xyz.out sum 2 5 6 19 40 </strong>

There are 6 arguments (excluding “xyz.out”)

2 + 5 + 6 + 19 + 40

= 72 red 382 % <strong>xyz.out diff 6 19 40 </strong>

There are 4 arguments (excluding “xyz.out”)

6 – 19 – 40 = -53 red 383 %

Name your program lab6Dargv.c and submit using <strong>submit 2031A lab6 lab6Dargv.c </strong>

<strong> </strong>

<strong>Part II Dynamic memory allocation Problem II-A </strong>

<strong>Subject:  </strong>Dynamically allocate array space, using malloc or calloc.




<strong>Specification </strong>

Write a (short) ANSI program that prompts the user for the size of an int array, and then creates the array dynamically (i.e., at run time).




<strong>Implementation </strong>

Download program lab6malloc.c. This program tries to create an array based on user entered size at run time. Observe how the array element is set using pointer notation.

Compile using<strong>  </strong><strong>gcc -ansi -pedantic-errors lab6malloc.c </strong>This complies the

program following ANSI (C90) standard strictly. Observe the error message <strong><em>ISO C90 forbids variable length array ‘my_array’.</em></strong>  No a.out was generated.

As mentioned in class, ANSI (C90) standard does not support variable-length array. That is, the array size should be a constant in the code so that the necessary memory space is allocated at compile time. To generate “dynamic” array at run time, in ANSI C we need to use malloc or calloc to allocate memory dynamically.

<ul>

 <li>Fix the program by allocating the array space dynamically, using malloc or calloc. Allocate needed space only.</li>

</ul>




Note: by using <strong>-ansi -pedantic-errors </strong>option of<strong> gcc, </strong>here we are following ANSI standard strictly. In order to pass compilation, your program cannot mix declarations and other code — need to declare all variables at the beginning. Also, cannot use // for comment.  (For all other questions, we don’t have these restrictions.)




<strong>Sample Inputs/Outputs: </strong>

red 388 % <strong>gcc -ansi -pedantic-errors lab6malloc.c    </strong> red 389 % <strong>a.out </strong>

# of elements in int array: <strong>1</strong>                         No more error <sub>message “</sub><strong><em><sub>ISO C90 </sub></em></strong>

[0]: -10    <strong><em>forbids variable length array …</em></strong>” red 390 % <strong>a.out</strong>

# of elements in int array: <strong>3</strong>

[0]: -10

[1]: 100 [2]: 200 red 391 % <strong>a.out</strong>

# of elements in int array: <strong>-20</strong>

Segmentation fault (core dumped) red 392 % <strong>a.out</strong>

# of elements in int array: <strong>1000000000000000</strong>

Segmentation fault (core dumped) red 393 %




Memory allocation by malloc or calloc may fail, in that case the program crashes. Thus if your program generates <em>Segmentation fault</em> for some input size, as shown above, that means you did not check the result of memory allocation. Fix the program by checking the result of memory allocation and if the allocation was not successful (how to detect this?), then display an error message “Memory allocation failed. Bye!” and exit the program (kind of like catching an exception in Java).

<strong> </strong>

<strong>Sample Inputs/Outputs: </strong>

red 388 % <strong>gcc -ansi -pedantic-errors lab6malloc.c    </strong> red 389 % <strong>a.out </strong>

# of elements in int array: <strong>1</strong>                     No more error message “<strong><em>ISO C90 </em></strong>

[0]: -10    <strong><em>forbids variable length array …</em></strong>” red 390 % <strong>a.out</strong>

# of elements in int array: <strong>3</strong>

[0]: -10

[1]: 100 [2]: 200 red 391 % <strong>a.out</strong>

Program terminates “peacefully”.

# of elements in int array: <strong>1000000000000000</strong>

No “segmentation fault”.

Memory allocation failed. Bye! red 392 % <strong>a.out</strong>

# of elements in int array: <strong>-20</strong> Memory allocation failed. Bye! red 393 %




Now uncomment the last block. Observe that the pointer (address) returned from malloc, which is casted into char*, can be passed to strlen(p), and printf(“%s”, p).  Complete the line above the printf statement and run again so that the sample output is generated. Recall we mentioned in class that for storing strings into the allocated memory space, you can either store character directly, using *(p+i) = ‘X’, or, pass the address to some string functions.




<strong>Sample Inputs/Outputs: </strong>

red 388 % <strong>gcc -ansi -pedantic-errors lab6malloc.c    </strong>




red 389 % <strong>a.out </strong>

# of elements in int array: <strong>1</strong>

[0]: -10

Hello 5 heXlo red 390 % <strong>a.out</strong>

# of elements in int array: <strong>3</strong>

[0]: -10

[1]: 100

[2]: 200  hello 5 heXlo red 391 % <strong>a.out </strong>

# of elements in int array: <strong>8</strong>

[0]: -10

[1]: 100

[2]: 200

[3]: 300

[4]: 400

[5]: 500

[6]: 600

[7]: 700  hello 5 heXlo red 393 % <strong>a.out </strong>

# of elements in int array: <strong>1000000000000000 </strong>

Memory allocation failed. Bye!

red 394 %

<strong> </strong>

<strong>No submission for this exercise. </strong>

<strong> </strong>

<strong>Problem II-B  (5+5+10 pts) </strong>

<strong>Subject  </strong>

Array of pointers. Dynamic memory allocation.  Heap.

No more error  message “<strong><em>ISO C90 forbids variable length array …</em></strong>”

Program terminates “peacefully”.

No “segmentation fault”.




In addition to allocating memory dynamically, another important feature of memory allocation functions malloc/calloc/realloc is that they are the ways in C to request a memory space in <strong>Heap</strong>, rather than in <strong>Stack</strong>. Local variables declared in a function (including main function) are stored in stack, where their memory storage are deallocated when the defining function exits (that’s why a local variable‘s lifetime ends automatically when its defining function returns). Heap memory space, on the other hand, provides persistent storage where the allocated memory remains allocated until the programmer explicitly requests that the space be deallocated (using free()). Nothing happens automatically.




<strong>Implementations </strong>

<ol>

 <li>Download, read, compile and run setArrMain.c. This simple program declares an array of int pointers and set the pointer in main. Note that variables a,b,c,d and e are local variables in main so they are stored in stack, but they will be deallocated only when main Hence as long as the program is running, these local variables are ‘alive’ and their memory addresses are valid. Thus the program runs well.</li>

</ol>

Observe how the values of the int pointees are accessed in printf at “pointee level”, using

*arr[i], which can also be written as **(arr+i).




Setting all the pointers in main is not that practical. The other provided programs setArr1.c and setArr2.c set the array of integer pointers through a void function

setArr(int index, int v). This function intends to set the pointers at index index to point to an integer of value v. Then in main, the programs intend to print out the pointees of the first 5 pointer elements, which should be -10,100,200,300,400.

<ol>

 <li>Download, compile and run c, and observe what happens. <strong>Write at the end of the program your explanation of the outputs. </strong></li>

</ol>




<ol start="2">

 <li>Download, compile and run c, and observe what happens. Run again and you probably see different results.</li>

</ol>

Is this version better than the previous version? A little bit, at least it did not crash.  <strong>Write at the end of the program your explanation of the outputs. </strong>




<ol start="3">

 <li>Both the two programs compile successfully but either does not work or does not work correctly. Fix the program by modifying the function setArr(). The program should produce the expected output as show below. You should not use global or static variables.</li>

</ol>

Name the new program setArr3.c.

red 316 % <strong>a.out</strong> arr[0] -*-&gt; -10 -10 arr[1] -*-&gt; 100 100 arr[2] -*-&gt; 200 200 arr[3] -*-&gt; 300 300 arr[4] -*-&gt; 400 400 red 317%




Submit your programs using

<strong>submit 2031A lab6 setArr1.c setArr2.c setArr3.c    </strong>or  <strong>submit 2031A lab6 setArr?.c   </strong>or

<strong>submit 2031A lab6 setArr[1-3].c  </strong>




(The ? and [1-3] are Unix shell filename wildcards, which we will discuss in class shortly.)

<strong> </strong>

<strong> </strong>

<strong>Part III Structures in C </strong>

<strong> </strong>

<strong>Problem III-A  (10 pts) </strong>

<strong>Subject:  </strong>Structure declaration, initialization and assignment. <strong> </strong>

<strong> </strong>

<strong>Implementation</strong>

Download file lab6struct.c. Look at the existing code, and then complete the program by following the comments.  Observe

<ul>

 <li>how a structure type is defined</li>

 <li>how a struct variable is declared and initialized at declaration o if a struct variable is declared but not initialized, its members get random/garbage values.</li>

 <li>how a struct variable’s member values are set after declaration, and how the values are retrieved.</li>

 <li>that, when a struct variable is assigned/copied to another struct variable o the values of the members are copied</li>

</ul>

o the two structures are independent. Changing members of one struct does not affects the other.

&#x25aa;   However, if the structure has pointer member, then after copy, both pointers point to the same pointee (kind of like ‘’shallow copy” in Java. ) If the pointee is modified, the change can be seen via both structures.

<ul>

 <li>how a struct variable with array as element is declared and initialized at declaration</li>

</ul>




<strong>Sample Inputs/Outputs: </strong>(The hexadecimal memory address would be different from here)

red 326 % <strong>a.out</strong>

———– simple struct ————– a: 32 4

b: 4196576 0                Random/garbage values

a: 100 4 b: 100 4




Enter value for b.data2: <strong>5937</strong> a: 100 4 b: 700 5937

——- struct with pointer member —————– xx: 5 0x7fffa2b65b1c 100 yy: 5 0x7fffa2b65b1c 100

<sup>      </sup>You might get different values for addresses c: 10000

xx: 5 0x7fffa2b65b1c 10000 yy: 5 0x7fffa2b65b1c 10000

——- struct with array member ——————

2 [100 400] red 327 %




<strong>Submission   </strong>Submit your program by issuing   <strong>submit 2031A lab6 lab6struct.c </strong>




<strong> </strong>

<strong>Problem III-A2   (10 pts) </strong>

<strong>Subject:  </strong>Structure and functions, array of structures, pointer and malloc for structures. <strong> </strong>

<strong> </strong>

<strong>Implementation</strong>

Download file lab6struct2.c.  compete the program, and observe, •            how a struct can be passed to a function as argument.

o both function getSum(struct ints) and getSum2()work correctly, but  o function processStruct(struct ints) does not work as expected.

&#x25aa;   fix the definition of function processStruct(struct ints) as well as its function call, so that argument structure can be modified correctly.

<ul>

 <li>how a function can be declared to return a structure. By returning a structure, the function can return more than one values by encapsulating multiple values into a struct.

  <ul>

   <li>Implement function getSumDiff(int, int), which calculates and returns the sum and difference of the two argument integers.</li>

  </ul></li>

 <li>how an array of structures is declared, initialized at declaration, and set after declaration</li>

 <li>how to use malloc/calloc to allocate space for a structure (in <strong>heap</strong>), if needed, and how to set member values via the pointer.

  <ul>

   <li>set the member values via the pointer returned by malloc/calloc o observe that from a structure pointer p, the structure’s member can be accessed using either (*p).data and p -&gt; data</li>

  </ul></li>

 <li>how an array of pointers to structures are declared. The pointers in the array are initially uninitialized. If needed, how to use malloc, calloc to allocate space for each pointer, and how to set the values using different approaches and notations. o Complete the code to access the members of the structures pointed by the array elements.</li>

</ul>




<strong>Sample Inputs/Outputs: </strong>

red 326 % <strong>a.out</strong>

——– struct and function —————– elements sum of a: 104 elements sum of a: 104




struct a before processing: 100 4 struct a after  processing: 101 104




Enter two integers: <strong>2 43</strong> sum is: 45, diff is -41

——— array of structs —————- arr[0]: 1 2 arr[1]: 3 4 arr[2]: 5 6

——— pointer to structs, with malloc —————-

Two member values: 777 888

——— array of pointers to structs, with malloc ——– pArr[0] -*-&gt; {22, 33} pArr[1] -*-&gt; {44, 55} red 327 %

<strong> </strong>

<strong>Submission   </strong>Submit your program by issuing   <strong>submit 2031A lab6 lab6struct2.c </strong>

<strong>Part IV Self-referential structures (Structures + Dynamic memory allocation)     </strong>

<strong> </strong>

<strong>Background:  Singly Linked list </strong>

Skip this section if you are familiar with linked list data structure and its basic operations.




A linked list consists of a chain of structures (called nodes), with each node containing a pointer (in Java this is called a ‘reference’) to the next node in the chain.







Note that the last node in the list contains a NULL pointer/reference.




To build up a linked list, the first thing we need is a structure that represents a single node in the list. For simplicity, let’s assume that a node contains only one integer data field. So a node struct contains nothing but an integer (the node’s data) and a reference/pointer to the next node in the list.

Here is how a node class is defined in Java:




Class Node {   int data;   Node next;

};




Here is how a node structure is defined in C:

struct node {   int data;   struct node * next;

};

Note that the next field has type struct node *, which means it can store the address of  another node structure (which is, of course, of the same type of this node).




Now that we have the node structure declared, we need a way to keep track of where the list begins. In other words, we need a pointer variable that always points to the first node in the list, which serves as our only access point to the whole list. Let’s name the variable head:

struct node * head;




Note that when the list is empty, head is NULL.




<strong>Insert a new node into the list </strong>

In general, creating and inserting a new node to the list requires three main steps:

<ol>

 <li>Allocate memory for the new node (how?)</li>

 <li>Store data in the node</li>

 <li>Insert the node into the list, which involves finding the proper place for the new node, and setting the next pointer of the new node and its ‘neighbors’ properly.</li>

</ol>

<strong> </strong>

<strong>Remove a node from the list </strong>

Deleting a node also involves three main steps

<ol>

 <li>Locate the node to be deleted</li>

 <li>Alter the next pointer of the previous node so that it ‘bypasses’ the deleted node 3. (Optional) Free the space occupied by the deleted node.</li>

</ol>

<strong>Linked list implementation in Java. </strong>

Download file MyLinkedList.java. This is a simplified Java implementation of Linked-list data structure. While you might never need to implement a linked list like this in Java (Java provides a Linked List data structure in its Collections package), reading this simplified implementation may help you understand some features of the Linked List data structure. For example, from the method get(int n), you can observe that getting the value of n’th element in the list involves visiting each of the first n nodes, hence <em>O(n)</em> time complexity, (whereas in Array, were elements are stored in memory consecutively,  this is accomplished by just going to address p + n*unitsize  directly, hence <em>O(1)</em> time complexity).

Compared against C, implementing Linked List in Java is relatively straightforward.   Compile and run the program to see the interesting outputs.

red 327 % javac MyLinkedList.java

red 328 % java  MyLinkedList

<strong> </strong>

<strong>Problem IV-0 </strong>

<strong>Subject:  </strong>Linked list implementation on stack (in main)

<strong> </strong>

<strong>Implementation:  </strong>

Download file lab6LL0.c, look at the code and play with it. Observe that this implementation, which is not very practical, creates nodes and link them directly. It works.

<strong> </strong>

<strong>Problem IV-1 </strong>

<strong>Subject</strong><strong>  </strong>

Linked list implementation on stack (in function)




<strong>Implementation:  </strong>

Download file lab6LL1.c, which moves the repeated implementation of insertion into a function insertBegining(). The code of insertBegining() imitates the code of method insertBegining() in MyLinkedList.java.

Compile and run the program, what did you get?

This is the implementation that had perplexed me for many years, as I could not figure out why the Java version insertBegining() in MylinkedList.java, which the C code imitates, works well, and the C code lab6LL0.c also works well,  but not this code.

Can you see the problem?  Hint: recall program setArr2.c which you just did in part II?




<strong>Problem IV-2   (20 pts) </strong>

<strong>Subject</strong><strong>  </strong>

Linked list implementation on heap.

<strong> </strong>

<strong>Implementation: </strong>

Fix the implementation of insertBegining()in lab6LL1.c, name the new program lab6LL2.c. Also implement functions len(), get().




<strong>Sample output: </strong>

red 330 % <strong>a.out</strong> 500 400 300 200 100 len: 5 get(0): 500 get(1): 400 get(3): 200

red 331 %




<strong>Submission:             </strong>Submit using<strong> submit 2031A lab6 lab6LL2.c </strong>

<strong> </strong>

Based on the prior practice, in programming assignment 2 you will be implementing a fullfledged Linked list data structure in C.




<strong> </strong>

<strong>In summary, for this lab, you should submit the following files: </strong>

<strong>Part I:   </strong><strong>lab6A.c  lab6B.c   lab6C.c  lab6Dargv.c</strong><strong>   </strong>

<strong>Part II:  </strong><strong>setArr1.c setArr2.c setArr3.c </strong>

<strong>Part III: </strong><strong>lab6struct.c lab6struct2.c </strong>

<strong>Part IV:  </strong><strong>lab6LL2.c  </strong>

<strong> </strong>

You can issue <strong>submit -l 2031A lab6</strong> in the terminal.

<strong> </strong>

<strong>Common Notes </strong>

All submitted files should contain the following header:

/***************************************

<ul>

 <li>EECS2031A – Lab 6 *</li>

 <li>Author: Last name, first name *</li>

 <li>Email: Your email address *</li>

 <li>eecs_num: Your eecs login username *</li>

 <li>Yorku #: Your York student number</li>

</ul>

****************************************/





