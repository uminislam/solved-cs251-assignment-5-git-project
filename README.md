Download Link: https://assignmentchef.com/product/solved-cs251-assignment-5-git-project
<br>



<ol>

 <li>Create a new Git project in https://git.cse.iitk.ac.in/ or in https://github.com/</li>

 <li>(Optional but recommended) Add your computer’s public SSH key by following the instructions at https://git.cse.iitk.ac.in/help/ssh/README</li>

 <li>Now that you’ve successfully setup a central git repository, clone it once locally in your PC. (using git clone at a folder named “user_1”)</li>

 <li>To simulate a multi-user usage of your newly created central git repo, clone the repository again in another folder (a folder named “user_2”).</li>

 <li>Let us think of activities in the first clone as user_1’s activity and the activities in second clone as user_2’s activity. Re-enact the activities of user_1 and user_2 in the following order.</li>

</ol>

<table width="0">

 <tbody>

  <tr>

   <td width="321">As User_1 (i.e. first clone),6.                  Add a simple hello.c program that prints “HelloWorld” in main() and compile it.hello.c#include&lt;stdio.h&gt;void main(){printf(“Helloworld!
”);}a.out7.                  Stage and Commit the code and the *.out binary. (using git add, git commit)8.                  Push these committed changes to the origin master (using “git push” or “git push -u” to set the upstream tracking reference)</td>

   <td width="321"> </td>

  </tr>

  <tr>

   <td width="321"> </td>

   <td width="321">As User_2 (i.e. second clone),9. Pull upstream changes into your local repository. (using git pull)</td>

  </tr>

  <tr>

   <td width="321">As User_1,10. You’re in the middle of a feature addition, so add a new line into your main().hello.c#include&lt;stdio.h&gt;void main(){printf(“Helloworld!
”);printf(“This must be a monolithic                 design
”);}</td>

   <td width="321"> </td>

  </tr>

 </tbody>

</table>




<table width="0">

 <tbody>

  <tr>

   <td width="321">11. Stage and Commit but do not push yet as you went to grab a cup of coffee.</td>

   <td width="321"> </td>

  </tr>

  <tr>

   <td width="321"> </td>

   <td width="321">As User_2,12. You’re simultaneously working on the same piece of code and have added a different feature.hello.c#include&lt;stdio.h&gt;             void microkernel_sendmsg(char *);void main(){printf(“Helloworld!
”);                 microkernel_sendmsg(“is more                 portable”);}void microkernel_sendmsg(char *a){                 printf(“microkernel: %s
”, a);}13. Stage, Commit and Push.</td>

  </tr>

  <tr>

   <td width="321">As User_1,14.              Try pushing to remote. You can now no longer push to the origin/master as your code is not up-to-date, git push will fail.15.              Pull and Resolve the merge conflicts (in hello.c and a.out) so that all of the newly added features (the print messages and function calls) work. (using git pull, git diff)Manual merge conflict resolution is required in hello.c to get the following#include&lt;stdio.h&gt;                 void microkernel_sendmsg(char *);void main(){printf(“Helloworld!
”);printf(“This must be a monolithic                     design
”);microkernel_sendmsg(“is more                     portable”);}void microkernel_sendmsg(char *a){                     printf(“microkernel: %s
”, a);} </td>

   <td width="321"> </td>

  </tr>

 </tbody>

</table>




<table width="0">

 <tbody>

  <tr>

   <td width="321">16. The binary (a.out) might also require merge conflict resolution. But as we do not need to track binaries, delete it (a.out), add the pattern “*.out” to a .gitignore file so that the binaries won’t be tracked anymore, stage, commit and push all these changes (removed a.out, updated hello.c and added .gitignore).</td>

   <td width="321"> </td>

  </tr>

  <tr>

   <td width="321"> </td>

   <td width="321">As User_2,17.              Pull the updates. It is not good practise to work directly in the master branch. Create a new branch called “feature_addition_getmsg” (using git branch and git checkout)18.              Make changes so that the hello.c now looks like this,#include&lt;stdio.h&gt;void microkernel_sendmsg(char *);             void microkernel_getmsg(char *);void main(){printf(“Helloworld!
”);printf(“This must be a monolithic                 design
”);microkernel_sendmsg(“is more                 portable”);}void microkernel_sendmsg(char *a){                 printf(“microkernel: %s
”, a);}void microkernel_getmsg(char *b){//TODO: getmsg feature}19. Commit and Push (since new branch you may have to use git push –set-upstream).</td>

  </tr>

  <tr>

   <td width="321">As User_1,20. Similarly User_1 has also created a branch called “feature_removal_sendmsg” from master with an intention to locally experiment on the master code without the sendmsg feature, thus changing hello.c to the following,#include&lt;stdio.h&gt;void main(){printf(“Helloworld!
”);printf(“This must be a monolithic             design
”);</td>

   <td width="321"> </td>

  </tr>

 </tbody>

</table>




<table width="0">

 <tbody>

  <tr>

   <td width="321">        }21.              As this is a local experiment, no need to pushthese changes, simply add and commit.22.              Pull from remote to get new branches fromUser_2. The feature_addition_getmsg branch of User_2 must be now downloaded and locally accessible to you. (using git pull and git branch -a)23.              As the new “feature_addition_getmsg” from user_2 looks intriguing, you would like to test these changes with your own experiment work “feature_removal_sendmsg”.24.              So create a new branch called“testing_no_sendmsg_with_getmsg” from the “feature_removal_sendmsg” branch and merge the “feature_addition_getmsg” branch into it. (using git branch, git checkout, git merge)Resolve the merge conflict resolutions so that hello.c in “testing_no_sendmsg_with_getmsg” looks like#include&lt;stdio.h&gt;void main(){printf(“Helloworld!
”);printf(“This must be a monolithic                 design
”);}void microkernel_getmsg(char *b){//TODO: getmsg feature}25. Add, Commit and Push the branch upstream.</td>

   <td width="321"> </td>

  </tr>

  <tr>

   <td width="321">As User_1,26. Checkout to master branch and edit hello.c so that you introduce an error or warning.#include&lt;stdio.h&gt;void main(){printf(“Helloworld!
”);printf(“This must be a monolithic             design
”);microkernel_sendmsg(“is more             portable”);</td>

   <td width="321"> </td>

  </tr>

  <tr>

   <td width="321">        }void microkernel_sendmsg(char *a){             printf(“microkernel: %s
”, a);}27.              Commit and push this erroneous code.28.              Since now you’ve tainted the master branch, you need to revert these changes before the boss gets to know that you’ve broken the production code.29.              Use git revert to revert the master branch to the previous commit, effectively undoing the last change, and push it back asap!Note that this doesn’t hide the tainted commit on the history of commits but only reverts it. So it is still possible to identify the culprit!</td>

   <td width="321"> </td>

  </tr>

  <tr>

   <td width="321"> </td>

   <td width="321">30. As User_2, make some changes to the hello.c in master branch and communicate these changes to User_1’s hello.c in master branch using patch files. (using “git format-patch” on sender side to generate a “.patch” file and “git am” on receiver side to apply this patch).</td>

  </tr>

 </tbody>

</table>