1.     
Operation,Array State S[1..6],S.top  
Initial,[_, _, _, _, _, _],0,empty  
PUSH(S, 4),[4, _, _, _, _, _],1,4 is at the bottom  
PUSH(S, 1),[4, 1, _, _, _, _],2  
PUSH(S, 3),[4, 1, 3, _, _, _],3,3 is at the top  
POP(S),"[4, 1, (3), _, _, _]",2,Returns 3  
"PUSH(S, 8)","[4, 1, 8, _, _, _]",3,8 overwrites 3  
POP(S),"[4, 1, (8), _, _, _]",2,Returns 8  
2.    
Operation,Array State Q[1..6],Head,Tail   
Initial,[_, _, _, _, _, _],1,1,empty  
ENQUEUE(Q, 4),[4, _, _, _, _, _],1,2  
ENQUEUE(Q, 1),[4, 1, _, _, _, _],1,3  
ENQUEUE(Q, 3),[4, 1, 3, _, _, _],1,4  
DEQUEUE(Q),[(4), 1, 3, _, _, _],2,4,Returns 4  
ENQUEUE(Q, 8),[_, 1, 3, 8, _, _],2,5  
DEQUEUE(Q),[_, (1), 3, 8, _, _],3,5,Returns 1  
3.   
Underflow occurs when trying to remove an element from a queue that has  nothing in it.    
A queue is empty when Head equals Tail. If Head == Tail, there is no data   between them to process.    
Overflow occurs when trying to add an element to a queue that has no available slots.  
A queue is full when (Tail + 1) equals Head. If moving the Tail forward by one position, Tail hitting the Head.
4.  
// Adds to the front (decrements head)
PUSH-FRONT(D, x)
    if D.head == 1
        D.head = D.length
    else
        D.head = D.head - 1
    if D.head == D.tail
        error "overflow"
    D[D.head] = x

// Adds to the back (standard enqueue)
PUSH-BACK(D, x)
    if (D.tail == D.length and D.head == 1) or (D.tail + 1 == D.head)
        error "overflow"
    D[D.tail] = x
    if D.tail == D.length
        D.tail = 1
    else
        D.tail = D.tail + 1

// Removes from the front (standard dequeue)
POP-FRONT(D)
    if D.head == D.tail
        error "underflow"
    x = D[D.head]
    if D.head == D.length
        D.head = 1
    else
        D.head = D.head + 1
    return x

// Removes from the back (decrements tail)
POP-BACK(D)
    if D.head == D.tail
        error "underflow"
    if D.tail == 1
        D.tail = D.length
    else
        D.tail = D.tail - 1
    return D[D.tail]