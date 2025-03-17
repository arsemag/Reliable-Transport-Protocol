# Reliable-Transport-Protocol



# Class Definitions

## ****** Sender *******
log(self, message): 
Allows us to directly write to standard error to have well communicated code. 

send(self, message):
It properly formats the packet to send to receiver while starting the time so we can keep track of the RTT of the packet.

recv(self, sock):
Receives the data then sets the host and ports while notifying if the sender has received a message or not from the receiver. 

handle_socket_input(self):
Processes incoming ACKs, updates RTT estimates using an exponentially weighted moving 
average, manages the transmission window, and handles timeouts to ensure reliable data transfer.

handle_stdin_input(self, seq):
Reads data from standard input and sends packets for the current window. If there are missing packets from a previous 
window, re-send those first.

process_window_acks(self):
Checks the current window for missing ACKs. If some packets in the window were not acknowledged (or a timeout occurred), 
mark them for retransmission and decrease the window size. Otherwise, slide the window and increase the window size by 1

run(self):
The run method manages the main event loop, handling input from both the socket and standard input, processing ACKs, 
managing timeouts, and terminating when all data has been transmitted and acknowledged.

## ****** Receiver ******

Methods:

log(self, message):
Allows us to directly write to standard error to have well communicated code. 

send(self, message)
Sends a JSON-encoded message to the remote host and port, if set, and logs the 
sent message for debugging.

recv(self)
Receives a message from the socket, sets the remote host and port if it's the first message, and logs the 
received message. If the message is from an unexpected source, it ignores it.

handle_new_packet(self, msg): 
Processes an incoming message by sending an ACK, handling new messages, and processing.

*** Helper *** 
jitter(self, msg)
Handles incoming packets in order, prints data if it matches the expected sequence, stores out-of-order 
packets for future processing, and processes stored packets once the correct sequence is reached.

run(self)
Continuously listens for incoming data using select, processes received messages, and 
handles data transmission and ordering.


TESTING

Throughout the development process, we used print statements and broke down the code into smaller 
sections to pinpoint where things were going wrong. We would test different scenarios, remove certain conditions, 
and change the code to make sure everything worked as expected. This helped me catch and fix issues step by step, 
making sure the final solution accurate. 




