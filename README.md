# 64 bit nasm code examples


#### MACOSx

1. On OS X, the symbols are prefixed <b>with an underscore</b>.
  call printf must be _printf and so on..   read more about nasm "--prefix _"
  
  The OS-provided symbols are going to stay stuck with a leading _, but your functions can be controlled with "-fleading-underscore".
  
  global main <- "main" is entry point by default, like in C/C++ "main()", but it can be configured:
  
  ld <b>-e mystart</b> -macosx_version_min 10.13.0 -static -o hello hello.o 
  
2. Assembling the Source File 

$  nasm -fmacho64 Hello.asm --prefix _ 

output Hello.o

3. Creating the Executable

$  ld -macosx_version_min 10.14.0 -lSystem Hello.o -o hello

output hello  <=  this is executable., so run ./hello

all together:
### $ nasm -fmacho64 Hello.asm --prefix _ && ld -macosx_version_min 10.14.0 -lSystem Hello.o -o hello && ./hello


or add alias to .bash_profile
and assemple with 

$ nal "Hello.asm"

````
alias nal='function nal_() { 
if [ ! -n "$1" ]; then
  echo "ASM file not specified, exit."
  return 0
fi

asm_file=$1
fname=`basename $asm_file`
binary=`echo $fname | rev | cut -f 2- -d '.' | rev`
nasm_o=${binary}.o

nasm -fmacho64 "${asm_file}" --prefix _ -o "${nasm_o}" && ld -macosx_version_min 10.14.0 -lSystem "${nasm_o}" -o "${binary}"

} ;nal_'
````

also read about this params:
-demangle -dynamic -arch x86_64 

#### NASM
https://nasm.us/doc/nasmdoc0.html

#### NASM tutorial +OSX sample
https://cs.lmu.edu/~ray/notes/nasmtutorial/

#### Tutorials x32
https://asmtutor.com


