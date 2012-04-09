# Weathermap-Archive
      
  Insanely small and simple application to archive and view your weathermaps (or any periodically generated images).
  This is an simple solution to get an overview of your networks usage evolution along the time. Most of the time,
  you MRTG will provide you with individual link usage over the time while a weathermap will give you an instant overview.
  But sometimes, you need to get a global view of your network along the time.
  
  I got the original idea when I was working for the IXP of Lyon (http://www.rezopole.net). We had a minor outage and I 
  really missed a proper archiving system.
  
  As a demo, I archive all weathermaps from OVH, a French Hosting compagny. http://ovh.jtlebi.fr/

## Installation

  This applications uses 2 modules.
  
  * Archiving engine
  * Web Interface / REST API
  
  Get the code 
    
    git clone https://github.com/jtlebi/Weathermap-archive.git
  
  Create a folder to hold the weathermaps
    
    $ mkdir -p /path/to/archive
  
  Adapt the example script in /path/to/code/bin/ovh.sh and add a rule to your cron

    $ vim /etc/crontab
    
    ```
    */5 * * * * root /path/to/code/bin/ovh.sh #run every 5 minutes
    ```
    
    Please not that it is highly recommended to create a dedicated unpriviledged user !
  
  Copy and edit conguration file
    
    $ cp /path/to/code/config/config.json.dist /path/to/code/config/config.json
  
  Install dependancies and Run it (tm) !
    
    $ cd /path/to/code/
    $ npm install -d
    $ cd src
    $ node server.js

  Next step :
    
    * create a dedicated unpriviledged user
    * make a start script

## Features

 * Periodically archive weathermaps via a cron script
 * Provide an easy API
 * Provide a simple and intutive interface to navigate the archived weathermaps
 * 2 level of categorizations
 ** top level group (organizations, units)
 ** map name
 
## API

  The provided API is a simple wrapper around the filesystem with some bonus security checks :). It aims to ease
  building any application relying in the archived data.
  All request are GET only and the answers are JSON.
  
  * GET /wm-api/groups => get a list a groups for which we have archives
  * GET /wm-api/:groupname/maps => get a list of available maps for this group
  * GET /wm-api/:groupname/:mapname/dates => get list of archived days
  * GET /wm-api/:groupname/:mapname/:date/times => get a list of archived time for this date
  * GET /wm-api/:groupname/:mapname/:date/:time.png => get a given map
  * GET /wm/ => static app files (Not really an API)
 
## Dependancies

  This application would not have been possible without some amazing external projects. Here is small list of these
  
  * Node.js > 0.6
  * Restify
  * Connect.js
  * Ember.js
  * Bootstrap

## License 

(The MIT License)

Copyright jtlebi.fr &lt;admin@jtlebi.fr&gt; and other contributors.

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
