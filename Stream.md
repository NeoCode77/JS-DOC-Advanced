# Stream 

> stream adalah suatu proses membaca dan menulis sebuah data dengan mengalirkan chunks per chunks sehingga dapat menghemat penggunaan memori.

**A. Readable Stream**

> sebuah proses membaca data dengan mengalirkan chunks per chunks dan menghasilkan chunks berupa buffer.
> yang termasuk readable stream adalah *request dari klien , readable file , dan stdin*.

|event|deskripsi|
|----|-----|
|data|menjalankan proses membaca dan menghasilkan data buffer|
|ready|akan dijalankan sebelum proses membaca dimulai|
|end|akan dijalanakan sesudah proses membaca| 
|pause|akan dijalankan ketika proses membaca dipause|
|resume|akan dijalanakan ketika proses membaca diresume|

|method|deskripsi|
|----|-----|
|pause|melakukan pause stream data|
|resume|melakukan resume stream data|
|on|menghandle event stream|

 ```javascript
 let fs = require("fs");
 
 let readFile = fs.createReadStream("file.txt");
 
 readFile.on("data",(chunks) => {
    console.log(chunks);              // chunks berupa buffer
    console.log(chunks.toString());   // mengubah buffer ke bentuk string
 })
 
 readFile.on("ready",() => {
    console.log("stream dimulai !!!");
 })
 
 readFile.on("end",() => {
    console.log("stream selesai !!!");
 })
 
 readFile.on("resume",() => {
    console.log("stream resume !!!");
 })
 
 readFile.on("pause",() => {
    console.log("stream pause !!!");
 })
 ```

**B. Writeable Stream**

> sebuah proses menulis data dengan mengalirkan chunks per chunks dan menghasilkan chunks berupa buffer.
> yang termasuk writeable stream adalah *response dari klien , writeble file , dan stdout*.

|event|deskripsi|
|----|-----|
|ready|akan dijalankan sebelum proses menulis dimulai|
|finish|akan dijalanakan sesudah proses menulis| 
|error|akan dijalankan ketika terjadi error|


|method|deskripsi|
|----|-----|
|write|menuliskan data pada stream|
|on|menghandle event stream|

 ```javascript
 let fs = require("fs");
 
 let writeFile = fs.createWriteStream("file.txt");
 writeFile.write("hello world");
 writeFile.write("my name is budi");
 
 readFile.on("ready",() => {
    console.log("stream dimulai !!!");
 })
 
 readFile.on("finish",() => {
    console.log("stream selesai !!!");
 })
 
 readFile.on("error",(err) => {
    console.log("stream error : " + err);
 })
 ```
 
 **C. Pipe**
 
 >pipe digunakan untuk mengalirkan data dari readable ke writeable.

```javascript
let fs = require("fs");

let fileRead = fs.createReadStream("file1.txt");
let fileWrite = fs.createWriteStream("file2.txt");

fileRead.pipe(fileWrite);
```

**D. Transfrom**
 
 >transform digunakan untuk memodifikasi data yang dialirkan dari readable ke writeable.

```javascript
let fs = require("fs");
let { Transform } = require("stream");

let fileRead = fs.createReadStream("file1.txt");
let fileWrite = fs.createWriteStream("file2.txt");

let modify = new Transform({
    transform: function(chunks,encoding,calback){
          let kapital = chunks.toString().toUpperCase();
          callback( null , kapital );
    });
};

fileRead.pipe(modify).pipe(fileWrite);
```
