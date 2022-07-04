# RIA Architecture via jenkov.com

[RIA Architecture](https://jenkov.com/tutorials/software-architecture/ria-architecture.html)

RIA (Rich Internet Applications) are a special breed of web applications where the user interface has much richer functionality than what the first and second generation web applications. They look and feel more like desktop applications. RIA user interfaces are typically developed using HTML5 + JavaScript + CSS3, Flex (Flash), JavaFX, GWT, Dart or some other RIA tool. In the long run, variations of HTML5 + JavaScript + CSS3 seems to be the winner (GWT and Dart can be compiled to JavaScript).

The richer GUI client of RIA user interfaces also results in a somewhat different internal architecture and design of the web applications. RIA user interfaces and their backends are typically more cleanly separated than for first and second generation web applications. This makes the RIA GUI more independent of the server side, and also makes it easier for GUI and server developers to work in parallel. I will explain how in this text, but first I have to explain how the typical internal design looked in first and second generation web applications.

## First Generation Web Applications

First generation web applications were page oriented. You would include all GUI logic and application logic inside the same web page. The web page would be a script which was executed by the web server, when requested by the browser. GUI logic and application logic were mixed up inside the same page script. Here is an illustration of this architecture and design:

![First generation web application architecture and design.](https://jenkov.com/images/software-architecture/ria-architecture-1.png)

Being page oriented, every action the application allowed was typically embedded in its own web page script. Each script was like a separate transaction which executed the application logic, and generated the GUI to be sent back to the browser after the application logic was executed. Here is an illustration of the paged nature of first generation web applications:

![The paged nature of first generation web applications.](https://jenkov.com/images/software-architecture/ria-architecture-2.png)

The GUI was pretty dumb. The browser showed a page. When the user clicked something in the page, the browser was typically redirected to a new page (script).

First generation web page technologies include Servlets (Java), JSP (JavaServer Pages), ASP, PHP and CGI scripts in Perl etc.

Anyone who has worked with first generation web application knows that this design was a mess. GUI logic and application logic was interleaved, making it hard to locate either one when you needed to make changes to either the GUI or application logic. Code reuse was low, because the code was spread over a large amount of web page scripts. GUI state (like pressed down buttons) which had to be maintained across multiple pages, had to be kept either in the session data on the server, or be sent along to each page and back to the browser again. If you wanted to change the programming language of the web page scripts (like from PHP to JavaServer Pages (JSP) ), that would often require a complete rewrite of the web application. It was a nightmare.

## Second Generation Web Applications

In second generation web applications developers found ways to separate the GUI logic from the application logic on the server. Web applications also became more object oriented than they had been when the code was spread over multiple pages. Often, web page scripts were used for the GUI logic, and real classes and objects were used for the application logic. Here is a diagram illustrating the design of second generation web applications:

![Second generation web applications.](https://jenkov.com/images/software-architecture/ria-architecture-3.png)

Frameworks were developed to help make second generation web applications easier to develop. Examples of such frameworks are ASP.NET (.NET), Struts + Struts 2 (Java), Spring MVC (Java), JSF (JavaServer Faces), Wicket (Java) Tapestry (Java) and many others. In the Java community two types of framework designs emerged. Model 2 and component based frameworks. I will not go to deep into the difference here, because in my opinion both designs are obsolete.

Second generation web applications were easier to develop than first generation web applications, but they still had some problems. Despite the better separation of GUI and application logic, the two domains still often got intertwined in each other. Also, since the GUI logic was written in the same language as the application logic, changing the programming language meant rewriting the whole application again. Additionally, due to the limits of second generation web application technologies, the GUIs developed were often more primitive than what people were used to from desktop applications. So, even if second generation web application technologies were a step forward, they were still a pain to work with.

### RIA Web Applications

RIA (Rich Internet Applications) web applications are the third generation of web applications. RIA web applications were first and foremost known for having a user interface that looked much closer to desktop applications.

To achieve these more advanced user interfaces, RIA technologies are typically executed in the browser using either JavaScript, Flash, JavaFX or Silverlight (both Flash and Silverlight are on their way out to my knowledge, but I could be wrong). Here is a diagram illustrating RIA web application architecture and design:

![RIA web application architecture and design.](https://jenkov.com/images/software-architecture/ria-architecture-4.png)

As you can see, the GUI logic is now moved from the web server to the browser. This complete split from the server logic has some positive and negative consequences for the design and architecture of the application.

First of all, the GUIs can become much more advanced with RIA technologies. That by itself is an advantage.

Second, because the GUI logic is executed in the browser, the CPU time needed to generate the GUI is lifted off the server, freeing up more CPU cycles for executing application logic.

Third, GUI state can be kept in the browser, thus further cleaning up the server side of RIA web applications.

Fourth, since the GUI logic completely separated from the application logic, it becomes easier to develop reusable GUI components, which can be reused no matter what server side programming language is used for the application logic.

Fifth, RIA technologies typically communicate with the web server by exchanging data, not GUI code (HTML, CSS and JavaScript). The data exchange is typically XML sent via HTTP, or JSON sent via HTTP. This changes the server side from being "pages" to being "services" that perform some part of the application logic (create user, login, store task etc.). When your server side becomes complete free from generating GUI, your application logic becomes very clear. Your application logic gets some data in, and sends some data out, and doesn't have to think about anything else. No GUI state, no GUI generation etc. This is a really big advantage during development. Yes, your application logic still has to generate either XML or JSON from data, but that is much, much easier than generating GUI, and much much closer to the application logic and data model.

Sixth, since the GUI and application logic on the server typically communiate via HTTP + JSON, or HTTP + XML, the GUI is 100% independent of what programming language that is used on the server. The GUI logic's interface to the server is just HTTP calls. This means that you can change the programming language and tools on the client independently of the server, as well as change the server tools without influencing the client.

Seventh, since GUI logic and application logic are completely separated, and the only interface between them is HTTP + JSON / XML, the GUI and application logic can also be developed independently of each other. The application logic developer can implement the services and test them independently of the GUI. And the GUI logic developer can just create a fake (mock) service which returns the data he needs to develop his GUI needs, so he can develop and test his GUI. Once the real service is ready, the mock service can be swapped for the real service without too much work.

Eighth, because the back end just consists of services that send and receive data, it is much easier add a different type of client in the future, if needed. For instance, you might want to add a native mobile iOS or Android application client, which also interacts with your back end services.

Ninth, since the back end now consist of simple services receiving and sending data, your web application is naturally prepared for the "open application" trend, where web applications can be accessed both via a GUI and via an API (in case your users need to write a program to interact with your web application).

Tenth, since the GUI and back end services only exchange data, the traffic load is often smaller than if the back end had to send both the data and HTML, CSS and JavaScript. Thus your bandwidth requirements may go down (but sometimes you end up sending more small requests than you would otherwise, so it may cancel each other out).

As you can see, what on the surface seems like a small change in how we develop web applications actually have quite a lot of beneficial side effects. Once you experience these advantages in a real project, you will never want to go back to second generation web applications again.

Here is a somewhat more detailed diagram of RIA architecture, so you can see all the separations of responsibility (and thus theoretically verify the advantages I have mentioned above):

![RIA web application architecture and design in more detail.](https://jenkov.com/images/software-architecture/ria-architecture-5.png)

Of course there are some negative consequences of RIA technology too. The complete split of GUI logic from application logic sometimes means that the GUI logic is implemented using a different programming language than the application logic. Your GUI logic might be implemented in JavaScript, ActionScript (Flash) or Dart, and the application logic in Java, C# or PHP. Java developers can use Google Web Toolkit (GWT) to program JavaScript GUIs using Java. The new RIA technologies means that the developer team must master more technologies. This is of course a disadvantage. But I think you can live with that, given all the advantages RIA web applications have.

## RIA Technologies

Here is a list of a few well-known RIA technologies:

- HTML5 + CSS3 + JavaScript + JavaScript frameworks
    - jQuery
    - jQuery Mobile
    - AngularJS
    - Sencha EXT-JS
    - SmartClient
    - D3
    - Dart
- GWT (Google Web Toolkit)
- JavaFX
- Flex (Flash)
- Silverlight (now unsupported)

My perception is that the world is moving towards HTML5 + CSS3 + JavaScript RIA solutions, rather than Flex and JavaFX. Microsoft has already shut down development of their Silverlight, and I suspect that JavaFX and perhaps even Flex will go the same way in the future. But that is just speculation.
