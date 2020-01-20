# hello_world
For printing hello_world

some new changes

# A1Q1
# Tianyi Zhou


	.data
space: .asciiz "\n"

note1: .asciiz "The value of 'a' is: "
note2: .asciiz "The value of 'b' is: "
note3: .asciiz "The value of 'a+b' is: \n"
note4: .asciiz "The value of 'a-b' is: \n"
note5: .asciiz "The value of 'a*b' is: \n"
note6: .asciiz "The value of 'a/b' is: \n"
note7: .asciiz "Sum of a, b are between 10 and 20"
note8: .asciiz "Sum of a, b are not between 10 and 20"

	.macro print_number
li $v0, 1
syscall
li $v0, 4
la $a0, space
syscall
	.end_macro
	
	.macro no_case
li $v0, 4
la $a0, note8
syscall
	.end_macro
		
.text
main:
	li $v0, 4
	la $a0, note1
	syscall
	li $v0, 5
	syscall
	move $a1, $v0
	
	li $v0, 4
	la $a0, note2
	syscall
	li $v0, 5
	syscall
	move $a2, $v0
	
	li $v0, 4
	la $a0, note3
	syscall
	add $t3, $a1, $a2
	move $a0, $t3
	print_number
	
	li $v0, 4
	la $a0, note4
	syscall
	sub $t4, $a1, $a2
	move $a0, $t4
	print_number
	
	li $v0, 4
	la $a0, note5
	syscall
	mul $t5, $a1, $a2
	move $a0, $t5
	print_number
	
	bne $a2, 0, division
	add $t3, $a1, $a2
	bge $t3, 10, case2
	no_case

case2: 
	ble $t3, 20, success
	no_case

success:
	li $v0, 4
	la $a0, note8
	syscall
	
division:
	li $v0, 4
	la $a0, note6
	syscall
#	mtc1 $a1, $f1
#	mtc1 $a2, $f2
#	div.s $f12, $f1, $f2
#	li $v0, 2
#	syscall
	
	mtc1 $a1, $f1
	mtc1 $a2, $f2
	div.s $f12, $f1, $f2
	li $v0, 2
	syscall
