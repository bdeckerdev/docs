# jBASE Sockets

<PageHeader />

jBASE offers some internal functions to gain access to Sockets.  jBASE socket functions are built in C based functions and can be accessed by using DEFC and importing the functions.

- DEFC VAR SOCKOPEN(handle, ip, port, timeout, setting)
- DEFC VAR SOCKCLOSE(handle, setting)
- DEFC VAR SOCKSEND(client\_handle, data\_to\_send, setting)
- DEFC VAR SOCKRECV(client\_handle, recieve\_message, setting)
- DEFC VAR SOCKSERV(port, server\_handle, conDetails)
- DEFC VAR SOCKACCEPT(server\_handle, client\_handle\_number, setting)
- DEFC VAR SOCKBIND(server\_handle, client\_handle\_number, client\_handle, setting)
- DEFC VAR GETSOCKBASE(server\_handle)
- DEFC VAR GETSERVERHANDLE(server\_handle, ctx)

Here is a github project with a good example on how to create both a socket client and server.

[https://github.com/zumasys/jbase\_sockets](https://github.com/zumasys/jbase_sockets)

Usage Example Opening a network cash drawer:
(Courtesy of Brent Blair) 

    INCLUDE JBC_SOCKS.h
    timeout = 10
    hostIPAddress='192.168.1.1'
    hostPort='12345'
    setting = ""
    debug=0
    handle = ""
    errorMessage = ""
    status = SOCKOPEN(handle, hostIPAddress, hostPort, timeout, setting)
    SOCKSEND(handle, 'opendrawer', errorMessage)
    setting = ""
    receiveMessage = ""
    size = SOCKRECV(handle, receiveMessage, setting)
    IF size # LEN(receiveMessage) THEN
      CRT 'No message returned from drawer'
    END ELSE
      CHANGE CHAR(10) TO @FM IN receiveMessage
      CHANGE CHAR(13) TO "" IN receiveMessage
      recievedLines = DCOUNT(receiveMessage, @FM)
      FOR recievedCounter = 1 TO recievedLines
        CRT "Drawer ", receiveMessage<recievedCounter> "MCP"
      NEXT recievedCounter
    END
    SOCKCLOSE(handle, setting)
    STOP

Response:
Drawer OPEN

[Back to Coding Corner](./../README.md)

<PageFooter />
