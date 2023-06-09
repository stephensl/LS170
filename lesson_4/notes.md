# Working with HTTP 

## Focus Areas
  - HTTP 
    - How it functions at more practical level.
    - text based protocol 
    - Structure of messages
      - set of rules concerned with syntax and structure of messages exchanged between applications. 
      - understanding meaning of rules, and how/when to apply them.
    - Request/Response 
      - continue building mental model of this behavior.

### Netcat 
  - Network utility with variety of features.
    - creating TCP connections between two network end points. 


### Bash 
  - command language for interacting with system environment

  #### Variables
  - declare in Bash using `=` operator, no spaces.
    `name='Lawton'` 
  - may be uppercase, lowercase, combination but case sensitive in referencing them
  
  - Referencing Variables 
    - use `$` prepended to variable name. 
    - we can pass variables as arguments to Bash commands. 
      
      ``` bash 
      echo $name

      # Lawton
      ``` 
    
    - If variable passed without `$` to the `read` command...
      - variable will be assigned to whatever input the `read` command receives.
      
      ```bash 
      read name 

      input 

      echo $name 

      # input 
      ```
  
    - If multiple variables passed to `read` and input a string with multiple words...

    ```bash 
      
    read first second third 

    Do you like apples?

    echo $first  # Do 

    echo $second # you 

    echo $third # like apples?

    ```


#### Bash Files
  - Commands are basically just executable files
    - Can create our own bash files
      - Do not require an extension, but `.sh` applied by convention. 
  
  - Running bash file 
    `bash hello_world.sh` 
      - alternatively, we can specify the mode of execution in the file itself.
        `#!/bin/bash` 
          - the `#!` is a *shebang* and is followed by path to file or program that should be used to run the subsequent code in the bash file. 
            - we're saying we want to use the program at `/bin/bash` to run the code.   
      - In order to run the code now, we must...
        - prepend a file path 
          - `./hello_world.sh`
        - ensure that permissions on file include executable 
          - `chmod +x hello_world.sh` 
            - the `+` indicates that we are adding a permission
            - the `x` specifies that permission is 'execute'

        - Now the file will run from command line...
        ```bash 
        ./hello_world.sh     
        ``` 

  #### Conditional Statements 
  - Allows for conditional logic through `if` statements and `case` statements.
    - `if` statement opens with the `if` command, ends with `fi`. 
    
    ```bash 
    if [[ <condition> ]]   # condition enclosed in square brackets with space between condition and bracket
    then                    # if condition is boolean, no need for brackets
      <commands>
    fi
    ```
  Statement tests truthiness of `<condition>` 
    - if true, executes whatever is between `then` and `fi`

  - Brackets are shorthand for running the `test` command.
    - `test` command provides operators for working with strings, integers, files, etc.

  ##### Operators 
    
    ###### STRINGS
      `-n string` : length of `string` is greater than `0`. 

      `-z string` : length of `string` is `0`.

      `string_1 = string_2` : `string_1` is equal to `string_2` 

      `string_1 != string_2` : `string_1` not equal to `string_2` 


    ###### INTEGERS 
      `-eq` : equal to 

      `-ne` : not equal to

      `-gt` : greater than 

      `-ge` : greater than or equal to

      `lt` : less than 

      `le` : less than or equal to


    ###### FILES 
      `-e path/to/file` : `file` exists

      `-f path/to/file` : `file` exists and is regular file (NOT directory)

      `-d path/to/file` : `file` exists AND IS a directory. 


    

  ### Examples: 
    
    1. Output a string if it is longer than `0`.

    ```bash 
    string='Hello'

    if [[ -n $string ]]
    then 
      echo $string
    fi 
    ```

    2. Compare two integers and output a string if they are equal. 

    ```bash 
    int1=5
    int2=5

    if [[ $int1 -eq $int2 ]]
    then 
      echo "Equality verified" 
    fi 
    ```

    3. Output `File exists` if the file `hello_world.sh` exists.
    
    ```bash 
    if [[ -e ./hello_word.sh ]]
    then 
      echo "File exists"
    fi 
    ```

### Testing for Multiple Conditions 
  - Nested `if` statements 
  
  ```bash 
  integer=4

  if [[ $integer -gt 3 ]]
  then 
    echo $integer is greater than 3

    if [[ $integer -gt 10 ]]
    then 
      echo $integer is also greater than 10
    fi 
  fi 
  ```

  - Two conditional branches using `if/else` 

  ```bash 
  integer=4 

  if [[ $integer -gt 10 ]]
  then 
    echo $integer is greater than 10
  else 
    echo $integer is not greater than 10 
  fi
  ```


  - Three conditional branches using `if/elif/else` 

  ```bash 
  integer=25

  if [[ $integer -lt 0 ]]
  then 
    echo "Your number is negative"
  elif [[ $integer -gt 100 ]]
  then 
    echo "Your number is greater than 100!"
  else 
    echo "Your number is between 0 and 100" 
  fi 
  ```


  - Two conditions using `&&`

  ```bash 
  integer=50 

  if [[ $integer -gt 10 ]] && [[ $integer -lt 100 ]]
  then 
    echo $integer is between 10 and 100. 
  fi
  ```


  - One of two conditions using `||` 

  ```bash 
  integer=50

  if [[ $integer -lt 0 ]] || [[ $integer -gt 100 ]]
  then 
    echo $integer is either less than zero or greater than 100.
  fi
  ```



  - Negating conditions using `!` 

  ```bash 
  integer=8 

  if [[ ! ($integer -lt 5 || $integer -gt 10) ]]
  then 
    echo $integer is between 5 and 10.
  fi
  ``` 


### Loops 

  - while 

  ```bash 
  counter=0 
  max=10 

  while [[ $counter -le $max ]]
  do 
    echo $counter 
    ((counter++))    # increment counter 
  done 
  ```


  - until 

  ```bash 
  counter=0
  max=10

  until [[ $counter -gt $max ]]
  do 
    echo $counter 
    ((counter ++))
  done 
  ```


  - for 
    - iterates through a list

  ```bash 
  numbers='1 2 3 4 5 6 7 8 9 10'

  for number in $numbers
  do 
    echo $number 
  done 
  ```

    - In the above example we assign a variable numbers to a string of numbers separated by spaces, this forms our 'list'. In our for expression we declare a new variable number, and then specify using in that we want to iterate through our $numbers list. The number variable is assigned to the value of each subsequent element in the list on each iteration. The commands between do and done are executed once for each element in the list.


### Bash Functions 
  - Provide way of containing one or more commands as a named 'chunk' of code that may be executed later.
    - Functions can optionally take one or more arguments 

  ```bash 

  greeting () {
    echo Hello $1
  }

  greeting 'Peter'   # outputs 'Hello Peter'

  ```

  - Define function called `greeting`. 
  - Code inside `{}` executed when function is called. 
  - Arguments referenced according to position.
    - First argument passed in has variable `1` assigned to it.
    - Variable is scoped to the function. 
    - Subsequent arguments would have `2`, `3`, `4`, etc. assigned. 

    ```bash 

    greeting () {
      echo "Hello $1"
      echo "Hello $2"
    }

    greeting 'Peter' 'Paul' 

      # Hello Peter
      # Hello Paul 
    ```



## Working with netcat 
  - network utility for reading and writing data across network connections using TCP or UDP. 


### Practicing setting up HTTP server
```bash

#!/bin/bash

# define function called server

function server () {

}


# set up coprocess

# allows us to run server function asynchonously alongside our nc command.

# naming process SERVER_PROCESS and telling it to execute server function.

coproc SERVER_PROCESS { server; }




# executing nc command.

# executes nc in listen and verbose mode, and sets it to listen for incoming connections on port 2345. 

# After port number is redirection of STDOUT and STDIN.

# Input nc receives can be accessed within the server function using the read command. 

# Any output from server function will be output by nc. 
nc -lv 2345 <&${SERVER_PROCESS[0]} >&${SERVER_PROCESS[1]}
```




## Summary 
  - HTTP is a *text-based* protocol. 
    - HTTP request/response involve sending text between client and server. 

  - In order for protocol to function correctly...
    - Request and Response must be structured in a way that client and server understand. 

  - HTTP/1.1 the end of the headers is indicated by an *empty line* 

  - The `Content-Length` header can be used to indicate the size of the body. 
    - This helps determine where the HTTP message should end. 


    