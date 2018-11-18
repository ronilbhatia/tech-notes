* **Serialization** - refers to the process by which data structures are transformed into a format that can be stored by a computer and recreated later in a potentially different environment. When the object is reconstructed it can be *deserialized* to create an identical clone of the original object.
  * serialization of object-oriented objects does not include any of the methods associated with the object
* A **virtual machine** is an emulation of a computer system. Virtual machines are based on computer architectures, and provide functionality of a physical computer.
  * *host* refers to the physical, 'real-world' hardware running the virtual machine, while the virtual machine being emulated on the real machine is referred to as the *guest*
* **Server** - a computer program that provides a service to another computer program (and its user, i.e. the *client*). Physical machines actually used to run the server are typically referred to as servers, however it's important to note that not all machines running servers are dedicated servers - it can allocate some of its resources to running a server, and others to perform other functions.
  * *Client-Server Model* - Servers are most commonly referred to in this context, in which the *server* program is constantly running and awaiting *requests* from the *client* to which it will provide *responses*.
  * Types of servers
    * *Web Server* - a computer program that serves requested HTML pages or files
      * *Puma*, used in Rails Applications, is a web server.
    * *Application Server* - a computer program that provides the logic to run a business application. Application servers typically (essentially always) contain an in-built web server.
    * *Mail Server* - application that receives incoming e-mail from local users and forwards outgoing e-mail for delivery
    * *File server* - computer responsible for the central storage and management of data files so that other computers on the same network can access them
* **Thread** - short for *thread of execution*. A way for a program to divide itself into two or more simultaneously running tasks. Differ from *processes* in that a thread is contained inside a process, which itself can contain multiple threads sharing the same resources.
