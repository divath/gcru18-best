# Code organization in Go projects

---

## Presentation

- based on Ashley McNamara & Brian Ketelsen "Go best practices" 
- youtube https://www.youtube.com/watch?v=MzTcsI6tn-0
- original slides https://talks.bjk.fyi/bketelsen/gcru18-best#/
- domain driven design https://github.com/marcusolsson/goddd

---

## Packages

---

#### Code Organization

There are two key areas of code organization in Go that will make a huge impact on the usability, testability, and functionality of your code:

---

#### Code Organization

- Package Naming
- Package Organization

---

#### Code Organization

We can't talk about them separately because one influences the other.

---

#### Package Organization - Libraries

- Packages contain code that has a single purpose

```
	archive	cmd	crypto	errors	go	index	math	path	sort	syscall	unicode bufio	compress  database  expvar	hash	internal  mime      reflect	strconv	testing	unsafe builtin	container debug	flag  
```

---

#### Package Organization - Libraries

When a group of packages provides a common set of functionalities with different implementations, they're organized under a parent.  Look at the contents of package *encoding*:

```
	ascii85     base32      binary      encoding.go hex         pem
	asn1        base64      csv         gob         json        xml
```

---

#### Package Organization - Libraries

Some commonalities:

- Packages names describe their purpose
- It's very easy to see what a package does by looking at the name
- Names are generally short
- When necessary, use a descriptive parent package and several children implementing the functionality -- like the *encoding* package

---

#### Package Organization - Applications

The packages we've seen are all libraries.  They're intended to be imported and used by some executable program like a service or command line tool.

What should the organization of your executable applications look like?

---

#### Package Organization - Applications

When you have an application, the package organization is subtly different.  The difference is the command, the executable that ties all of those packages together.

---

#### Package Organization - Applications

Application package organization has a huge impact on the testability and functionality of your system.

---

#### Package Organization - Applications

When writing an application your goal should be to write code that is easy to understand, easy to refactor, and easy for someone else to maintain.

---

#### Package Organization - Applications

Most libraries focus on providing a singularly scoped function; logging, encoding, network access, database storage.

Your application will tie all of those libraries together to create a tool or service.  That tool or service will be much larger in scope.  

---

#### Package Organization - Applications

When you're building an application, you should organize your code into packages, but those packages should be centered on two categories:

- Domain Types
- Services

---

#### Package Organization - Applications

*Domain Types* are types that model your business functionality and objects. 

*Services* are packages that operate on or with the domain types.

---

#### Package Organization - Applications

A domain type is the substance of your application.  If you have an inventory application, your domain types might include *Product* and *Supplier*.  If you have an HR administration system, your domain types might include *Employee*, *Department*, and *Business Unit*.

---

#### Package Organization - Applications

The package containing your domain types should also define the interfaces between your domain types and the rest of the world.  These interfaces define the things you want to do with your domain types.

- *EmailDispatcher*
- *ConnectionProvider*
- *Authenticator*
- *LeaseManager*
- *EmployeeStorage*

---

#### Package Organization - Applications

Your domain type package should be the root of your Go packages directory.  This makes it clear to anyone opening the codebase what is project about, what types are being used, and what operations will be performed on those types.

---

#### Package Organization - Applications

The *domain* package, or *root* package of your application should not have any external dependencies.  
> It exists for the sole purpose of describing your types and their behaviors.

---

#### Package Organization - Applications

The implementations of your domain interfaces should be in separate packages, organized by dependency.

---

#### Package Organization - Applications

Dependencies include:

- Data sources & data access (postgres, vertica, awss3, cache, mocks, fakedb)
- API (grpc, rest, routes, conversion, apiv2)
- Client commands (cli, cmd, main)
- Metrics & Logging (metrics, logging, params)
- Testing & Data generation (generator)

You should have one package per dependency.

---

#### Package Organization - Applications

Why one package per dependency?

- Simple testing
- Easy substitution/replacement/refactoring
- Consistency
- No circular dependencies
- Easier to navigate

---

## Example

Card transaction processing 

(whiteboard)

---

### Questions?

---?image=assets/image/gitpitch-audience.jpg&opacity=100

@title[Thank You!]

## Thank You
