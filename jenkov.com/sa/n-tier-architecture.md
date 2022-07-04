# N Tier Architecture via jenkov.com

[N Tier Architecture](https://jenkov.com/tutorials/software-architecture/n-tier-architecture.html)

N tier architecture means splitting up the system into N tiers, where N is a number from 1 and up. A 1 tier architecture is the same as a single process architecture. A 2 tier architecture is the same as a client / server architecture etc.

A 3 tier architecture is a very common architecture. A 3 tier architecture is typically split into a presentation or GUI tier, an application logic tier, and a data tier. This diagram illustrates a 3 tier architecture:

![A system with 3 tier architecture.](https://jenkov.com/images/software-architecture/n-tier-architecture-1.png)

The presentation or GUI tier contains the user interface of the application. The presentation tier is "dumb", meaning it does not make any application decisions. It just forwards the user's actions to the application logic tier. If the user needs to enter information, this is done in the presentation tier too.

The application logic tier makes all the application decisions. This is where the "business logic" is located. The application logic knows what is possible, and what is allowed etc. The application logic reads and stores data in the data tier.

The data tier stores the data used in the application. The data tier can typically store data safely, perform transactions, search through large amounts of data quickly etc.

## Web And Mobile Applications

Web applications are a very common example of 3 tier applications. The presentation tier consists of HTML, CSS and JavaScript, the application logic tier runs on a web server in form of Java Servlets, JSP, ASP.NET, PHP, Ruby, Python etc., and the data tier consists of a database of some kind (mysql, postgresql, a noSQL database etc.). Here is a diagram of a typical 3 tier web application:

![A 3 tier web application.](https://jenkov.com/images/software-architecture/n-tier-architecture-2.png)

Actually, it is the same principle with mobile applications that are not standalone applications. A mobile application that connects to a server typically connect to a web server and send and receive data. Here is a diagram of a typical 3 tier mobile application:

![A 3 tier mobile application.](https://jenkov.com/images/software-architecture/n-tier-architecture-3.png) 

## Rich Internet Applications (RIA)

In the first generations of web applications a lot of the HTML, and parts of the CSS and JavaScript was generated by scripts running on the web server. When a browser requests a certain page on the web server, a script was executed on the web server which generated the HTML, CSS and JavaScript for that page.

Today the world is moving to rich internet applications (RIA). RIA also uses a 3 tier architecture, but all the HTML, CSS and JavaScript is generated in the browser. The browser has to download the initial HTML, CSs and JavaScript files once, but after that the RIA client only exchanges data with the web server. No HTML, CSS or JavaScript is sent forth and back (unless that is part of the data, like with an article that contains HTML codes).

RIA applications are explained in more detail in the next text in the software architecture trail.

## Web Application Advantages

The purpose of N tier architecture is to insulate the different layers of the application from each other. The GUI client doesn't know how the server is working internally, and the server doesn't know how the database server works internally etc. They just communicate via standard interfaces.

Web applications especially have another advantage. If you make updates to the GUI client or the application logic running on the server, all clients get the latest updates the next time they access the application. The browser downloads the updated client, and the updated client accesses the updated server.