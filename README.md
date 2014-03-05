Provisioning an Ubuntu 12.04 instance with MongoDB using Chef, following Ch 11.3 - 'MongoDB' 
in Ben Dixon's Leanpub __Reliably Deploying Rails Applications__ ([find here](https://leanpub.com/deploying_rails_applications)).
### Dependencies

* ruby (2.0)
* knife-solo (0.4)
* berkshelf (2.0)

### Commands

(2. is inessential after a server been prepared by knife solo.)

1. berks install
2. knife solo prepare root@\<my server ip\>
3. knife solo cook root@\<my server ip\>

### Result
The foregoing got MongoDB onto my server, but access to the Mongo shell was not as the chapter indicated. 
````
mongod
````
...resulted in
````
*********************************************************************
 ERROR: dbpath (/data/db/) does not exist.
  Create this directory or give existing directory in --dbpath.
   See http://dochub.mongodb.org/core/startingandstoppingmongo
   *********************************************************************
````
...which I cured with
````
mongod --dbpath /var/lib/mongodb/ --port 12345
````
...(the default mongo port was already occupied on my server, hence '12345'.) To access the Mongo shell
I opened another shell and entered
````
mongo --host localhost:12345
````
...after that everything was as described in Ben's chapter.
