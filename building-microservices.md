Notes taken while studying [Building Microservices](https://www.amazon.com.br/Building-Microservices-English-Sam-Newman-ebook/dp/B09B5L4NVT)

On "Why I Wrote This Book" section
> My own experiences, as
> well as those of my colleagues at ThoughtWorks and elsewhere, reinforced the fact that
> using larger numbers of services with their own independent lifecycles resulted in more
> headaches that had to be dealt with.

# 1. Microservices

## Small, and Focused on Doing One Thing Well

> Microservices are small, autonomous services that work together.

> Codebases grow as we write code to add new features. Over time, it can be difficult to
> know where a change needs to be made because the codebase is so large. Despite a drive
> for clear, modular monolithic codebases, all too often these arbitrary in-process
> boundaries break down. Code related to similar functions starts to become spread all over,
> making fixing bugs or implementations more difficult.

So, even though you can create boundaries within a monolith to ensure code organization,
their compliance only depends on the discipline and good code review practices. These
boundaries are eventually broken, and, once they are broken, they are more likely
to be broken again.

One way people try to organize monoliths is by following the Single Responsibility Principle, which states
"Gather together those things that change for the same reason, and separate those things that change for 
different reasons". This same approach is used when splitting microservices. It makes it so the boundary
between microservices is the business boundary, and it helps to prevent them from growing too much.

Defining how small a microservice should be is difficult, because it depends on things like
the expressiveness of the language and how complex is the business logic. Using lines of code
or number of files is not a good approach.

> Jon Eaves at
> RealEstate.com.au in Australia characterizes a microservice as something that could be
> rewritten in two weeks, a rule of thumb that makes sense for his particular context.
> 
> Another somewhat trite answer I can give is small enough and no smaller. When speaking
> at conferences, I nearly always ask the question who has a system that is too big and that
> you’d like to break down? Nearly everyone raises their hands. We seem to have a very
> good sense of what is too big, and so it could be argued that once a piece of code no
> longer feels too big, it’s probably small enough.
> 
> A strong factor in helping us answer how small? is how well the service aligns to team
> structures. If the codebase is too big to be managed by a small team, looking to break it
> down is very sensible
> 
> the smaller the
> service, the more you maximize the **benefits and DOWNSIDES (!!!)** of microservice architecture

## Autonomous

Each microservice is a separate entity, they should be isolated from each other, and communicate
via network calls.

They should be able to change independently of each other, and be deployed without forcing
other microservices to change.

When designing the API of a service, whe should be wary of what e expose. If we expose too much,
we run into the risk of coupling other services to implementation details of the service itself, 
which are not necessarily integral to the business rule. This can hinder the refactoring process later on.

> Without decoupling, everything breaks down for us. The golden rule: can you make a
> change to a service and deploy it by itself without changing anything else? If the answer is
> no, then many of the advantages we discuss throughout this book will be hard for you to
> achieve.

## Technology Heterogeneity

Having separate services allows us to use different techonologies for each one of them,
which allows us to pick the best tools for each job, instead of a one-size-fits-all solution.
For the same reason, the risk of trying out new techonologies is greatly reduced.

## Resilience

If a whole microservice fails, this crash won't propagate to the other services. They will be
able to continue working, albeit with reduced functionality. This of course depends on how
they communicate with each other.

## Scaling

When scaling a monolith, you have to increase the resources (or number of processes) for the whole monolith.
With microservices, you can scale only the needed services, leaving other services 
that don't stress the system running on lighter specs.

## Ease of Deployment

Deploying a monolith can be risky. This leads to more infrequent deploying, which, ironically, increases the
risk even more, as more changes will be deployed simultaneously. With microservices, we can make more frequent,
smaller deploys, with lower risk. Issues with the deployment of a microservice can be isolated. 
Rollbacks are also easier and faster.

## Organizational Alignment

Instead of having a large team deal with a large codebase, we can have smaller teams deal with smaller
codebases, which tends to be more productive.

## Composability

With a monolith, we usually have only one connection point (usually a single exposed API for a client app).
However, with microservices, we can have multiple connection points, allowing much more flexibility
on how we reuse our services.

## Optimizing for Repleceability

Replacing a legacy monolith is expensive and dangerous. Replacing (or removing) a microservice for a better implementation
is faster and safer.

## What about Service-Oriented Architecture?

> Service-oriented architecture (SOA) is a design approach where multiple services
> collaborate to provide some end set of capabilities. A service here typically means a
> completely separate operating system process. Communication between these services
> occurs via calls across a network rather than method calls within a process boundary.

> you should instead think of
> microservices as a specific approach for SOA in the same way that XP or Scrum are
> specific approaches for Agile software development

## Other decompositional techniques

### Shared Libraries

- You lose true technology heterogeneity
- Cannot scale library code separately from process which uses it 
- Cannot deploy library separately from the entire process (except with dinamically linked libraries)
- Less system resiliency
- Can be a good option for common tasks which aren't specific to the business domain

### Modules (like erlang processes)

- They have some advantages over shared libraries, however
- We also lose some technology heterogeneity (the author didn't say this, but I think you could just transform a module into
  an adapter which communicates with a microservice written to substitute the module)
- Limited in how we can scale independently (not sure if this applies to erlang though)
- Can drift toward integration techniques that are overly coupling (this I agree with)
- Lack seams for architectural safety measures (I'm also not sure about this, Erlang is very good with fault tolerance)

> Technically, it should be possible to create
> well-factored, independent modules within a single monolithic process. And yet we rarely
> see this happen. The modules themselves soon become tightly coupled with the rest of the
> code, surrendering one of their key benefits. Having a process boundary separation does
> enforce clean hygiene in this respect (or at least makes it harder to do the wrong thing!). I
> wouldn’t suggest that this should be the main driver for process separation, of course, but
> it is interesting that the promises of modular separation within process boundaries rarely
> deliver in the real world.

## No silver bullet

> microservices are no free lunch or silver bullet, and
> make for a bad choice as a golden hammer. They have all the associated complexities of
> distributed systems, and while we have learned a lot about how to manage distributed
> systems well, it is still hard

# 2. The Evolutionary Architect


