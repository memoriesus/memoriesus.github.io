---
post: page
title: conditional binding in Swift
tags: [iOS,Swift]
comment: true
---
# Conditional binding
In Swift, if can be followed immediately by a variable declaration and assignment - that is , by let or var and a new local variable name, possibly followed by a colon and a type declaration, then an equal sign and a value as below:
`if let var = val {`
This syntax, called a conditional binding, is actually a shorthand for conditionally upwrapping an optional, the assigned value is expected to be an optional - the compiler will stop you if it's not-- and this is what happens:
* if the Optional is nil, the condition fails and the block is not executed.
* If the optional is not nil, then:
1, The optional is unwrapped.
2, The unwrapped value is assigned to the declared local variable.
3, The block is executed with the local variable in scope.
Thus, a conditional binding is a convenient shorthand for safely passing an unwrapped optional into a block.The Optional is unwrapped, and the block is executed, only if the Optional can be unwrapped.
It is perfectly reasonable for the local variable in a conditional binding to have the same name as an existing variable in the surrounding scope. It can even have the same name as the Optional being unwrapped! There is then no need to make up a new name, and inside the block the unwrapped value of the Optional overshadows the original Optional, which thus cannot be accessed accidentally.
Here’s an example of a conditional binding. where I optionally unwrap a Notification’s userInfo dictionary, attempt to fetch a value from the dictionary using the "progress" key, and proceed only if that value turns out to be an NSNumber that can be cast down to a Double:
`let prog = n.userInfo?["progress"] as? Double if prog != nil {
self.progress = prog! }
`
We can rewrite that code as a conditional binding:
`if let prog = n.userInfo?["progress"] as? Double { self.progress = prog
}
`
It is also possible to nest conditional bindings. To illustrate, I’ll rewrite the previous example to use a separate conditional binding for each Optional in the chain:
`if let ui = n.userInfo {
if let prog = ui["progress"] as? Double {
self.progress = prog }
}
`
The result, if the chain involves many optional unwrappings, can be somewhat verbose and the nest can become deeply indented — Swift programmers like to call this the “pyramid of doom”. To help avoid the indentation, successive conditional bindings can be combined into a condition list, with each condition separated by comma:
`if let ui = n.userInfo, let prog = ui["progress"] as? Double { self.progress = prog
}
`
In that code, the assignment to prog won’t even be attempted if the assignment to ui
fails (because n.userInfo is nil).
Condition lists do not have to consist solely of conditional bindings. They can include ordinary conditions. The important thing is the left-to-right order of evaluation, which allows each condition to depend upon the previous one. Thus it would be possible (though not as elegant) to rewrite the previous example like this:
`if let ui = n.userInfo, let prog = ui["progress"], prog is Double { self.progress = prog as! Double
}
`
Nevertheless, I am not fond of this kind of extended condition list. I actually prefer the pyramid of doom; I find it considerably more legible, because the structure reflects perfectly the successive stages of testing. If I want to avoid the pyramid of doom, I can use a sequence of guard statements :
`guard let ui = n.userInfo else {return}
guard let prog = ui["progress"] as? Double else {return} self.progress = prog
`

