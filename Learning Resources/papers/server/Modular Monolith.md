> [!PDF|] [[3593856.3595909.pdf#page=1&selection=22,32,30,26|3593856.3595909, p.1]]
> > Our prototype implementation reduces application latency by up to 15× and reduces cost by up to 9× compared to the status quo

Contradiction with Micro service:
1. Its hurts performance
> > It hurts performance
> > It hurts correctness
> > It is hard to manage
> >  It freezes APIs.
> > It slows down application development.


> [!PDF|] [[3593856.3595909.pdf#page=2&selection=91,0,106,48|3593856.3595909, p.2]]
> > Write monolithic applications that are modularized into logically distinct components. (2) Leverage a runtime to dynamically and automatically assign logical components to physical processes based on execution characteristics. (3) Deploy applications atomically, preventing different versions of an application from interacting.

> [!PDF|255, 208, 0] [[3593856.3595909.pdf#page=2&annotation=519R|3593856.3595909, p.2]]
> > The two main parts of our proposal are (1) a programming model with abstractions that allow developers to write singlebinary modular applications focused solely on business logic, and (2) a runtime for building, deploying, and optimizing these applications
> 

> [!PDF|yellow] [[3593856.3595909.pdf#page=2&selection=131,1,139,47&color=yellow|3593856.3595909, p.2]]
> > The programming model enables a developer to write a distributed application as a single program, where the code is split into modular units called components (Section 3). This is similar to splitting an application into microservices, except that microservices conflate logical and physical boundaries. Our solution instead decouples the two: components are centered around logical boundaries based on application business logic, and the runtime is centered around physical boundaries based on application performance

> [!PDF|yellow] [[3593856.3595909.pdf#page=2&selection=118,0,175,63&color=yellow|3593856.3595909, p.2]]
> > The two main parts of our proposal are (1) a programming model with abstractions that allow developers to write singlebinary modular applications focused solely on business logic, and (2) a runtime for building, deploying, and optimizing these applications. The programming model enables a developer to write a distributed application as a single program, where the code is split into modular units called components (Section 3). This is similar to splitting an application into microservices, except that microservices conflate logical and physical boundaries. Our solution instead decouples the two: components are centered around logical boundaries based on application business logic, and the runtime is centered around physical boundaries based on application performance (e.g., two components should be co-located to improve performance). This decoupling—along with the fact that boundaries can be changed atomically—addresses C4. By delegating all execution responsibilities to the runtime, our solution is able to provide the same benefits as microservices but with much higher performance and reduced costs (addresses C1). For example, the runtime makes decisions on how to run, place, replicate, and scale components (Section 4). Because applications are deployed atomically, the runtime has a bird’s eye view into the application’s execution, enabling further optimizations. For example, the runtime can use custom serialization and transport protocols that leverage the fact that all participants execute at the same version. Writing an application as a single binary and deploying it atomically also makes it easier to reason about its correctness (addresses C2) and makes the application easier to manage (addresses C3). Our proposal provides developers with a programming model that lets them focus on application business logic, delegating deployment complexities to a runtime (addresses C5). Finally, our proposal enables future innovations like automated testing of distributed applications (Section 5).
> 
> 