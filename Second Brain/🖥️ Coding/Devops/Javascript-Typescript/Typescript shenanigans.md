

### Extending vs. implementing a pure abstract class in TypeScript

[Ask Question](https://stackoverflow.com/questions/ask)
https://stackoverflow.com/questions/35990538/extending-vs-implementing-a-pure-abstract-class-in-typescript 

```
The **implements** keyword treats the A class as an interface, that means **C has to implement all the methods defined in A**, no matter if they have an implementation or not in **A**. Also there are no calls to super methods in **C**.

**extends** behaves more like what you'd expect from the keyword. You have to implement only the abstract methods, and super calls are available/generated.

I guess that in the case of abstract methods it does not make a difference. But you rarely have a **class** with only abstract methods, if you do it would be much better to just transform it to an **interface**.
```
You can easily see this by looking at the generated code. I made a playground example [here](http://www.typescriptlang.org/Playground#src=abstract%20class%20A%20%7B%0A%20%20%20%20abstract%20m()%3A%20void%3B%0A%09otherM()%20%7B%0A%09%09console.log(%22otherm%22)%3B%0A%09%7D%0A%7D%0A%0Aclass%20B%20extends%20A%20%7B%0A%20%20%20%20m()%3A%20void%20%7B%20%7D%0A%7D%0A%0Aclass%20C%20implements%20A%20%7B%0A%20%20%20%20m()%3A%20void%20%7B%20%7D%0A%7D).