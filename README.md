# CS 352 — Compiler Testcases

This test harness works slightly differently than the one provided by the TA.

## Features

* Lists passed and failed tests
* Shows program output on failure
* Utilizes `make debug` to allow you to output debugging information to more easily resolve errors when testcases fail
  * If you don't have a `debug` task in your Makefile, the harness will simply run `make`
  * You can still test against the graded `make` build if you have a `debug` task by running `./test_all release`
* Really easy to drop in new tests
* Tests can have descriptive names
* Very flexible setup to easily add new kinds of tests (output must match a regex, etc)
* Colorized output!
* Runs from any directory! (no need to `cd` to the tests directory)
* Chainable! If any tests fail, `test_all` exists with `1`

## Recommended setup

1. Clone this repo to the tests directory in your project folder

	```	
	git clone https://github.com/alecgorge/cs352-tests.git tests
	```
	
2. Create a `debug` task in your `Makefile`. *Do not* put this task first in your Makefile or that will be the task that is run by the TAs when they grade by running `make`:

	```
	debug:y.tab.c lex.yy.c
		gcc -DDEBUG=1 y.tab.c lex.yy.c -o parser -lfl

	```
3. Modify your lexer utilize a macro to only output information when `DEBUG` is defined. I like print out the token names and values of ID's and strings. Here is a sample macro with a bad name:

	```
	#ifdef DEBUG
	#	define only_output_in_debug_mode(...) 		printf(__VA_ARGS__)
	#else
	#	define only_output_in_debug_mode(...) 		do {} while(0)
	#endif
	```
4. Modify your grammar to make your errors verbose.
5. Create a `test` task in your `Makefile`:

	```
	test:
		chmod +x ./tests/test_all
		./tests/test_all
	```
6. Run `make test`
7. Submit new tests by forking this repo and submitting a pull request! All tests that should fail go in the `shouldnt_work` folder and all tests that should pass go in the `should_work` folder.

## Adding new tests

Submit new tests by forking this repo and submitting a pull request! All tests that should fail go in the `shouldnt_work` folder and all tests that should pass go in the `should_work` folder.

## Notes

I used the [NameChanger](http://mrrsoftware.com/namechanger/) to number all of the test cases from Logan. Thanks for the test cases Logan!
