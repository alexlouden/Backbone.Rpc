fs = require 'fs'
exec = require('child_process').exec

task 'build', 'batch execute everything', () ->
  invoke 'clean'
  invoke 'build:lint'  
  invoke 'test'  
  invoke 'build:document'
  invoke 'build:concat'
  invoke 'build:minify'

task 'clean', 'cleaning up dist and docs folder', () ->
  console.log 'Cleaning up dist and docs folder'
  fs.unlink 'docs'

task 'test', 'running tests with phantom', () ->
  console.log 'Running tests'
  exec 'phantomjs --local-to-remote-url-access=yes bin/phantomjs.js', (error, stdout, stderr) -> 
    console.log stdout
    console.log stderr
    if error != null
      console.log error

task 'build:document', 'generates docs with docco', () ->
  console.log 'Creating documentation'
  exec 'docco src/backbone.rpc.js', (error, stdout, stderr) -> 
    console.log stdout
    console.log stderr
    if error != null
      console.log error

task 'build:concat', 'adds the license tag to the output file', () ->
  console.log 'Adding license tag to the output file'
  rpc = fs.readFileSync 'src/backbone.rpc.js', 'utf-8'
  license = fs.readFileSync 'license.txt', 'utf-8'
  fs.writeFileSync 'backbone.rpc.js', license + '\n\n' + rpc, 'utf-8'

task 'build:minify', 'minifies the plugin', () ->
  console.log 'Minifiying the plugin'
  exec 'uglifyjs -o backbone.rpc.min.js backbone.rpc.js', (error, stdout, stderr) -> 
    console.log stdout
    console.log stderr
    if error != null
      console.log error

task 'build:lint', 'lints the plugins src file', () ->
  console.log 'Linting the plugin'
  child = exec 'nodelint -h', (error, stdout, stderr) -> 
    console.log 'out ' + stdout
    console.log 'err ' + stderr
    if error != null
      console.log 'error ' + error

task 'pages:copyDocs', 'copies the current docs to the pages folder', () ->
  console.log 'Copy docs'