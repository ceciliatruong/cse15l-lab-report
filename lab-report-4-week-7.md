# Week 7 Lab Report
## Part 1
My lab partner and I decided to change the name of `start` parameter and its uses to `base`.
Below are the commands we performed.

`vim DocSearchServer.java/start<Enter>dwibase<Esc>ndwibase<Esc>ndwibase<Esc>:wq<Enter>`

`vim DocSearchServer.java` 

`/start<Enter>`, moves the cursor to the beginning of the word being searched in the file
![](images\silly-lab-images.jpg)

 `dw`, deletes the `start` term 
 ![](images\delete.jpg)

 `ibase<Esc>`, insert `base` term in place of start
 ![](images\insert-base.jpg)

 `ndw`, go to the next `start` term and delete it
 ![](images\delete-again.jpg)

 `ibase<Esc>`, insert `base` again
 ![](images\insert-again.jpg)

 `ndw`, go to the next `start` term and delete it
 ![](images\delete-3.jpg)

 `ibase<Esc>`, insert `base` term in place of start 
 ![](images\insert3.jpg)

 `:wq<Enter>`, save the revisions. 

 Note: We decided to not change the final start in the file becuse it was in the DocSearchServer class and it ultimately served a different purpose from the rest of the starts that we changed.

 ## Part 2
 1. Editing the file directly
 * Time took: 32 secs
 * Difficulties/details: With the editing task that I chose, all I had to do was `<Ctrl>`+`F` the start term and type in base for every instance of start. I found this method a lot easier and more intuitive since I'm used these commands.
 2. Editing the file through `vim`
 * Time took: 41 secs
 * Difficulties/details: I followed the commands above that my lab partner and I came up with during lab. I mainly had trouble being quick enough with my inputs because I found it hard to connecting the meaning of the commands to the commands itself.

 Reflection Questions:
 1. Which of these two styles would you prefer using if you had to work on a program that you were running remotely, and why?
 * I prefer the first method of editing directly on the file since I'm not as comfortable or familiar with `vim` commands. The first method feels a lot more intuitive as I've stated before since I just have to use what I already know to work on a program. 
 2. What about the project or task might factor into your decision one way or another? (If nothing would affect your decision, say so and why!)
 * I would use the first method no matter what the project or task may be. Even if there may be a quicker way to work on a program with `vim`, I would still use the first method since it would take a proficient amount of time to learn `vim` for me to naturally come up with a solution in `vim`. Despite this, I can understand how the power of being able to edit from the terminal can be useful so that would be a factor that would make me want to use `vim`.    
