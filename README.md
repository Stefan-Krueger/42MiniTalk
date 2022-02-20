# 42MiniTalk
Project Minitalk at 42 School

## Challenge:   

Two processes can communicate via the operating system using commands. There are a number of fixed commands and two so-called "user commands": "SIGUSR1" and "SIGUSR2".    

Over these two "lines" no data, but only "signals" can be exchanged, similarly as with power lines: on and off, 1/0, thus binary.   

So the data you want to transport must first be transferred to a binary format and then sent over the line bit by bit.   

Most students use the two "lines" for the two states "0" and "1", e.g. SIGUSR1 = 0 and SIGUSR2 = 1. This creates something like a Morse protocol, but this has no flow safety and error correction by design.   

The operating system provides functions for the communication between processes, these are addressed over signal.h. Thereby there is the following convention:   

"signal" waits for messages on certain channels (e.g. SIGUSR1 / SIGUSR2), which are then evaluated bit by bit via the parameter "action".     

"kill" sends a binary signal to a process named in the "pid" parameter over a line named "SIGUSR1" or "SIGUSR2".   

## Bonus:  

For the bonus part, the server should acknowledge the data, i.e. send something like an acknowledgment. Also, Unicode data should be transferable.    

## Execution of the programs:   

Two files are created, "server" and "client", which are started in different terminal windows. First one starts the "server", which writes its own process ID (PID) into the command line and waits from now on in continuous loop for signals, which it writes then likewise into the command line. After each received text the server also writes a newline.   

The client is started with two parameters, the PID of the server and the attached message, the so-called "payload". Messages that contain a space must be enclosed in quotes. In the simplest case, after sending the message, the client finishes its flow and is terminated.   

For a bonus version of the program, the client should compare the number of characters sent with the number of characters received from the server. This way you can see if any data has been lost.   

## Implementation:   

### Client  

3 functions "action", "mt_kill" and "main".  

#### action:  

Evaluate acknowledgements on the lines SIGUSR1 and SIGUSR2. SIGUSR1 is used to count the transmitted characters and SIGUSR2 is used as a terminating signal (like Enter).  

#### mt_kill:  

Sending the payload, i.e. transmitting a word, a longer string (in " "), or a text file (with cat).  

Send a NULL (8 bit 0) as completion of the transmission   

#### main  

Reading the commandline with PID and "Payload". As PID the number is taken, which the server program outputs after the start.  

Receiving acknowledgements on the lines SIGUSR1 and SIGUSR2, calling "action  

Sending the "Payload" with mt_kill, arguments PID and Message  

### Server  

2 functions "action" and "main"  

#### action:   

Get the PID of the client so that the acknowledgment can be transmitted back (client_pid = info->si_pid).  

Bitwise OR compaired to SIGUSR2  

If the read character is "0", then acknowledgement via SIGUSR2 to client and reset client_PID  

Otherwise printout of the recognized character into the command line and confirmation via SIGUSR1 to client   

Shift to next bit to the left (Leftshift)  

#### main:   

Printout of the server PID  

Sending of acknowledgements via "action  

Receive payload on SIGUSR1 and SIGUSR2  
