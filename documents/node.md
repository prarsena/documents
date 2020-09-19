## In the node REPL mode (type `node`):
	
	- to clear the console: cmd + k
	
	- to show all available constructors/methods: double tab
	
	- double tap can be done at many points:

	- for example type `os.`, double tab to see all available methods.

	- the underscore variable is a stand-in for the last in-memory in the REPL:

		- >4+4
		- >8
		- >_+4
		- >12

	- To exit: ctrl + d

## General new node/javascript things:

	-   Read from a file require `fs` module : `const input = fs.readFileSync('./file.txt', 'utf-8')

	-   ES6 template string : ` \`Here is my input string: ${input} and it is ${Date.now()}\` `` 
