computers/machines can only understand machine language i.e. binary/bits 1’s & 0’s.

So our computational power is different ways of orchestration of these bits,  to make them do our requirements/calculations/programs.

So, first let’s look at the hardware.

1’s 0’s are voltages present and not present.

So the hardware to perform these 1s and 0s evolved like this:

Mechanical / Electromagnetic parts - Big, clanky, hot, slow .

Vacuum tubes - Removed mechanical clunks but still huge.

Transistors - Semi conductors - Real inflection moment - tiny,

no heat, no mechanical wear. can be mass produced, densely packed, cheap.

Integrated Circuits (IC’s) - transistors bunched on a silicon wafer (silicon wafer acts as a connector)

Micro processors - Entire CPU on a chip.

CPU has different individual computing parts like Registers, ALU, Control logic etc.…. 

When switches were huge, each part used to have its own set of compute hardware / switches. 
Now hardware is so tiny that you put all the parts of cpu on a single silicon wafer. The modern chip (cpu).

Previously the hardware was so huge and slow that we can only afford to run a single program with the entire machine.  Eventually as hardware became fast and efficient, it enabled us to do multiple process/programs. So now why use this capable hardware for single program, why dedicate entirety of it for a single program. 

The first operating system is born. 
Basically an operating system is a manager that manages multiple processes to run on the single hardware we have. The first operating system is UNIX. 

Now for a machine to do what we want it to do, we need to tell it i.e., tell the hardware/ our orchestration of switches in the language of 0’s and 1’s - this is binary language / machine language.
You directly talk to hardware/machine in machine language - this is tedious. 
Initially the instructions to a machine were given through punching cards (our way to convey 0’s and 1’s to machines).
Then Assembly took birth , assembly is just human interpretable form of writing binary operations.
Now for this assembly to get converted into machine language we first should prepare a program or set of instructions based on which our assembly language is converted into binaries. That is Assembler. 
So first Assembler is machine with machine language , because we first created instructions of how the language we write should be converted into binaries so that the hardware can understand what we are doing through the assembly language.

First assembler is made in machine language so that it can compile/convert some assembly code into binaries. Then we write a new assembler code in assembly and use our previous assembler (written in machine code) to help us compile this new assembler written in assembly. 
Thus new assembler written in assembly is born. In this way we can improve the compiler with the language we are using it to compile. This is called *Bootstrapping.* 

Now the point in history is this: we are at hardware/computer which are called PDP-7. 
On this now we have UNIX, Assembly, Assembler. Now the language we used to operate this machine is called “B” programming language.

From this point there are two things made possible from one important inflection point.
1. Birth of C programming language.  2. Portable Operating System.

For the above two points to make sense we need to go back to hardware. 
Every chip/CPU has its own micro-architecture, so the same machine code is differently understood by different hardware/chip/cpu because the architecture of the compute hardware to process those bits is different. So each cpu architectures has their own set of rules to understand machine code, that is called ISA, Instruction set Architecture. 

Now before PDP-7 the hardware was so primitive that there is no scope for operating system. The compute hardware was slow, so using that to run only a single program made sense. Not even running multiple processes or programs was not even efficient and feasible. If our compute is so primitive, then why waste further compute on operating system use if for a program.

Note that this piece of writing is not intended to be accurate wrt what actually happened in history, this is give myself a sense where things actually came from - so that it will help me make more sense in software journey.

But with PDP-7 Unix is born, first operating system for managing multi-processes. Unix was then written in assembly. So the operating system is not portable across compute hardwares of different architectures. Since unix is written in assembly and assembly directly deals with hardware. So when the hardware changes the assembly code also had to be written again for unix os. So unix os is not portable.

Now one of the most important  inflection point: birth of *‘C’ programming language and how it made the operating system portable.*

During the era of PDP-7 the memory is like this due to contemporary hardware. Each memory unit is addressed as a 18bit word. i.e., the lowest memory unit that we can address with our computer language (at that time B was used on pdp 7) B  is a 18bit word. Today we use int, char ; different data types with different byte sizes, because we are able address memory as bytes. But pdp 7 can only address 18bit chunks due to hardware at that time, so for any operation of entities that are of size less that 18 bits - first you get that 18bit memory unit , then perform bitwise operations like bit-masking etc… i.e. use only bits you want and remaining of those 18bits are unused. So obviously different data types were not possible, no abstraction beyond hardware limitation is possible. Soon people wanted more flexibility but B couldn’t because of word addresssing way of it’s existence.

Then came PDP-11, here the hardware allowed “*byte-addressability of memory”.*  This naturally allowed the beginning of a more flexible language “C”. Now we have data types, structs, pointers are now more feasible because the pointer arithmetic evolved like this:

previously in B : ptr1 = 18 bit word, ptr1+1 (next ptr) = another 18 bit word. 
now in C: ptr_char points to char type (mem location = 00) , ptr_char + 1  points to mem location 01.

            ptr_int points to int type (mem location = 06), ptr_int + 1 points to mem location 08 (06 + 2bytes [size of int]).

next ptr = currt ptr mem + no.of bytes of data type. 

now the pointer arithmetic makes more sense and exactly mirrors hardware. 

Ok, now C is born. Now how C made operating system portable. This is beautiful actually. 

So at or before PDP-7, the hardware was **word-addressed**. For example, PDP-7 was **18-bit word-addressable**, and other machines were **24-bit** or **36-bit word-addressable**. So the **entire hardware model itself changed from machine to machine**.

1. The hardware model itself was different. The **lowest addressable unit was a word**, and that lowest addressable unit **varied across machines**.
2. If you write a programming language for these hardwares, then for **each hardware**, pointer arithmetic differed, character storage differed, and language semantics differed. There was **no stable common abstraction** on which programming languages could operate.

When **byte addressing** was introduced, the **lowest addressable unit of hardware became common across different machines**. Byte addressing was now the same across hardware platforms.

Because byte addressability was common, **abstract computing concepts could be defined**. Data types became compatible with byte addressing, pointer arithmetic became consistent across machines, and language semantics could be shared across hardware.

This **unifying nature of byte addressing** gave rise to **portable abstract concepts**, which were formalized in the **C programming language**.

This is the beauty of C, the first formalized abstraction of computing concepts wrt hardware. So, because of this reason C when you write code in C the writer gets to know exactly how he is dealing with memory. 

Now, the beauty in other way. C doesn’t hide hardware. It directly Interacts with it. Whatever code we do in C directly touches hardware, literally, whatever we write (right or wrong) - No restrictions. That is C is both powerful and dangerous. 

The beauty, C is where hardware abstraction and software bare bones meet. 

Previously Unix is not portable because it was written in assembly and also the hardware’s basic units themselves were different for each type of system. So to the entire code of OS has to be re-written for that another type of system. 

Now, Portability was achieved by writing only a small hardware-dependent compiler and runtime in assembly for each new architecture, then recompiling the existing C-based operating system’s code since the abstract computing concepts are same. This bootstrapping approach eliminated the need to rewrite the entire OS for every machine.
Thus the re-written Unix in C, became portable. Such a major explosive point of even this is.

Beautiful and powerful enabler.

 
Actually I have read much more and gone a bit deeper, this is the condesation of my exploration that removed doubts in my brain regarding the current state of software and hardware. Surprisingly, this cleared so much unknown-ness because I actually understood the birth of core principle of Computer engineering, Compilers and Operating systems.
