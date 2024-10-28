# New Feature mtcp (MultiPath TCP)

## How it works:

```
Here’s how it works.
One MPTCP connection manages a set subflows, 
each of them is a TCP socket carrying some synchronization metadata. 
At any given time, the MPTCP connection can use one or more of the available subflows.
```

