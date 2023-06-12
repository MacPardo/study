# Building Microservices

On "Why I Wrote This Book" section
> My own experiences, as
> well as those of my colleagues at ThoughtWorks and elsewhere, reinforced the fact that
> using larger numbers of services with their own independent lifecycles resulted in more
> headaches that had to be dealt with.

## 1. Microservices

### Small, and Focused on Doing One Thing Well

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

