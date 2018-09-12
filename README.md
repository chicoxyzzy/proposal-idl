# IDL for ECMAScript

This repository is intended for an investigation into using an Interface Description Language (IDL) in the ECMAScript standard.

## Motivation

### Why expand the standard library?

JavaScript programmers currently use a fairly minimal standard library, and include additional libraries implemented in JavaScript, for example from npm. This creates the following issues:
- **Size**: When starting up an application, all library code has to be loaded. On the web, pages are frequently started and navigated to, so the impact on startup time and bandwidth usage is significant; "serverless" faces related issues of startup time.
- **Quality and stability**: Many developers want a "standard" solution which they can depend on over time to continue to exist and be well-maintained. Having to choose between several competing projects of unknown quality and future maintenance is an additional cost when trying to get a task done.
- **Optimizability**: Built-in libraries can have implementations which tie in more deeply into the JavaScript engine; this gives the potential for better performance in some cases.

### Why do standard library work in TC39?

Standard libraries can be developed in various different standards venues, and that's a good thing that will likely continue. TC39 is a good place to develop some of these libraries for the following reasons:

- **Cross-environment**: TC39's library which works in all JavaScript environments. For example, the same code can work in both web browsers and Node.js. In practice, TC39 standards are often implemented inside of JavaScript engines, which are developed separately from web browsers, enabling greater reach across projects which embed the engine and less duplication of implementation. In developing standards, TC39 attempts to find a solution which works for multiple embedding environments.
- **Integrating feedback from stakeholders**: TC39 meetings and GitHub discussion incorporate a large cross-section of the JavaScript community, including implementers, academics, large websites, tools authors, framework maintainers, library authors, etc. It's not perfect, but we are working on improving inclusion from the community. Taking this feedback into account leads to better library definitions.
- **Coordination among implementations**: TC39 has a good track record in driving coordinated releases of new features across current versions of all major web browsers. This coordination may be motivated by the extensive community discussion which each feature had in its design process, and the highly precise resulting specifications. Developers like this quality for platform predictability. TC39's process can appear to be slow with its large amount of discussion, but the rapidly coordinated implementation can "pay it back".

### Issues with the current approach

TC39 has been gradually been adding to its standard library using "ecmaspeak" notation, defined in the [Algorithm Conventions](https://tc39.github.io/ecma262/#sec-algorithm-conventions) section of the specification. This provides two main components:
- Methods are declared with a heading, which indicates what object they are a property of, what arguments they take (just as a name) and implies the `"length"` property of the function object.
- Arguments and the receiver are coerced with explicit `ToObject`, `ToString`, `ToLength`, `RequireObjectCoercible`, etc calls; options bags are accessed with `Get`; in general, everything about processing and understanding arguments is interspersed with the definition of algorithms in general.

#### Ease of following conventions in new specifications

The free-form nature of argument handling makes it hard to follow conventions reliably. For example, in Intl, [...]

#### Auto-generation of bindings in native implementations

#### "type" definitions for tools

## Requirements

### Casts of arguments

#### Laziness

### Overloading

### Matching JS conventions

## Which language?

### WebIDL

[WebIDL](https://heycam.github.io/webidl/) is a language used by web specifications to declare interfaces and coercions. Some advantages of using WebIDL in ECMAScript are:
- Specifications could be developed in a more uniform way, regardless of venue, enabling more sharing and cross-pollination
- Some of the infrastructure for WebIDL may be reused for JavaScript "for free"
- The additional features of WebIDL to support JavaScript may be useful for other uses of WebIDL; improvements to this standards infrastructure could be broadly beneficial.
- From the perspective of minimizing complexity, 

The idea to use WebIDL in ECMAScript has been received positively by WebIDL's current maintainers. See [the tracking label](https://github.com/heycam/webidl/labels/jsidl) for issues related to supporting JavaScript.

### JSIDL

[Previous attempts](https://github.com/w3ctag/jsidl) to solve this problem involved proposing a new IDL for ECMAScript. Some reasons for going down this path are:
- The feature set needed by JavaScript is different from the Web. They follow different conventions, e.g., enumerability, overloading, the types of conversions, etc. Overlap is only partial.
- In practice, some of the software handling JSIDL
- From the perspective of 

### Let's put off the decision

There are TC39 members who are strong supporters of each the WebIDL and JSIDL paths. The intention of this proposal repository is to start by collecting requirements and drafting what we want the ECMAScript specification to look like, and using the results of that investigation, determine whether we want to pursue using WebIDL with extensions, or use a separate JSIDL.

## Plan from here

In terms of the TC39 Stage Process, the following milestones are planned with respect to the stage process, when *entering* each stage:

1. Entering Stage 1: We agree we want to discuss the topic
    * During Stage 1: Discussion of requirements, work on technical alternatives
2. Entering Stage 2: Agreement on WebIDL vs JSIDL; first draft of IDL itself; IDL conversion drafted for at least one major component of JS
    * During Stage 2: Formalize more of the JS specification as IDL and formalize the IDL definition itself; experiment with automated use of IDL in tools
3. Entering Stage 3: Entire specification is converted to IDL, and IDL definition is fully rigorous; at least one tool is making some use of the IDL
    * During Stage 3: Make further use of IDL in tools, tests and native implementations
4. Entering Stage 4: At least one native implementation uses code generated from the IDL; at least two native implementations implemented any/all normative changes; test262 uses IDL to exhaustively test coercions; PR against the entire specification is prepared
