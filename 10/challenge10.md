# Challenge 10

Download the challenge from [here](flava.pcap)

## Overview

You're given a packet capture of the network traffic of a colleague who was infected by a malware!

For a start, search through the PCAP file to find out what is suspicious within it!

**[Activity]** Find the suspicious traffic!

Is the traffic readable? Could you try to figure out what it is up to?

I'm providing you with a useful tool that can help you figure things easily!

```
/**
 * requires node.js with ES6 support, or babel
 */
'use strict';

const vm = require('vm');
const fs = require('fs');

const __loggers__ = {};
function log(tag) {
  if (__loggers__.hasOwnProperty(tag))
    return __loggers__[tag];

  return (__loggers__[tag] = function() {
    let args = [].slice.call(arguments).map(e => typeof e === 'string' ? `"${e}"` : e);
    console.log(`>> ${tag}(${args})\n`);
  });
}

class EvalLogger {
  constructor(opt) {
    this.opt = opt || {};
    let sandbox = this.sandbox = {
      __Function__: code => (() => sandbox.eval(code)),
      document: {
        write: log('document.write'),
        writeln: log('document.write'),
      }, 
      alert: log('alert')
    };
    let self = this;
    // hook eval
    ['setTimeout','fromChar','charAt','substr', 'setInterval', 'window','jQuery','$','eval','reduce','copyTo','charCodeAt','Stringify'].forEach(func => sandbox[func] = (() => {
      return code => {
        log(func)(code);
        return self.run(code);
      }
    })());

    // hook function constructor
    let context = self.context = vm.createContext(sandbox);
    let monkeyPatch = new vm.Script('\'use strict\';Function.prototype.constructor = __Function__;');
    monkeyPatch.runInContext(context);
  }

  run(code) {
    code = (code || '') + '';
    
    let jjencodePrefix = 'return';
    if (code.indexOf(jjencodePrefix) === 0) {
      code = `(function () {${code}})()`;
    }

    try {
      return vm.runInContext(code, this.sandbox, {timeout: 100000});
    } catch(err) {
      console.error(`[*] "${err}" occured while executing `);
    }
  }
}

if (process.argv.length === 3) {
  const fileName = process.argv[2];
  if (!fileName.match(/^\-h$/i)) {
    let content = fs.readFileSync(fileName).toString('utf8');
    new EvalLogger().run(content);
    process.exit();
  }
}

console.log('Usage: node ${process.argv[1]} [filename]')
```

Once you figure out most of these, you'll should hit a wall where you need some brute-forcing!

Due to time constraints:

```
a = 0x8ede69460cac52c9b467d795fecd1 
```

You will understand what the above is used for when you see it!

## Stage 2! SWF

There are few ways to decompile SWF files. For this particular challenge I'd recommend [https://www.free-decompiler.com/flash/download/](https://www.free-decompiler.com/flash/download/)!

**[Activity]** Go ahead and solve the first layer using the key you get from the previous stage!

Look at layer 2, what do you have to do now??

You're almost there! Everything should be pretty high-level and straightforward now!

**[Activity]** Solve them all!