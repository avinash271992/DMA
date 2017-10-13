# DMA
LINk @ http://www.makelinux.net/ldd3/chp-15-sect-4
Understanding of Direct memory access 

DMA is the hardware mechanism that allows peripheral components to transfer their I/O data directly to and from main memory without the need to involve the system processor. Use of this mechanism can greatly increase throughput to and from a device, because a great deal of computational overhead is eliminated.

points
 1. Data transfer can be triggered in two ways: either the software asks for data (via a function such as read) or the hardware asynchronously pushes data to the system.
 2. The hardware writes data to the DMA buffer and raises an interrupt when it's done.
 3. The interrupt handler gets the input data, acknowledges the interrupt, and awakens the process, which is now able to read data.
 4. The second case comes about when DMA is used asynchronously. This happens, for example, with data acquisition devices that go on pushing data even if nobody is reading them. In this case, the driver should maintain a buffer so that a subsequent read call will return all the accumulated data to user space. The steps involved in this kind of transfer are slightly different:

The hardware raises an interrupt to announce that new data has arrived.

The interrupt handler allocates a buffer and tells the hardware where to transfer its data.

The peripheral device writes the data to the buffer and raises another interrupt when it's done.

The handler dispatches the new data, wakes any relevant process, and takes care of housekeeping.




