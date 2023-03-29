# Child Process

**A. Exec**

>method asynchronous yang digunakan untuk melakukan command shell/bash.

```javascript
let { exec } = require("child_process");

exec( "ls -l" , ( err , stdout , stderr ) => {
    if( err ){
      console.log( err );
    }
    
    if( stderr ){
      console.log( stderr );
    }
    
    console.log( stdout );
});

```

**B. ExecSync**

>method synchronous yang digunakan untuk melakukan command shell/bash.

```javascript
let { execSync } = require("child_process");

let command = execSync( "ls -l" );

console.log( command.toString() );

```

**C. ExecFile**

>method asynchronous yang digunakan untuk menjalankan file bash(.sh).

```javascript
let { execFile } = require("child_process");

execFile( "./bash.sh" , ( err , stdout , stderr ) => {
    if( err ){
      console.log( err );
    }
    
    if( stderr ){
      console.log( stderr );
    }
    
    console.log( stdout );
});

```

**D. ExecFileSync**

>method synchronous yang digunakan untuk menjalankan file bash(.sh).

```javascript
let { execFileSync } = require("child_process");

let command = execFileSync( "./bash.sh" );

console.log( command.toString() );

```
