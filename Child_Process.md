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

**E. Spawn**

>method asynchronous yang digunakan untuk melakukan command shell/bash dan menghasilkan stream.
>untuk menjalankan spawn di os windows harus disertakan opsi *{ shell : true }*.

```javascript
// windows
let { spawn } = require("child_process");

let command = spawn( "dir", { shell : true });

command.stdout.on("data",( chunks ) => {
    console.log( chunks.toString() );
});

command.stderr.on("data",( chunks ) => {
    console.log( chunks.toString() );
});

command.on("exit" , (code) => {
    console.log( "program exit with code", code );
});

command.on("error" , ( err ) => {
    console.log( err );
});
```

**F. spawnSync**

>method synchronous yang digunakan untuk melakukan command shell/bash dan menghasilkan stream.
>untuk menjalankan spawn di os windows harus disertakan opsi *{ shell : true }*.

```javascript
let { spawnSync } = require("child_process");

let command = spawnSync( "ls -l" );

if( command.err ){
    console.log( command.err.message );
}else if( command.stderr.toString() ){
    console.log( command.stderr.toString() );
}else{
    console.log( command.stdout.toString() );
};
```
