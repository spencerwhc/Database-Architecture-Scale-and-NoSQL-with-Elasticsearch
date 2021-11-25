# Lecture: To SQL or to NoSQL?

### What is the difference between SQL database and No SQL database?

ACID and the BASE acronyms

- ACID stands for Atomicity, Consistency, Isolation, and Durability.

  these databases go to great extents to ensure that if there is some value at a row-column thing that has a 42, and if everyone is simultaneously looking at that, it says 42 no matter who's looking at it. And that's over time. And if it changes, then all of the viewers of that information, so it's simultaneous writers and simultaneous readers. If everyone is trying to write at it and everyone is trying to read at it at a given moment in time, maybe a millisecond later it's different. But at a given moment time, everyone is seeing the same thing, and that's the consistency. When you make a change, it's isolated from the other changes. One writer might set it to 2 and one moment later set it to 4. That's okay, as long as it was 2 and then it was 4, not like 2, 4, 2 for a little while again, 4 a little while, etc. And that's the isolation that everything you do happens, and then when it's done, it's done and it doesn't seem to move backwards in time.

- BASE stands for Basically, Available, Soft state, Eventual consistency

  eventual consistency means that if there is a value somewhere in this blob of stuff of X in it and somebody sets it to 1 and everyone looks at it and it's a 1 and then somebody sets it to 2, for a while, depending on who's looking at it, it might either be a 1 or a 2, but then eventually it's a 2, okay? So if you wait long enough this system will sort of percolate the change from the 1 to the 2 through everywhere and all of the readers will eventually see the 2. It's not that it's not consistent, it's that eventually it's consistent. It's not guaranteed to be consistent.

**Examples for ACID**

Atomaic consistency, it will block the x=10 until all user have seen x = 20 , then it will change to x=10
![image info](../images/1.png)
![image info](../images/2.png)
![image info](../images/3.png)

**Examples for BASE**

Eventual consistency, all the server will know x=42 at time 0, but when writter write x=10 into database, one of the server will change to x=10 at time 1 but other remains the same, same for x=20, in this moment, some user will see 42 or 10 or 20, eventually, all the server will updated to be x=20 as it has time of 2.
![image info](../images/4.png)
![image info](../images/5.png)
![image info](../images/6.png)
![image info](../images/7.png)
![image info](../images/8.png)
![image info](../images/9.png)

### Database software

![image info](../images/10.png)

### Compromises

![image info](../images/11.png)

- Global Unique Identifier that's a combination of random numbers and the current time that are carefully constructed to be global. And then that becomes kind of your primary key.
- Transactions ensure that on an ACID-based database that you're not getting stale data.
- UNIQUE constraints are difficult. Again, in an ACID database, you could say insert csev on conflict, do nothing, or on conflict, ignore, on conflict, update. So that's when UNIQUE Constraints are triggering. In BASE you got none, because you just don't know. You're talking to one of 10,000 servers and there's no way for them to contact all of the other ones. You have to insert it and then find a way to recover when you turned out to have inserted the same record. There's no uniqueness.
- we sort of give this beautiful query. we hand tune it, we optimize it, we get the index just right and then we get a little tiny bit of data back and it's exactly the data that we want.
- I got 10,000 servers, let's just hit them all and see what happens and then throw away the stuff we don't want. And we'll see sort of applications that use this type of BASE eventual consistency system with a bunch of retrieve and throw away methodology.
