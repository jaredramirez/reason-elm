## Reason-Elm
> Bindings for mounting and interacting with Elm applications in Reason.

### Motivation
Writing web applications in Elm is nice. It's type system and enforced architecture
are just a couple of the really cool things that it offers. The Elm ecosystem is
pretty small compared to the Javascript(JS) ecosystem, and this is a draw back
when coming from the world of JS. Interop with JS is possible, but it requires
writing regular JS code, which has none of Elm's safety. This is where Reason
enters the picture. Reason can communicate more direclty with JS with much more
type safety than vanilla JS. The possibility of writing an Elm app and handling
JS interop with Reason is pretty powerful. Having access to the entire JS
ecosytem in a (more) typesafe way is pretty exciting, so Reason-Elm was created.

### Getting Started
* Install
  * With yarn: `yarn add reason-elm`
  * With npm: `npm install --save reason-elm`
* Add `reason-elm` as a dependency in `bsconfig.json`
```
{
  ...
  "bs-dependencies": ["reason-elm"]
}
```

* Use `ReasonElm` (To import Elm directly in Reason take a look at [this webpack config](https://github.com/jaredramirez/reason-elm-example/blob/master/webpack.config.js)):
```
module R = Js.Result;

[@bs.module]
external elmProgram : ReasonElm.elmProgram = "path/to/elm/Main.elm";

let instance =
  ReasonElm.mount(
    ~flags={"foo": "bar"},
    ~moduleName="Main.Nested", /* 'moduleName' defaults to "Main" */
    elmProgram /* Must be last arguement! */
  );

switch instance {
| R.Ok(i) => Js.log("Elm is running.")
| R.Error(errorMessage) => Js.log(errorMessage)
};
```

Checkout [this example](https://github.com/jaredramirez/reason-elm-example)!

### Docs
* [`elmProgramBase : type`](DOCS.md#elmProgramBase)
* [`elmProgram : type`](DOCS.md#elmProgram)
* [`elmProgramWithPorts : type`](DOCS.md#elmProgramWithPorts)
* [`elmInPort : type`](DOCS.md#elmInPort)
* [`elmOutPort : type`](DOCS.md#elmOutPort)
* [`elmInstance : type`](DOCS.md#elmInstance)
* [`elmInstanceWithPorts : type`](DOCS.md#elmInstanceWithPorts)
* [`mount : func`](DOCS.md#mount)

### Roadmap
* Convert `Js.t` objects to OCaml records
  * Currently the Elm 'instance & 'ports are `Js.t` objects

If you have any suggestions or run into any bugs, please open an issue!
