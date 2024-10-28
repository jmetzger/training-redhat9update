# New Feature mtcp (MultiPath TCP)

## What is it ? (under the hood)

  * A set of additional extensions for tcp

## Picture 

![image](https://github.com/user-attachments/assets/67af95d1-4b28-40ae-8529-014785611978)

## How it works:

```
Here’s how it works.
One MPTCP connection manages a set subflows, 
each of them is a TCP socket carrying some synchronization metadata. 
At any given time, the MPTCP connection can use one or more of the available subflows.
```

## Do both sides need MPTCP ?

```
Yes both of them need to have the same to support multi-path. 

If any of them (client or server) does not have then they act as a regular TCP flow. 

Mainly, at the beginning of the connection, the (3-way handshake) both of them 
exchange the information (MP_CAPABLE) that is it possible or not. 

If possible then the socket establishes another flow which is mainly done by Path Manager. 
For more details (https://www.rfc-editor.org/rfc/rfc6824)
```
