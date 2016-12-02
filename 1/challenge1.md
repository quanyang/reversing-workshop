# Challenge 1

Download the challenge binary from [here]("challenge1.exe").

## Start


We are given a binary, the first step is to identify what kind of binary it is.

```
$ file challenge1.exe
challenge1.exe: PE32 executable for MS Windows (console) Intel 80386 32-bit
```

Since its a Windows PE, boot up your Windows environment and play around with it.

So it seems, the executable is asking for some kind of password.

Let's begin reversing with IDA. Let's first learn some useful shortcut keys in IDA.

The few shortcuts useful are:

- spacebar - Used to change to/from callgraph view.  
- shift-f12 - View strings in binary.  
- x - Find cross references to a memory address.  
- n - Rename function  
- ; - Add comments to an instruction
- esc - Back to previous location
- ctrl+enter - Forward to earlier location

The first step to reversing anything is to be able to identify the functions or instruction segments which is interesting to us. In this case, we need to be able to find the password for this challenge and we know that there must be some comparison or check for a correct password.

#### Activity - 5 Minutes
[**Activity**] Find the function of interest in this challenge. Let's call this the main function to make things easier.
***Hint: "Enter password:"***

Now that we found function we can clearly see from the callgraph view that based on the result of the comparison, the execution would branch into either of the two basic block; one of them printing `Correct!`, which is probably where we want the execution to end up in.

From here we can then trace execution back to the instruction responsible for deciding which basic block to branch to.  
[**Activity**] Could you find the function responsible for deciding which basic block to branch to?

#### Activity - 3 Minutes
Before we start reversing the other functions, lets take another look at the main function.  
[**Activity**] The password is assigned to a local variable in this function can you find it?

[**Activity**] Is the hardcoded password the answer to this challenge?

#### Activity - 20 Minutes
Since we now know that the password is encoded, there are two ways to perform authentication here.

1. Decode password and compare with user-input.
2. Encode user-input and compare with encoded password.

[**Activity**] Determine which method is used in this particular challenge.

Spend some time exploring the other functions found so far.

[**Activity**] It appears that a popular encoding method is used here, are you able to identify it?

[**Activity**] Does decoding the password work? Why doesn't it work?

#### Activity - 15 Minutes

[**Activity**] Find the plaintext password and obtain the flag!
***Hint: You might have to write a script to decoded the encoded password. :)***
 

## Takeaway
- Learning how to use IDA pro.
- Learning how to begin analysing a binary.
- Learning how to Google.
- Learning some basic script writing.


