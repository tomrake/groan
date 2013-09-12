groan
=====

Testing for grunt tasks.

This is a quest for find out how to debug gruntjs tasks
-----

This quest started with a general web query on testing grunt tasks which resulted in useless advice.
I proceeded to ask the question how do grunt developers debug and test grunt?
The "use the source luke" answer are [The grunt tesing directory](https://github.com/gruntjs/grunt/tree/master/test).


The tasks is the test directory are run by a subgrunt task.

     // Run sub-grunt files, because right now, testing tasks is a pain.
      grunt.registerMultiTask('subgrunt', 'Run a sub-gruntfile.', function() {
        var path = require('path');
        grunt.util.async.forEachSeries(this.filesSrc, function(gruntfile, next) {
          grunt.util.spawn({
            grunt: true,
            args: ['--gruntfile', path.resolve(gruntfile)],
          }, function(error, result) {
            if (error) {
              grunt.log.error(result.stdout).writeln();
              next(new Error('Error running sub-gruntfile "' + gruntfile + '".'));
            } else {
              grunt.verbose.ok(result.stdout);
              next();
            }
          });
        }, this.async());
      });
