Task: To watch C based and RISCV based lab videos and execute the task of compiling the C code using gcc and riscv compiler


1. Compiling C code with gcc

    step1 : create a C file in the home directory

                  leafpad sum1ton.c

      and write the C code
   
      ![Screenshot 2024-07-17 090905](https://github.com/user-attachments/assets/437a9fcd-ee0b-4cd1-b023-ec7d79d3b77a)

   step2 : compile the C code using gcc command as shown below

                  gcc sum1ton.c  # for compiling sum1ton.c
   
                  ./a.out # to run the executable file created

      ![Screenshot 2024-07-17 140753](https://github.com/user-attachments/assets/dfdd8025-6569-48b2-949d-9d6cd9c2b63e)
             
2. Compiling C code with RISCV gcc

    step1 : Compile using RISCV gcc compiler as shown below

                   riscv64-unknown-elf-gcc -o1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c

      ![Screenshot 2024-07-17 092749](https://github.com/user-attachments/assets/2a82d4a0-3ba4-4995-b2a1-679dd62aa9ed)

    step2 : To See the assembly code of the C program, run the following command.

                   riscv64-unknown-elf-objdump -d sum1ton.o
                  
      ![Screenshot 2024-07-17 125007](https://github.com/user-attachments/assets/e33886d2-58e8-4b29-9731-262935cf8b24)
