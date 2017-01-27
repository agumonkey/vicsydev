# [vicsy/dev](https://github.com/codr4life/vicsydev) | lispy tests
    
### preramble
I prefer my tests simple and flexible, designed around the application rather than imposed on it. These days, I usually start with basic functions and assertions; and add what I need when I need it. The holy grail is a reusable library that allows the same progressive approach without getting in the way, while helping out with more elaborate tasks like test discovery, grouping and benchmarking. This post describes the humble beginnings of that library in Common Lisp.

### tags
Each test carries a unique set of tags in it's definition. When running tests, a set of tags may be specified to only trigger tests matching all specified tags. An optional set of tags to skip may also be specified; tests matching any specified tags are skipped, which allows excluding non relevant tests within the triggered set. The approach relies on creativity with a touch of discipline when specifying tags; but the process is gradual and non-intrusive, Just add whatever tags needed to accomplish what needs to be done and to take advantage of any patterns that emerge. 

<script src="https://gist.github.com/codr4life/3f0a91c5704ae771aa76fb59761b52bc.js"></script>

### benchmarking
Premature optimisation is the root of many problems, but so is not having any idea about the performance of your code. Unfortunately, I've found that most test frameworks don't even bother with benchmarks, and the ones that do require too much ceremony. There are no rational reasons for separating benchmarks and tests, the framework described here comes with the ability to run any set of tests as a benchmark with specified number of warmups and repetitions.

<script src="https://gist.github.com/codr4life/6f9e94c7473de2c372930d4d3b44d833.js"></script>

<script src="https://gist.github.com/codr4life/4570b9849db331329b2b9979b89dad12.js"></script>
    
### fixtures
I prefer my fixtures to wrap around tests, to allow using block statements for allocating and releasing resources. Like tests, fixtures are uniquely identified by a set of tags. When running tests, fixtures matching skipped tags will not run.

<script src="https://gist.github.com/codr4life/c1a4ba8160f897e304cfce4919565a59.js"></script>

### implementation
Included below is the complete implementation of all functionality described here, it's trivial enough to clone and own if you feel like tweaking it. Besides a few custom [utilities](https://github.com/codr4life/cl4l/blob/master/utils.lisp), it uses [unique indexes](https://github.com/codr4life/cl4l#indexes) for mapping tags to tests and fixtures in order; the same thing could be accomplished with (gensym), (intern), built-in sets and manual sorting if you prefer more code in your code.

<script src="https://gist.github.com/codr4life/a7c73dd6b64a39ed6e3af3cf56b19ce7.js"></script>

### but
I've been playing around with this approach for 20 years now, and have yet to find a language where it isn't doable enough to improve on the status quo. The excuses usually offered for enforcing more ceremonial test procedures are mostly about CI; and CI in itself is mostly process fluff to cover up for lacking culture.
    
### peace, out
You may find more posts in the same spirit <a href="http://vicsydev.blogspot.de/">here</a>, and a full implementation of this framework and more <a href="https://github.com/codr4life/cl4l">here</a>.