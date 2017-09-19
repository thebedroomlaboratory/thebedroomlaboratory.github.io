---
title: AWS Environment set up for Maker 2014
date: 2014-06-26T16:35:23+00:00
author: jonni3darko
categories:
  - Projects
---
![](/wp-content/uploads/2014/06/aws1.png)

As part of our Maker 2014 project we decided to utilise an AWS server Martin had signed up to. While we will probably end up using a local server on the day we thought it was a good opportunity to give AWS a test run. As well as giving us a way to share an environment while working as a distributed team, the process of setting up the AWS will serve to document the setup we require for our project. The aim would be to later create a script that does all the installs and setups for us.

Originally posted on [jonnie.io](http://blog.jonnie.io/aws-environment-set-up-for-maker-2014/)

**Note: at the time of writing, this is a work in progress and I hope to keep it updated**

So what do we need to install & setup?

  * [Before we start](#beforestart)
  * [Node.js](#nodesetup)
  * [Mongodb](#Mongodbsetup)

<a name="beforestart"></a>

### Before we start

Lets make sure everything is update on our system using `apt-get`:

<pre><code class="lang-bash">   &lt;span class="hljs-built_in">sudo&lt;/span> apt-get upgrade 
   &lt;span class="hljs-built_in">sudo&lt;/span> apt-get update
</code></pre>

<a name="nodesetup"></a>

# Node.js Setup

What is Node.js? It is a Server-side implementation of the Javascript platform which allows rapid development of applications. This is particularly true if you are using complete Javascript stack such as [MEAN]() (MongoDB, Express.js,Angular.js & Node.js) as development can be more consistent and be designed within the same system. This make rapid prototyping and proof of concept that much quicker.

![nodejs.org](https://cloud.githubusercontent.com/assets/3673943/3397003/7ab4c020-fd17-11e3-8c71-5f972dafdeba.jpg)

From my research online I have found that it is suggested building Node.js from source as packages in the Advanced Packaging Tool (AptGet) do not work always or are outdated at times on Ubuntu. So the first thing we need to do is install the some dependences required for building Node.js

  * [build-essential](http://packages.ubuntu.com/lucid/build-essential) which is used to build Debian packages
  * [lamp-server](https://help.ubuntu.com/community/ApacheMySQLPHP) which installs Apache, MySQL & PHP for linux

<pre><code class="lang-bash">   &lt;span class="hljs-built_in">sudo&lt;/span> apt-get install build-essential lamp-server^
</code></pre>

Next we need to get the node packages to build, I went with v0.10.22 as I knew it was a stable release but if you wish to go for a newer version check out the [Node.js dist](http://nodejs.org/dist/) site for the verion number of your choice

<pre><code class="lang-bash">   &lt;span class="hljs-comment">#Get Node package&lt;/span>
   wget http://nodejs.org/dist/v0.&lt;span class="hljs-number">10.22&lt;/span>/node-v0.&lt;span class="hljs-number">10.22&lt;/span>.tar.gz
   &lt;span class="hljs-comment">#unarchive it&lt;/span>
   tar -xvzf node-v0.&lt;span class="hljs-number">10.22&lt;/span>.tar.gz
</code></pre>

Next we need to move to the node directory, run the configuration script, build it and then install it

<pre><code class="lang-bash">  &lt;span class="hljs-comment">#Move into directory&lt;/span>
  &lt;span class="hljs-built_in">cd&lt;/span> node-v0.&lt;span class="hljs-number">10.22&lt;/span>
  &lt;span class="hljs-comment">#Run the configuration script&lt;/span>
  ./configure
  &lt;span class="hljs-comment">#Build it&lt;/span>
  make
  &lt;span class="hljs-comment">#Install Node&lt;/span>
  &lt;span class="hljs-built_in">sudo&lt;/span> make install
</code></pre>

The configuration script just sets up what ever environment variables required and performs checks required to build Node for our platform

The `make` utility is to determine automatically which pieces of Node.js needs to be recompiled, and issues the commands to recompile them. 

Node should be all set now so let&#8217;s test by checking the version

<pre><code class="lang-bash">   node -v
   &lt;span class="hljs-comment">#Should output something like the following depending on the version you installed: v0.10.22&lt;/span>

   npm version
   &lt;span class="hljs-comment"># should out put something like&lt;/span>
   &lt;span class="hljs-comment"># { http_parser: '1.0',&lt;/span>
   &lt;span class="hljs-comment">#   node: '0.10.22',&lt;/span>
   &lt;span class="hljs-comment">#   v8: '3.14.5.9',&lt;/span>
   &lt;span class="hljs-comment">#   ares: '1.9.0-DEV',&lt;/span>
   &lt;span class="hljs-comment">#   uv: '0.10.19',&lt;/span>
   &lt;span class="hljs-comment">#   zlib: '1.2.3',&lt;/span>
   &lt;span class="hljs-comment">#   modules: '11',&lt;/span>
   &lt;span class="hljs-comment">#   openssl: '1.0.1e',&lt;/span>
   &lt;span class="hljs-comment">#   npm: '1.3.14' }&lt;/span>
</code></pre>

<a name="Mongodbsetup"></a>

## Mongodb Setup

MongoDB is an open-source document database, and the leading NoSQL database. Among its features it includes JSON-style documents with dynamic schemas which offer simplicity and power. This is especially useful with node since we are already working with Javascript, and in a prototyping and rapid development environment it means we don&#8217;t have to get hung up on our models and can change them on the fly.

We will use `.deb` packages to install MongoDB. While Ubuntu includes its own MongoDB packages, the official MongoDB packages are generally more up-to-date.
  
So the first thing we need to do is add the [MongoDB public GPG Key](http://docs.mongodb.org/10gen-gpg-key.asc) 

<pre><code class="lang-bash">   &lt;span class="hljs-built_in">sudo&lt;/span> apt-key adv --keyserver hkp://keyserver.ubuntu.com:&lt;span class="hljs-number">80&lt;/span> --recv &lt;span class="hljs-number">7&lt;/span>F0CEB10
</code></pre>

Create the /etc/apt/sources.list.d/mongodb.list list file using the following command:

<pre><code class="lang-bash">   &lt;span class="hljs-built_in">echo&lt;/span> &lt;span class="hljs-string">'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen'&lt;/span> | &lt;span class="hljs-built_in">sudo&lt;/span> tee /etc/apt/sources.list.d/mongodb.list
</code></pre>

Now we need to reload local package database

<pre><code class="lang-bash">   &lt;span class="hljs-built_in">sudo&lt;/span> apt-get update
</code></pre>

Install mongoDB

<pre><code class="lang-bash">   &lt;span class="hljs-built_in">sudo&lt;/span> apt-get install mongodb-org
</code></pre>

Create /data/db which is where our schemas will be stored (this may require sudo)

<pre><code class="lang-bash">   mkdir /data/db
</code></pre>

Make sure you change the permissions of this folder so that you do not require sudo, I did this by giving my username and a specific group access

       sudo chown -R username.groupname /data/db
    

Finally you can start running MongoDB with the command `mongod` Or `sudo /etc/init.d/mongod start`.
  
Again I recommend changing the permissions so that sudo is not required.

#### Coming soon&#8230;.. 

I will follow thing up with a tutorial on creating a minimal starting point for a Node Restful service which we will eventually use to communicate with our arduino, intel galileo and Raspberry Pi (I will also follow up on getting a similar setup installed on a Pi)

<div style="display:none">
  <h5 id="sources">
    Sources
  </h5>
  
  <ul>
    <li>
      <a href="http://askubuntu.com/questions/328681/installing-the-latest-node-js-mongodb">http://askubuntu.com/questions/328681/installing-the-latest-node-js-mongodb</a>
    </li>
    <li>
      <a href="http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/">http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/</a>
    </li>
    <li>
      <a href="http://stackoverflow.com/questions/5300861/mongodb-only-works-when-run-as-root-on-ubuntu-data-directory-issue">http://stackoverflow.com/questions/5300861/mongodb-only-works-when-run-as-root-on-ubuntu-data-directory-issue</a>
    </li>
  </ul>
</div>