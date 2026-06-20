
---------------------------------------------
**section 2 - Intro to node.js**
------------------------------------------------------------------
vid 5 

| node.js pros                                                   | use node.js                 |
| -------------------------------------------------------------- | --------------------------- |
| single threaded, based on event driven, non-blocking i/o model | Api with database behind it |
| suitable to build fast and scalable data intensive apps        | data streaming              |
| big interprises start to use it                                | real time chat apps         |
| faster, have npm which is free package for everyone            | server side web application |
vid 6
- the file system require calling that make the object built in the module 'fs' and will able us to use all of this function and objects
vid 8
 ```
 fs.readFileSync(`./txt/input.txt`, 'utf-8') \\ variable to read the file and we start with the Home folder which the node'js is located , we add between arrows the path of file and the protocol of language 
 ```
 - and now we can explain how to view the way of writing in file 
```
const txtout = 'this is what we know about the avocado'
fs.writeFileSync('./txt/output.txt', textout) // iside the arrows we add path also , the text variable we want to add to file  
```
--------------------------------------------
vid 9 
- synchronous is blocking code due to execution every line by line 
- asynchronous is non-blocking code because the lines take more execution time is running at the background 
- for each node.js app is single thread and all users of app use only one thread
-  we use so many callback functions in node.js
---------------
vid10
we here talking about reading and writing files 

```
fs.readFile('./txt/start.txt','utf-8',(err, data)=>{console.log(data)})
console.log('will read file')
```
this is the type of the reading file without any blocking the run time for other features in code 
```
//Non-Blocking, asynchronous way
fs.readFile('./txt/start.txt', 'utf-8', (err, data1) => {
  fs.readFile(`./txt/${start}.txt`, 'utf-8', (err, data2) => {
    console.log(data2);
    fs.readFile('./txt/append.txt', 'utf-8', (err, data3) => {
      console.log(data3);
      fs.writeFile('./txt/final.txt', `${data2}\n${data3},'utf-8`, err => {
        console.log('your file has been written');
      });
    });
  });
});
console.log('Will read file!');
```
- this is the way to show how the queue inside the background compiling which function have the priority first 
- error handling here appear only when the txt file doesn't exist on the folder so there are no real test to error handler or something