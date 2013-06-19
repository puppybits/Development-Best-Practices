# Rules
* Everyone's code could be less buggy and more flexible. Don't take feedback personal.

# Goals for reviewing code
* Keep sub-optimal code from getting in the code base.
* Collectively share knowledge and become better developers.

# Pull Request Process
* create a git branch `git checkout -b 'my_feature'`
* commit to the git branch frequently. (ie 4 or 5 times a day)
* push your git branch to GitLab at least once a day `git push origin my_feature`
* when you task is complete go to the git lab site and create a pull request
* email everyone about your code review and give them 24 hours to review your code.

# What to review
1. **are the dependencies minimized as much as possible?** 
 1. good choice of efficient data types for the use/access pattern.
 2. what OO pattern is being used and is it the right pattern for the job?
 3. is the public interface only exposing the bare minimum?
 4. does each public and private minimize use to objects outside of the local scope?
2. is the architect following with best practices?
3. is the code only building for what today's requirements are?
4. is the architect flexible?
5. how could this function break? (look at param data structures)
6. does it follow the coding styles guidelines?
