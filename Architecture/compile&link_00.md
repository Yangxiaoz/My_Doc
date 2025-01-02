# Compile of The minimun code in linux

*a demo now*

1. precompile

```bash
gcc -E main.c -o main.i
```

2. compile

```bash
gcc -S main.i -o main.s
```

3. assembly

```bash
gcc -c main.s -o main.o
```

4. link

```bash
gcc main.o -o a
```

5. disassembly

```bash
objdum -d a > disassembly.txt
```